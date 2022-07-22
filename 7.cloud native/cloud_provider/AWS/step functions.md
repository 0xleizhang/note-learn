

```
aws stepfunctions --endpoint http://localhost:8083 create-state-machine --definition "$(cat local.asl.json)" --name "HelloWorld" --role-arn "arn:aws:iam::012345678901:role/DummyRole"
```