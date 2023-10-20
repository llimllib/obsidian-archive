List the secrets in a project

```
aws secretsmanager list-secrets
```

Search for any secrets matching a particular string (`"test"`)

```
aws secretsmanager list-secrets --filter Key=all,Values="test"
```

