# NBA Game Day Notifications / Sports Alerts System

## Project Overview

The Game Day Notifications project is designed to send real-time NBA game score updates to users via SMS or Email. It utilizes Amazon SNS, AWS Lambda, Amazon EventBridge, and the NBA Game API (SportsData.io) to provide sports fans with up-to-date game information. This project showcases how cloud technologies can be used to build automated alert systems with a focus on efficiency and security.

## Features

- Fetches live NBA game scores using the SportsData.io API.
- Sends score updates to users through SMS/Email using Amazon SNS.
- Scheduled updates are automated using Amazon EventBridge.
- Built with security in mind, ensuring least privilege policies are followed for IAM roles.

## Prerequisites

- **SportsData.io Account**: Sign up for a free account and get your API Key.
- **AWS Account**: Basic understanding of AWS services and Python is required.
- **Python**: Version 3.x for Lambda function deployment.

## Technical Architecture

- **API**: NBA Game API (via SportsData.io)
- **Cloud Provider**: AWS (Amazon Web Services)
- **Core Services**: SNS (Simple Notification Service), Lambda, EventBridge
- **Programming Language**: Python 3.x
- **IAM Security**: Implemented least privilege policies for Lambda, SNS, and EventBridge.

## Project Structure

game-day-notifications/ ├── src/ │ ├── gd_notifications.py # Main Lambda function code ├── policies/ │ ├── gd_sns_policy.json # SNS publishing permissions │ ├── gd_eventbridge_policy.json # EventBridge to Lambda permissions │ └── gd_lambda_policy.json # Lambda execution role permissions ├── .gitignore └── README.md # Project documentation

## 2. Create an SNS Topic
Go to the AWS Management Console.
Navigate to the SNS service.
Click Create Topic and choose Standard for the topic type.
Name the topic (e.g., gd_topic) and note down the ARN.
Click Create Topic.
## 3. Add Subscriptions to the SNS Topic
After creating the topic, click on the topic name.
Navigate to the Subscriptions tab and click Create subscription.
For Email:
Select Email and enter the email address.
For SMS (phone number):
Select SMS and enter the phone number in international format (e.g., +1234567890).
Click Create Subscription.
For Email: Confirm subscription via the link sent to the inbox.
For SMS: Subscription is immediately active.
## 4. Create the SNS Publish Policy
Go to IAM service in the AWS Management Console.
Navigate to Policies → Create Policy.
Choose JSON and paste the policy from gd_sns_policy.json.
Replace REGION and ACCOUNT_ID with your own AWS region and account ID.
Click Next: Tags (optional) → Next: Review.
Name the policy (e.g., gd_sns_policy) and click Create Policy.
## 5. Create an IAM Role for Lambda
Go to IAM → Roles → Create Role.
Select AWS Service and choose Lambda.
Attach the following policies:
gd_sns_policy (created in the previous step).
AWSLambdaBasicExecutionRole.
Click Next: Tags (optional) → Next: Review.
Name the role (e.g., gd_role) and click Create Role.
Save the ARN of the role for use in the Lambda function.
## 6. Deploy the Lambda Function
Go to Lambda service in the AWS Management Console.
Click Create Function → Author from Scratch.
Name the function (e.g., gd_notifications).
Select Python 3.x as the runtime.
Assign the IAM role (gd_role) created earlier.
Under Function Code, paste the contents of src/gd_notifications.py from the repository.
In Environment Variables, add:
  NBA_API_KEY: your NBA API key
  SNS_TOPIC_ARN: the ARN of the SNS topic you created earlier.
Click Create Function.
## 7. Set Up Automation with EventBridge
Go to EventBridge service in the AWS Management Console.
Navigate to Rules → Create Rule.
Select Event Source as Schedule.
Set the cron schedule for when you want updates (e.g., hourly).
Under Targets, select the Lambda function (gd_notifications) and save the rule.
## Test the System
Go to your Lambda function in the AWS Console.
Create a test event to simulate execution.
Run the function and check CloudWatch Logs for any errors.
Verify that SMS notifications are being sent to the subscribed users.
## What We Learned
Designing a notification system using AWS SNS and Lambda.
Securing AWS services by implementing least privilege IAM policies.
Automating workflows using EventBridge for scheduled events.
Integrating external APIs (NBA Game API) into cloud-based systems.
Future Enhancements
Add NFL score alerts to expand functionality.
Store user preferences (e.g., teams, game types) in DynamoDB for personalized alerts.
Implement a web UI for managing notifications and preferences
