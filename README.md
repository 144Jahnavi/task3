# task3
Here’s a concise **README.md**:

---

# AWS Lambda Deployment Guide

This guide explains how to deploy two AWS Lambda functions:

1. **Add Two Numbers**: Adds two numbers and returns the result.
2. **Store File in S3**: Uploads a document/PDF file to an S3 bucket.

---

## Deployment Steps

### Prerequisites
- **AWS CLI** installed and configured.
- An S3 bucket for file storage.
- IAM role with:
  - `AWSLambdaBasicExecutionRole`
  - `AmazonS3FullAccess`

### Steps

1. **Create the S3 Bucket**:
   - Use the AWS Console or CLI to create an S3 bucket.
   
2. **Zip and Deploy the Functions**:
   - Save the code for each function in a `.py` file.
   - Zip the files:
     ```bash
     zip add_two_numbers.zip add_two_numbers.py
     zip store_file_s3.zip store_file_s3.py
     ```
   - Deploy using AWS CLI:
     ```bash
     aws lambda create-function \
         --function-name AddTwoNumbers \
         --runtime python3.x \
         --role <role-arn> \
         --handler add_two_numbers.lambda_handler \
         --zip-file fileb://add_two_numbers.zip
     
     aws lambda create-function \
         --function-name StoreFileS3 \
         --runtime python3.x \
         --role <role-arn> \
         --handler store_file_s3.lambda_handler \
         --zip-file fileb://store_file_s3.zip \
         --environment Variables="{BUCKET_NAME=<your-bucket-name>}"
     ```

3. **Test the Functions**:
   - Test via the AWS Console or CLI with appropriate input events.

---

.
