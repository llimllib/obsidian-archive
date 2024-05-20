---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
List the secrets in a project

```
aws secretsmanager list-secrets
```

Search for any secrets matching a particular string (`"test"`)

```
aws secretsmanager list-secrets --filter Key=all,Values="test"
```

