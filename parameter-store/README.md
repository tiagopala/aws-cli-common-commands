# AWS CLI Parameter Store Commands

This file contains some common AWS CLI commands for the [Systems Manager - Parameter Store](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html)

For the full sns commands check the [aws cli ssm documentation](https://docs.aws.amazon.com/cli/latest/reference/ssm/).

> Note: All the examples below are referencing the localstack. To reference the services on your aws account remove `--endpoint-url` parameter.

## Put parameter

```bash
aws --no-verify-ssl --endpoint-url=$HOST_URL ssm put-parameter \
--overwrite \
--name "/domain/microservice/feature-flag" \
--value "true" \
--type String 
```

## Describe parameters

```bash
aws --endpoint-url=http://localhost:4566 ssm describe-parameters
```