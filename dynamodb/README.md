# AWS CLI DynamoDB Commands

This file contains some common AWS CLI commands for the [DynamoDB](https://aws.amazon.com/dynamodb/) service.

For the full sns commands check the [aws cli dynamodb documentation](https://docs.aws.amazon.com/cli/latest/reference/dynamodb/).

> Note: All the examples below are referencing the localstack. To reference the services on your aws account remove `--endpoint-url` parameter.

## Create table

```bash
aws --endpoint-url=http://localhost:4566 dynamodb create-table \
--table-name table-name \
--attribute-definitions \
AttributeName=HashKey,AttributeType=S \
AttributeName=SortKey,AttributeType=S \
--key-schema \
AttributeName=HashKey,KeyType=HASH AttributeName=SortKey,KeyType=RANGE \
--provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5
```

### Batch Write Item (Adicionar múltiplos itens de uma só vez)

```bash
aws --no-verify-ssl --endpoint-url=$HOST_URL dynamodb batch-write-item \
--request-items file://steps.json
```

- ```steps.json``` example:

    ```json
    {
        "table-name": [
            {   
                "PutRequest": {
                    "Item": { 
                        "HashKey": { "S": "string" },
                        "SortKey": { "S": "string-1" },
                        "CreationDate": { "S": "2022-04-18T19:24:02.829484909" },
                    }
                }
            },
            {   
                "PutRequest": {
                    "Item": { 
                        "HashKey":{ "S": "string" },
                        "SortKey": { "S": "string-2"} ,
                        "CreationDate": { "S":"2022-04-18T19:24:02.829484909" }, 
                    }
                }
            },
        ]
    }
    ```