Prerequisites
AWS account with access to the following services:
AWS Lambda
Amazon S3
Amazon DynamoDB
Amazon SNS
AWS CLI installed (optional for deployment automation)
Python 3.x (used for Lambda functions)
Setup Instructions
1. Create S3 Bucket
Log in to the AWS Console.
Navigate to S3 and create a new bucket.
Name the bucket (e.g., inventory-<random-number>).
Note the bucket name, as it will be used in the Lambda function setup.
2. Upload Lambda Functions
Go to AWS Lambda and create a function.
For the Load-Inventory function:
Name: Load-Inventory
Runtime: Python 3.9
Role: Attach a role with S3 and DynamoDB access
Copy the content from load_inventory.py to the Lambda function editor and deploy.
Repeat the steps for the Check-Stock function using the code in check_stock.py.
3. Configure S3 Event Trigger for Lambda
Go to your S3 bucket, and under Properties, create an event notification.
Set it to trigger on All object create events, and link it to the Load-Inventory Lambda function.
4. Set up DynamoDB Table
Navigate to DynamoDB and create a table.
Name the table Inventory and set Store as the partition key and Item as the sort key.
5. Create SNS Topic and Subscribe
Go to Amazon SNS and create a topic named NoStock.
Subscribe to the topic using your email address. Confirm the subscription via the email you receive.
6. DynamoDB Stream Trigger for Stock Check
In DynamoDB, enable Streams for the Inventory table.
Add a new trigger in the Check-Stock Lambda function to listen for DynamoDB changes.
Testing the System
Upload one of the sample inventory files (found in /sample_data) to the S3 bucket.
The Load-Inventory Lambda function will be triggered, loading data into DynamoDB.
If any items are out of stock, the Check-Stock Lambda function will send an email notification via SNS.

