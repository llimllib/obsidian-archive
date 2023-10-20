list parameters

```
aws ssm describe-parameters
```

delete all parameters (as long as there's fewer than one page  and you don't need shell quoting (how do you tell bash that the quotes in a shell substitution are real quotes - eval or something?))

```
ws ssm delete-parameters --names $(aws ssm describe-parameters | jq -r '.Parameters|map(.Name)|join(" ")'
```