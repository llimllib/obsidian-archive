list them

```
aws iam list-open-id-connect-providers
```

delete the first one in the list

```
aws iam delete-open-id-connect-provider --open-id-connect-provider-arn \
  $(aws iam list-open-id-connect-providers | \
    jq -r .OpenIDConnectProviderList[0].Arn)
```

