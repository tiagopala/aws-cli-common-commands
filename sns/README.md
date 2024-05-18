# AWS CLI SNS Commands

This file contains some common AWS CLI commands for the [SNS](https://aws.amazon.com/sns/) service.

For the full sns commands check the [aws cli sns documentation](https://docs.aws.amazon.com/cli/latest/reference/sns/).

> Note: All the examples below are referencing the localstack. To reference the services on your aws account remove `--endpoint-url` parameter.

## Commands

### Create Topic

```bash
aws --endpoint-url=http://localhost:4566 sns create-topic \
--name topic-name
```

### Create subscription SNS <> SQS

```bash
aws --endpoint-url=http://localhost:4566 sns subscribe \
--topic-arn arn:aws:sns:sa-east-1:000000000000:topic-name \
--protocol sqs \
--notification-endpoint arn:aws:sqs:sa-east-1:000000000000:queue-name \
--output text
```

> We could also store the `subscription_arn` in a variable to reuse at a later stage, as we could see at [set subscription-attributes](#set-subscription-attributes).

```bash
subscription_arn=$(
aws --endpoint-url=http://localhost:4566 sns subscribe \
--topic-arn arn:aws:sns:sa-east-1:000000000000:topic-name \
--protocol sqs \
--notification-endpoint arn:aws:sqs:sa-east-1:000000000000:queue-name \
--output text)
```

### Set subscription-attributes

```bash
aws --endpoint-url=http://localhost:4566 sns set-subscription-attributes \
--subscription-arn "$subscription_arn" \
--attribute-name RawMessageDelivery \
--attribute-value true
```

### Adding a FilterPolicy:

```bash
aws --no-verify-ssl --endpoint-url=$HOST_URL sns set-subscription-attributes \
--subscription-arn "$subscription_arn" \
--attribute-name FilterPolicy \
--attribute-value '{"source": ["source-microservice"]}'
```

### List Topics

```bash
aws --no-verify-ssl --endpoint-url=$HOST_URL sns list-topics
```

### List Subscriptions

```bash
aws --no-verify-ssl --endpoint-url=$HOST_URL sns list-subscriptions
```