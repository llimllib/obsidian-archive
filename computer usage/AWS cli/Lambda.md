To run a lambda job: 

```
aws lambda invoke \
  --function-name <function_name> \
  --cli-binary-format raw-in-base64-out \
  --payload '{"json": "payload"}' \
  /tmp/lambda_output.log
```