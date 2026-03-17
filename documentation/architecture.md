# Architecture Explanation

## Overview
This project uses an event-driven architecture to process data automatically when a request is received. The pipeline is built using Amazon SQS, AWS Lambda, AWS Glue, and Amazon S3.

## Architecture Flow
Data Request -> Amazon SQS -> AWS Lambda -> AWS Glue -> Amazon S3 Processed Output

## Components

### 1. Amazon S3
Amazon S3 is used as the storage layer in this project. The raw input dataset is stored in the `sales-data/raw/` folder, and the transformed output is written to the `sales-data/processed/` folder.

### 2. Amazon SQS
Amazon SQS acts as the messaging layer. A message is sent to the queue whenever a file needs to be processed. The message contains the file name and the S3 source and destination paths.

For our pipeline we used the message below in JSON format to trigger the pipeline flow:

{
  "file_name": "sales_data.csv",
  "source_path": "sales-data/raw/",
  "destination_path": "sales-data/processed/"
}
