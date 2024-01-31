﻿# ENABLING-VPC-FLOW-LOGS-WITH-AUTOMATION


- `lambda_function.py` creates VPC Flow Logs for the VPC ID in the event
- `event-pattern.json` is the CloudWatch Rule event pattern for monitoring the `CreateVpc` API call.
- `test-event.json` is a sample CloudTrail event that can be used with the Lambda function, as it contains the VPC ID



In this scenario, in my organization. i was expected  to automate the creation of VPC Flow Logs whenever we create a new VPC, I was expected to accomplish this with a CloudWatch rule and a Lambda function.


I created a new trail on aws cloudtrail service,created an s3 bucket to store trail logs ,then created 2 log groups on cloudwatch,one for cloudtrail logs and the second for vpc flow logs.

On my newly created trail, I  enabled the cloudwatch logs option to monitor my cloudtrail logs and notify me when specific activity occurs.Then created a new role in order to send CloudTrail events to this CloudWatch Logs log group.

On Cloudwatch i created a new rule type (rule with an event pattern),event source (AWS Service) , then selected EC2 as SERVICE NAME, then EVENT TYPE (AWS API call with cloudtrail),then specific operation(s) in the field directly below i provided "CreateVpc", 

ACTION
In the next window i selceted add target (Lambda function)  , using  my knowledge of python i was able to create a lambda function on aws SDK for python which is boto3 ,this lambda function is able to extract the vpc id from the event and enable the vpc flow logs.I added the lambda function arn  and then comlpleted the rule creation.

I configured the environment variables with the VPC flow log group ARN which i created on cloudwatch an also VPC flow logs role ARN.

RESULT: 
When a new VPC is created ,vpc flow logs is not enabled by default, if we navigate back to cloud watch service it is noticed that the lambda function has put in a log group for enableVpcflowlogs. and if we click the link for flow logs in newly created vpc ,we will verify there is an event creating flow logs.Now my Organization was able to enable vpc flow logs with automation .# Terraform-State

