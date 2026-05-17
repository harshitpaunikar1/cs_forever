# Serverless Computing

Serverless lets you run code without provisioning or managing servers. You deploy
functions, configure triggers, and the platform handles everything else — scaling,
patching, availability, and infrastructure. You pay only for the compute you consume.

---

## What "Serverless" Means

**There are still servers** — you just don't manage them. The cloud provider:
- Provisions compute on demand
- Scales from zero to millions of requests automatically
- Charges per invocation and compute time (no idle cost)
- Handles OS patching and runtime upgrades

**FaaS (Function as a Service)**: your code runs in response to an event. Single function,
stateless, short-lived. Examples: AWS Lambda, Google Cloud Functions, Azure Functions.

**BaaS (Backend as a Service)**: fully managed backends for common needs.
Examples: Firebase (database, auth), Auth0, Algolia (search).

**Serverless containers**: run containers without managing cluster nodes.
Examples: AWS Fargate, Google Cloud Run, Azure Container Instances.

---

## When to Use Serverless

**Good fit**:
- Event-driven workloads: file upload triggers processing, webhook handlers
- Scheduled jobs: cron-like tasks (nightly reports, data cleanup)
- API backends with variable or unpredictable traffic
- Glue code between services (data transformation, fan-out)
- Workloads with zero baseline traffic (scale-to-zero eliminates idle cost)

**Poor fit**:
- Long-running processes (Lambda max 15 minutes)
- Latency-sensitive workloads that can't tolerate cold starts
- Applications with persistent in-process state
- Very high, steady-state traffic (containers often cheaper)
- Workloads needing GPU compute

---

## Cold Starts

A **cold start** happens when your function hasn't been invoked recently and the
platform must:
1. Provision a compute environment
2. Download and load your code
3. Initialize the runtime
4. Run your initialization code

This adds latency — typically 100ms to several seconds depending on runtime and code size.

| Runtime | Typical Cold Start |
|---------|-------------------|
| Python/Node.js | 100-500ms |
| Java/JVM | 1-5 seconds |
| Go (static binary) | 100-200ms |
| Container image | 2-10 seconds |

**Mitigation strategies**:

```python
# Keep initialization outside the handler (runs once per warm instance)
import boto3
import json

# These run during cold start, not on every invocation
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('orders')

def handler(event, context):
    # This runs on every invocation — keep it fast
    order_id = event['pathParameters']['orderId']
    response = table.get_item(Key={'id': order_id})
    return {
        'statusCode': 200,
        'body': json.dumps(response['Item'])
    }
```

- **Provisioned concurrency** (AWS Lambda): keeps instances pre-warmed; eliminates cold starts at extra cost
- **Minimize package size**: smaller = faster load
- **Use compiled languages** (Go, Rust) for lowest cold start times
- **Keep-warm hacks**: scheduled ping every 5 minutes (avoid — better to use provisioned concurrency)

---

## AWS Lambda

### Execution Model

| Invocation Type | Description | Example trigger |
|-----------------|-------------|----------------|
| **Synchronous** | Caller waits for response | API Gateway, ALB, SDK |
| **Asynchronous** | Lambda queues the event; retries on failure | S3, SNS, EventBridge |
| **Event source mapping** | Lambda polls the source | SQS, Kinesis, DynamoDB Streams |

### Function Anatomy

```python
# Python handler
import json
import os
import logging

logger = logging.getLogger()
logger.setLevel(logging.INFO)

def handler(event, context):
    """
    event: dict — the triggering event payload
    context: LambdaContext — runtime info (function_name, remaining_time_in_millis, etc.)
    """
    logger.info("Event: %s", json.dumps(event))

    # For API Gateway events
    http_method = event.get('httpMethod', '')
    path = event.get('path', '')
    body = json.loads(event.get('body', '{}') or '{}')

    # Business logic
    result = process(body)

    return {
        'statusCode': 200,
        'headers': {
            'Content-Type': 'application/json',
            'Access-Control-Allow-Origin': '*',
        },
        'body': json.dumps(result)
    }
```

```javascript
// Node.js handler
const { DynamoDBClient, GetItemCommand } = require("@aws-sdk/client-dynamodb");

// Initialized once per warm instance
const client = new DynamoDBClient({ region: "us-east-1" });

exports.handler = async (event, context) => {
    const { id } = event.pathParameters;

    const response = await client.send(new GetItemCommand({
        TableName: process.env.TABLE_NAME,
        Key: { id: { S: id } }
    }));

    if (!response.Item) {
        return { statusCode: 404, body: JSON.stringify({ error: "Not found" }) };
    }

    return {
        statusCode: 200,
        body: JSON.stringify(response.Item),
    };
};
```

