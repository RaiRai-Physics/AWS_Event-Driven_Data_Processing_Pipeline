# Setup Steps

Step 1: Create an Amazon S3 Bucket
Create an S3 bucket to store both the raw input data and the processed output data.

Inside the bucket, create data/raw and data/processed folder. Our sales_data.csv file will go in the data/raw folder, whereas the output parquet file will be saved in the data/processed folder.

Step 2: Create an Amazon SQS queue that will receive data processing requests

Step 3: Create an IAM Role for AWS Lambda
We make sure that the IAM role has permission to:
-read messages from SQS
-write logs to Amazon CloudWatch
-start an AWS Glue job

Step 4: Create an IAM Role for AWS Glue
The roles should have permissions to:
-read files from Amazon S3
-write processed files back to Amazon S3
-write logs to CloudWach

Step 5: Create AWS Glue Job
We use the glue IAM role we created and apply it to this Gluejob. 
The Glue Job should:
-Read the CSV file from the S3 raw folder
-perform the required data transformations
-write the transformed output into the S3 processed folder

Step 6: Create AWS Lambda function
We use the appropriate lambda role that we created in step 3 for our lambda function.
The lambda function should:
-Receive the SQS message
-extract the file name, source path, and destination path
-Trigger the AWS Glue job

We also set the following environment variables in Lambda:
-GLUE_JOB_NAME
-BUCKET_NAME

We then deploy the code.

Step 7: Configure SQS as a Trigger for Lambda
Add the SQS queue as a trigger for the lambda function. 

Step 8: Upload the Dataset to S3
We upload the csv file sales_data.csv to the data/raw folder of our S3 bucket.

Step 9: Send a message to SQS
We send the following JSON message to the SQS queue:

{
  "file_name": "sales_data.csv",
  "source_path": "sales-data/raw/",
  "destination_path": "sales-data/processed/"
}

This message tells the pipeline which file to process and where to store the output.

Step 10: Verify the Pipeline
After sending the message:
-Check that lambda is triggered
-Check that Glue job starts successfully
-Check that the processed output is created in the S3 processed folder
