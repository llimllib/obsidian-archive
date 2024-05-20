---
updated: '2024-03-07T17:45:11Z'
created: '2024-03-07T17:45:11Z'
---
```bash
#!/usr/bin/env bash
# To use this script, run:
#
# $ eval $(bin/assume-role.sh)
#
# assume the required role and read the new credentials into an array
set -euo pipefail

# the ARN of the role you want to access
ROLE=arn:aws:iam::123456123456:role/SomeAccessRole
# the name to give it the assumed role session
NAME=some-access-role

# attempt to assume the role given by the ARN above, and read the short-lived
# credentials into an array named "creds" with three elements:
# [access key, secret key, session token]
if ! read -ra creds <<< "$(aws sts assume-role \
    --role-arn $ROLE \
    --role-session-name $NAME \
    --query "Credentials.[AccessKeyId,SecretAccessKey,SessionToken]" \
    --output text)"; then
    # we might be running with a role's no-longer-valid AWS environment
    # variables, so unset them and attempt to try again. If the user has auth
    # configured in their home dir, the next call will use those creds
    unset AWS_ACCESS_KEY_ID
    unset AWS_SECRET_ACCESS_KEY
    unset AWS_SESSION_TOKEN
    read -ra creds <<< "$(aws sts assume-role \
        --role-arn $ROLE \
        --role-session-name $NAME \
        --query "Credentials.[AccessKeyId,SecretAccessKey,SessionToken]" \
        --output text)"
fi

# print an export statement for each variable, so the user can eval them
printf 'export AWS_ACCESS_KEY_ID="%s"\n' "${creds[0]}"
printf 'export AWS_SECRET_ACCESS_KEY="%s"\n' "${creds[1]}"
printf 'export AWS_SESSION_TOKEN="%s"\n' "${creds[2]}"
```

script derived from [this stackoverflow answer](https://stackoverflow.com/a/67636523)

I don't really _like_ this method of getting creds with `assume-role`, but it works for now. If you have a better way, definitely let me know.