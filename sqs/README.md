# AWS CLI SQS Commands

This file contains some common AWS CLI commands for the [SQS](https://aws.amazon.com/sqs/) service.

For the full sns commands check the [aws cli sqs documentation](https://docs.aws.amazon.com/cli/latest/reference/sqs/).

> Note: All the examples below are referencing the localstack. To reference the services on your aws account remove `--endpoint-url` parameter.

## Manipulating Queues

### Create Queue

```bash
aws --endpoint-url=http://localhost:4566 sqs create-queue \
--queue-name queue-name
```

### Create Queue + Dead Letter Queue (DLQ)

> Note: The SQS DLQ must be created beforehand, especially when using LocalStack.

```bash
aws --endpoint-url=http://localhost:4566 sqs create-queue \
--queue-name queue-name \
--attributes "
{
    \"RedrivePolicy\":\"{\\\"deadLetterTargetArn\\\":\\\"arn:aws:sqs:sa-east-1:000000000000:queue-name-dlq\\\",\\\"maxReceiveCount\\\":\\\"5\\\" }\"
}"
```

### List Queues

```bash
aws --endpoint-url=http://localhost:4566 sqs list-queues
```

### Delete Queue

```bash
aws --endpoint-url=http://localhost:4566 sqs delete-queue \
--queue-url http://localhost:4566/000000000000/queue-name
```

### Purge queue

```bash
aws --endpoint-url=http://localhost:4566 sqs purge-queue \
--queue-url http://localhost:4566/000000000000/queue-name
```

## Manipulating Messages

### Receive a message

```bash
aws --endpoint-url=http://localhost:4566 sqs receive-message \
--queue-url http://localhost:4566/000000000000/queue-name
```

## Send message

```bash
aws --endpoint-url=http://localhost:4566 sqs send-message \
--queue-url http://localhost:4566/000000000000/queue-name \
--message-body file://event.json \
--message-attributes file://message-attributes.json
```

1. `event.json` example:

    ```json
    {
        "customer": {
            "name": "Tiago Pala",
            "documentNumber": "string",
        }
    }
    ```

2. `message-attributes.json` example:

    ```json
    {
        "propertyName": {
            "dataType": "String",
            "stringValue": "propertyValue"
        }
    }
    ```