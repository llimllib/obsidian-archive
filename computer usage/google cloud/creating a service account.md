login:
`gcloud auth login`

show the available projects:
`gcloud projects list`

set the current project, pick one from the list:
`gcloud config set project <project_id>` to set

make sure the services you need are enabled:
`gcloud services enable bigquery.googleapis.com [other services here...]` 

- if you need a list of all services: `gcloud services list --available`

create a service account:
```
gcloud iam service-accounts create \
    bigquery-dev-user \
    --description="Service account for my app to dump data into bigquery"
    --display-name="bigquery-dev-user"
```

Find the roles you want to give your service account. For me, I want to give the service account permissions to write and read big query data, so I used:

```
$ gcloud iam roles list | grep bigq
name: roles/bigquery.admin
name: roles/bigquery.connectionAdmin
name: roles/bigquery.connectionUser
name: roles/bigquery.dataEditor
name: roles/bigquery.dataOwner
name: roles/bigquery.dataViewer
name: roles/bigquery.filteredDataViewer
name: roles/bigquery.jobUser
name: roles/bigquery.metadataViewer
name: roles/bigquery.readSessionUser
name: roles/bigquery.resourceAdmin
name: roles/bigquery.resourceEditor
name: roles/bigquery.resourceViewer
name: roles/bigquery.user
name: roles/bigqueryconnection.serviceAgent
name: roles/bigquerydatapolicy.maskedReader
description: 'Gives BigQuery Data Transfer Service access to start bigquery jobs in
name: roles/bigquerydatatransfer.serviceAgent
name: roles/bigquerymigration.editor
name: roles/bigquerymigration.orchestrator
name: roles/bigquerymigration.translationUser
name: roles/bigquerymigration.viewer
name: roles/bigquerymigration.worker
```

And chose `roles/bigquery.dataOwner` as the one I'll give it. (Note that some of the roles come with descriptions - you can widen your query if you want to see those, for example with `grep -A3 bigq`)

Give your user the role you chose:

```
gcloud projects add-iam-policy-binding bigquery-dev-user \
  --member="serviceAccount:bigquery-dev-user@<project_id>.iam.gserviceaccount.com" \
  --role="roles/bigquery.dataOwner"
```

If you don't want to construct that member name by hand, here's an example query that might help:

```
gcloud iam service-accounts list \
  --format json \
  --filter="displayName:bigquery-dev-user" | \
  jq -r .[0].email
```

It seems to me that this should be showing an IAM policy, but isn't showing anything?

```
gcloud iam service-accounts get-iam-policy \
  $(gcloud iam service-accounts list \
    --format json \
    --filter="displayName:bigquery-dev-user" | \
      jq -r .[0].email)
```

just prints an etag, which is confusing to me. Anyway, onwards.

Generate a key for the service user

```
gcloud iam service-accounts keys create ./bigquery-dev-user.json \
  --iam-account=$( \
    gcloud iam service-accounts list \
      --format json \
      --filter="displayName:bigquery-dev-user" | \
        jq -r .[0].email)
```

This will save a key in `bigquery-dev-user.json` in google's JSON format.

For my purposes, I'll want to stick the key into an environment variable, so `jq -c . < bigquery-dev-user.json` will minimize it for me.

To test the json key, it looks like you first activate it. Before we do, let's save our user's account email in a variable to make our lives easier

```
export SVC_ACCOUNT=$(gcloud iam service-accounts list \
  --format json \
  --filter="displayName:bigquery-dev-user" | \
    jq -r .[0].email)
```

Now I can make that my active google cloud account:

```
gcloud auth activate-service-account $SVC_ACCOUNT \
  --key-file=./bigquery-dev-user.json
```

You should see a response like `Activated service account credentials for: [bigquery-dev-user@<project_id>.iam.gserviceaccount.com]`

And at last I can test as that user!

```
$ bq query 'select count(*) from publicdata:samples.shakespeare'
BigQuery error in query operation: Access Denied: Project <project_id>: User does not have bigquery.jobs.create permission in project <project_id>.
```

ok... I thought we got that with the IAM roles earlier? Logging back in as myself (with `gcloud auth login`, which pops the browser and does the oauth dance), I'm able to run this command to list the roles for each IAM user:

```
$ gcloud projects get-iam-policy <project_id>
bindings:
- members:
  - serviceAccount:bigquery-dev-user@<project_id>.iam.gserviceaccount.com
  role: roles/bigquery.dataOwner
- members:
  - user:me@me.org
  role: roles/owner
etag: BwXmigDOR6c=
version: 1
```

Alright, so I do have dataOwner permission, but that must not include query perms! That's fine, let's try by testing uploading a csv.

After logging back in as the service account user, I ran

```
# create a dataset
bq mk --dataset ds

# create a csv file
printf "a,b,c\n1,2,3" > test.csv

# try to load it
bq load --autodetect --source_format=CSV ds.deleteme ./test.csv

# BigQuery error in load operation: Access Denied: Project <project_id>: User does not have bigquery.jobs.create permission in project <project_id>.
```

OK, fine looks like we need to add more permissions than `dataOwner` to allow our user to upload data.

I log back in as myself, and add the `bigquery.user` role:

```
gcloud projects add-iam-policy-binding <project_id> \
  --member="serviceAccount:bigquery-dev-user@<project_id>.iam.gserviceaccount.com" \
  --role="roles/bigquery.user"
```

Then, once again log in as the service user, and 💥 it finally succeeds!

```
$ bq load --autodetect --source_format=CSV ds.deleteme ./test.csv
Upload complete.
Waiting on bqjob_r31a9f8532234badf_00000182b39ec3da_1 ... (1s) Current status: DONE
```

Let's clean up our test dataset

```
bq rm -r ds
```

`-r` tells bq to remove it recursively - otherwise it complains that the dataset isn't empty.

And that's... it! Nothing was complicated, but that sure was a lot of steps.