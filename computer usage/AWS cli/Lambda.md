---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
To run a lambda job: 

```
aws lambda invoke \
  --function-name <function_name> \
  --cli-binary-format raw-in-base64-out \
  --payload '{"json": "payload"}' \
  /tmp/lambda_output.log
```