### Configuration

```yaml
# Key settings
Runtime: python3.12 / nodejs20.x / go1.x / java21
Memory: 128MB to 10240MB   # CPU scales proportionally with memory
Timeout: 3s to 900s (15 min)
Environment Variables:
  TABLE_NAME: orders-prod
  LOG_LEVEL: INFO

# Concurrency
ReservedConcurrency: 100   # Hard limit for this function
ProvisionedConcurrency: 10 # Pre-warmed instances (eliminates cold starts)

# Packaging
DeploymentPackage: ZIP (up to 50MB) or container image (up to 10GB)
```

### Event Sources (Triggers)

```yaml
# API Gateway HTTP API (simplest, lowest latency)
Events:
  ApiEvent:
    Type: HttpApi
    Properties:
      Path: /orders/{id}
      Method: GET
      ApiId: !Ref MyApi

# S3 trigger
  S3Event:
    Type: S3
    Properties:
      Bucket: !Ref UploadsBucket
      Events: s3:ObjectCreated:*
      Filter:
        S3Key:
          Rules:
            - Name: suffix
              Value: .jpg

# SQS queue (Lambda polls)
  SQSEvent:
    Type: SQS
    Properties:
      Queue: !GetAtt OrdersQueue.Arn
      BatchSize: 10
      FunctionResponseTypes:
        - ReportBatchItemFailures   # Partial batch failure handling

# EventBridge scheduled rule (cron)
  ScheduledEvent:
    Type: Schedule
    Properties:
      Schedule: cron(0 2 * * ? *)   # Daily at 2 AM UTC
```

### Layers

Lambda Layers share code and dependencies across functions:

```bash
# Create a layer
mkdir -p python/lib/python3.12/site-packages
pip install requests -t python/lib/python3.12/site-packages/
zip -r dependencies.zip python/

aws lambda publish-layer-version \
  --layer-name my-dependencies \
  --zip-file fileb://dependencies.zip \
  --compatible-runtimes python3.12
```

---

## AWS SAM (Serverless Application Model)

SAM extends CloudFormation with Lambda-specific resource types.

```yaml
# template.yaml
AWSTemplateFormatVersion: "2010-09-09"
Transform: AWS::Serverless-2016-10-31

Globals:
  Function:
    Runtime: python3.12
    Timeout: 30
    MemorySize: 256
    Environment:
      Variables:
        POWERTOOLS_SERVICE_NAME: orders-api
        LOG_LEVEL: INFO
    Layers:
      - !Ref PowertoolsLayer

Parameters:
  Environment:
    Type: String
    AllowedValues: [dev, staging, prod]

Resources:
  OrdersApi:
    Type: AWS::Serverless::Api
    Properties:
      StageName: !Ref Environment
      Auth:
        DefaultAuthorizer: CognitoAuthorizer
        Authorizers:
          CognitoAuthorizer:
            UserPoolArn: !GetAtt UserPool.Arn

  GetOrderFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: src/get_order/
      Handler: app.handler
      Policies:
        - DynamoDBReadPolicy:
            TableName: !Ref OrdersTable
      Events:
        GetOrder:
          Type: Api
          Properties:
            RestApiId: !Ref OrdersApi
            Path: /orders/{id}
            Method: GET

  OrdersTable:
    Type: AWS::Serverless::SimpleTable
    Properties:
      PrimaryKey:
        Name: id
        Type: String

  PowertoolsLayer:
    Type: AWS::Serverless::LayerVersion
    Properties:
      LayerName: aws-lambda-powertools
      ContentUri: layers/powertools/
      CompatibleRuntimes:
        - python3.12

Outputs:
  ApiUrl:
    Value: !Sub "https://${OrdersApi}.execute-api.${AWS::Region}.amazonaws.com/${Environment}"
```

```bash
# SAM CLI
sam build                          # Build Lambda packages
sam local invoke GetOrderFunction  # Test locally
sam local start-api                # Local API Gateway emulator
sam deploy --guided                # Interactive first deploy
sam deploy                         # Subsequent deploys
sam logs -n GetOrderFunction --tail
```

---

## Serverless Framework

