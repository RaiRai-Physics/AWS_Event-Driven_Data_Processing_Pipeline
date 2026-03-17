# AWS_Event-Driven_Data_Processing_Pipeline
Event-driven AWS data pipeline using SQS, Lambda, Glue, and S3 for automated file processing

## Project Overview
This project demonstrates an event-driven data processing pipeline built using Amazon SQS, AWS Lambda, AWS Glue, and Amazon S3. 
The pipeline is designed to process a dataset stored in Amazon S3 whenever a request message is sent to an SQS queue. 
The transformed output is then stored in a separate processed folder in S3.

## Objective
To design and implement an event-driven pipeline where:
- A message is sent to an Amazon SQS queue
- AWS Lambda is triggered automatically
- Lambda starts an AWS Glue job
- AWS Glue reads the dataset from Amazon S3
- The data is transformed and stored in a processed S3 location

## Services Used
- Amazon SQS
- AWS Lambda
- AWS Glue
- Amazon S3
- Amazon CloudWatch

## Architecture
Data Request -> SQS Queue -> Lambda Trigger -> Glue Job -> Processed Data in S3

## Project Structure
aws-event-driven-pipeline/

|-- README.md
|-- architecture-diagram.png
'-- documentation/
    |-- architecture.md
    |-- setup_steps.md
    '-- testing.md 
