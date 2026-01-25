# AWS Lambda

## Links
- [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
- [AWS Lambda Pricing](https://aws.amazon.com/lambda/pricing/)
- [AWS Lambda With Python](https://docs.aws.amazon.com/lambda/latest/dg/lambda-python.html)
- [Powertools for AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/powertools-for-lambda.html)
  - [Powertools for Lambda - Python](https://docs.aws.amazon.com/powertools/python/latest/)
    - [Powertools for Lambda - Python full feature set](https://docs.aws.amazon.com/powertools/python/latest/#features)
  - [Powertools for Lambda - Java](https://docs.aws.amazon.com/powertools/java/latest/)
  - [Powertools for Lambda - TypeScript](https://docs.aws.amazon.com/powertools/typescript/latest/)

## Overview
AWS Lambda is a compute service that runs code without the need to manage servers. Your code runs, scaling up and down automatically, with pay-per-use pricing. You can use AWS Lambda to run code in response to events, such as changes to data in an Amazon S3 bucket or an update to a DynamoDB table. You can also invoke Lambda functions directly using the `AWS SDKs` or `HTTP endpoints`.
- File processing: Process files automatically when uploaded to Amazon Simple Storage Service. See file processing examples for details.
- Long-running workflows: Use durable Lambda functions to build stateful, multi-step workflows that can run for up to one year. Perfect for order processing, approval workflows, human-in-the-loop processes, and complex data pipelines that need to remember their progress.
- Database operations and integration examples: Respond to database changes and automate data workflows. See database examples for details.
- Scheduled and periodic tasks: Run automated operations on a regular schedule using EventBridge. See scheduled task examples for details.
- Stream processing: Process real-time data streams for analytics and monitoring. See Kinesis Data Streams for details.
- Web applications: Build scalable web apps that automatically adjust to demand.
- Mobile backends: Create secure API backends for mobile and web applications.
- IoT backends: Handle web, mobile, IoT, and third-party API requests. See IoT for details.

## AWS SAM
- [AWS Serverless Application Model (SAM) Documentation](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html)
- [AWS SAM GitHub Repository](https://github.com/aws/serverless-application-model)
- [AWS Serverless Function](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-resource-function.html)
- [AWS SAM Template Anatomy](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-specification-template-anatomy.html)
- [AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam-cli.html)

## AWS Infrastructure Composer
- [AWS Infrastructure Composer Documentation](https://docs.aws.amazon.com/infrastructure-composer/latest/userguide/what-is-infrastructure-composer.html)
- [Using Lambda with Infrastructure Composer](https://docs.aws.amazon.com/lambda/latest/dg/services-appcomposer.html)

## Lambda Configurations
- [AWS Lambda in AWS SAM](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-resource-function.html)
- [AWS Lambda in Infrastructure Composer](https://docs.aws.amazon.com/infrastructure-composer/latest/userguide/aws-lambda.html)
- [AWS Lambda in AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html)
- [AWS Lambda Permissions](https://docs.aws.amazon.com/lambda/latest/dg/lambda-permissions.html)


## Durable Functions
- [Durable Functions for AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/durable-functions.html)
- [Durable Functions SDK for Python](https://docs.aws.amazon.com/lambda/latest/dg/durable-functions-python-sdk.html)
- [Durable Functions SDK for Java](https://docs.aws.amazon.com/lambda/latest/dg/durable-functions-java-sdk.html)
- [Durable Functions SDK for TypeScript](https://docs.aws.amazon.com/lambda/latest/dg/durable-functions-typescript-sdk.html)

 ## Lambda Managed Instances
- [AWS Lambda Managed Instances](https://docs.aws.amazon.com/lambda/latest/dg/lambda-managed-instances.html)  

## Lambda Runtimes
- [AWS Lambda Runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html)
- [AWS Lambda Runtime API](https://docs.aws.amazon.com/lambda/latest/dg/runtime-api.html)
- [AWS Lambda Custom Runtimes](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-custom.html)
- [AWS Lambda Runtime Interface Clients](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-interfaces.html)
  - [AWS Lambda Runtime Interface Client for Python](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-interfaces-python.html)
  - [AWS Lambda Runtime Interface Client for Java](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-interfaces-java.html)
  - [AWS Lambda Runtime Interface Client for Node.js](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-interfaces-node.html)

## Configuring Functions
- [Configuring Lambda Functions](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html)
- [AWS Lambda Environment Variables](https://docs.aws.amazon.com/lambda/latest/dg/configuration-envvars.html)
- [AWS Lambda Deployment Packages](https://docs.aws.amazon.com/lambda/latest/dg/lambda-deployment-packages.html)
- [AWS Lambda Layers](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html)
- [AWS Lambda Extensions](https://docs.aws.amazon.com/lambda/latest/dg/configuration-extensions.html)
- [AWS Lambda Function URLs](https://docs.aws.amazon.com/lambda/latest/dg/lambda-function-urls.html)

## Invoking Functions
- [Invoking AWS Lambda Functions](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html)
- [AWS Lambda Event Sources](https://docs.aws.amazon.com/lambda/latest/dg/lambda-invocation-eventsourcemapping.html)
- [AWS Lambda Synchronous Invocations](https://docs.aws.amazon.com/lambda/latest/dg/lambda-invocation-sync.html)
- [AWS Lambda Asynchronous Invocations](https://docs.aws.amazon.com/lambda/latest/dg/lambda-invocation-async.html)
- [AWS Lambda Destinations](https://docs.aws.amazon.com/lambda/latest/dg/invocation-destinations.html)

## Function Scaling and Concurrency
- [AWS Lambda Function Scaling](https://docs.aws.amazon.com/lambda/latest/dg/invocation-scaling.html)
- [AWS Lambda Reserved Concurrency](https://docs.aws.amazon.com/lambda/latest/dg/configuration-concurrency.html)
- [AWS Lambda Provisioned Concurrency](https://docs.aws.amazon.com/lambda/latest/dg/configuration-concurrency-provisioned.html)
- [AWS Lambda Throttling](https://docs.aws.amazon.com/lambda/latest/dg/invocation-throttling.html)

## Best Practices and Troubleshooting and Testing
- [AWS Lambda Best Practices](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html)
- [AWS Lambda Monitoring and Troubleshooting](https://docs.aws.amazon.com/lambda/latest/dg/monitoring-functions.html)
- [AWS Lambda Error Handling and Retries](https://docs.aws.amazon.com/lambda/latest/dg/invocation-error-handling.html)
- [AWS Lambda Testing and Debugging](https://docs.aws.amazon.com/lambda/latest/dg/testing-functions.html)
- [AWS Lambda Security Best Practices](https://docs.aws.amazon.com/lambda/latest/dg/best-practices-security.html)
- [AWS Lambda Performance Tuning](https://docs.aws.amazon.com/lambda/latest/dg/best-practices-performance.html)
- [AWS Lambda Cost Optimization](https://docs.aws.amazon.com/lambda/latest/dg/best-practices-cost.html)

## Lambda Language-Specific Resources
- [AWS Lambda with Python](https://docs.aws.amazon.com/lambda/latest/dg/lambda-python.html)
- [AWS Lambda with TypeScript](https://docs.aws.amazon.com/lambda/latest/dg/lambda-typescript.html)
- [AWS Lambda with Node.js](https://docs.aws.amazon.com/lambda/latest/dg/lambda-nodejs.html)
- [AWS Lambda with Java](https://docs.aws.amazon.com/lambda/latest/dg/lambda-java.html)
- [AWS Lambda with .NET](https://docs.aws.amazon.com/lambda/latest/dg/lambda-dotnet.html)
- [AWS Lambda with Go](https://docs.aws.amazon.com/lambda/latest/dg/lambda-go.html)
- [AWS Lambda with Ruby](https://docs.aws.amazon.com/lambda/latest/dg/lambda-ruby.html)
- [AWS Lambda with PowerShell](https://docs.aws.amazon.com/lambda/latest/dg/lambda-powershell.html)

## Lambda API Reference
- [AWS Lambda API Reference](https://docs.aws.amazon.com/lambda/latest/dg/API_Reference.html)
- [AWS Lambda SDKs and Tools](https://docs.aws.amazon.com/lambda/latest/dg/lambda-sdks.html)
- [AWS SDK for Python (Boto3) - Lambda](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/lambda.html)
- [AWS SDK for JavaScript (v3) - Lambda](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/clients/client-lambda/index.html)
- [AWS SDK for Java - Lambda](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/lambda-examples.html)
- [AWS SDK for Go - Lambda](https://docs.aws.amazon.com/sdk-for-go/api/service/lambda/)
- [AWS SDK for Ruby - Lambda](https://docs.aws.amazon.com/sdk-for-ruby/v3/api/Aws/Lambda.html)
- [AWS SDK for Rust - Lambda](https://docs.rs/aws-sdk-lambda/latest/aws_sdk_lambda/)
- [AWS CLI - Lambda](https://docs.aws.amazon.com/cli/latest/reference/lambda/index.html)

## Lambda Examples and Tutorials
- [AWS Lambda Examples](https://docs.aws.amazon.com/lambda/latest/dg/lambda-examples.html)
- [AWS Lambda Tutorials](https://docs.aws.amazon.com/lambda/latest/dg/lambda-tutorials.html)
- [Create a Lambda Function](https://docs.aws.amazon.com/lambda/latest/dg/getting-started-create-function.html)