```yaml
# serverless.yml
service: orders-api
frameworkVersion: "3"

provider:
  name: aws
  runtime: nodejs20.x
  region: us-east-1
  stage: ${opt:stage, 'dev'}
  environment:
    TABLE_NAME: orders-${self:provider.stage}
  iam:
    role:
      statements:
        - Effect: Allow
          Action: [dynamodb:GetItem, dynamodb:PutItem, dynamodb:UpdateItem]
          Resource: !GetAtt OrdersTable.Arn

functions:
  getOrder:
    handler: src/orders/get.handler
    events:
      - httpApi:
          path: /orders/{id}
          method: GET
    memorySize: 256
    timeout: 10

  processOrder:
    handler: src/orders/process.handler
    events:
      - sqs:
          arn: !GetAtt OrdersQueue.Arn
          batchSize: 10

resources:
  Resources:
    OrdersTable:
      Type: AWS::DynamoDB::Table
      Properties:
        TableName: orders-${self:provider.stage}
        BillingMode: PAY_PER_REQUEST
        AttributeDefinitions:
          - AttributeName: id
            AttributeType: S
        KeySchema:
          - AttributeName: id
            KeyType: HASH
```

```bash
serverless deploy --stage prod
serverless invoke --function getOrder --stage prod
serverless logs --function getOrder --tail
serverless remove --stage dev    # Tear down environment
```

---

## Google Cloud Run

Cloud Run runs containers without managing infrastructure. Unlike Lambda, there's
no 15-minute limit and it supports any language or binary.

```bash
# Deploy from Docker image
gcloud run deploy myapp \
  --image gcr.io/myproject/myapp:1.0 \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated \
  --memory 512Mi \
  --min-instances 0 \
  --max-instances 100 \
  --concurrency 80               # Requests per instance

# Deploy from source (automatically builds container)
gcloud run deploy myapp --source .
```

**Cloud Run vs Lambda**:
- Cloud Run: container-based, no timeout limit (default 60min), per-request concurrency model
- Lambda: function-based, 15min max, one request per instance at a time

---

## Step Functions (Workflow Orchestration)

```json
{
  "Comment": "Order processing workflow",
  "StartAt": "ValidateOrder",
  "States": {
    "ValidateOrder": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123:function:validate-order",
      "Next": "ProcessPayment",
      "Catch": [{
        "ErrorEquals": ["ValidationError"],
        "Next": "OrderFailed"
      }]
    },
    "ProcessPayment": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123:function:process-payment",
      "Retry": [{
        "ErrorEquals": ["PaymentRetryableError"],
        "IntervalSeconds": 2,
        "MaxAttempts": 3,
        "BackoffRate": 2
      }],
      "Next": "NotifyCustomer"
    },
    "NotifyCustomer": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123:function:notify",
      "End": true
    },
    "OrderFailed": {
      "Type": "Fail",
      "Error": "OrderFailed",
      "Cause": "Order validation failed"
    }
  }
}
```

---

## Event-Driven Patterns

**Fan-out** (SNS → multiple SQS queues → multiple Lambdas):

```
Order Created Event
        │
   SNS Topic
   ┌────┴────┐
   SQS       SQS
   │         │
Lambda    Lambda
(fulfill) (notify)
```

**Queue-based load leveling** (SQS → Lambda):
- Smooths traffic spikes
- Lambda scales with queue depth
- Dead-letter queue for failed messages

```python
# SQS batch processing with partial failure support
def handler(event, context):
    failures = []
    for record in event['Records']:
        try:
            process(json.loads(record['body']))
        except Exception as e:
            logger.error("Failed to process %s: %s", record['messageId'], e)
            failures.append({'itemIdentifier': record['messageId']})

    return {'batchItemFailures': failures}
```

---

## Observability

```python
# AWS Lambda Powertools
from aws_lambda_powertools import Logger, Tracer, Metrics
from aws_lambda_powertools.metrics import MetricUnit

logger = Logger()
tracer = Tracer()
metrics = Metrics(namespace="OrdersAPI")

@logger.inject_lambda_context(log_event=True)
@tracer.capture_lambda_handler
@metrics.log_metrics
def handler(event, context):
    metrics.add_metric(name="OrdersProcessed", unit=MetricUnit.Count, value=1)

    with tracer.capture_method:
        result = process_order(event)

    logger.info("Order processed", extra={"order_id": result["id"]})
    return result
```

---

## Lambda Limits Reference

| Limit | Value |
|-------|-------|
| Max timeout | 15 minutes |
| Max memory | 10,240 MB |
| Max deployment package (ZIP) | 50 MB (250 MB unzipped) |
| Max container image size | 10 GB |
| /tmp storage | 512 MB (up to 10 GB with ephemeral storage config) |
| Max concurrent executions (default) | 1,000 per region (soft limit) |
| Max environment variable size | 4 KB total |
| Max layers | 5 per function |
| Synchronous payload (request/response) | 6 MB |
| Asynchronous payload | 256 KB |
