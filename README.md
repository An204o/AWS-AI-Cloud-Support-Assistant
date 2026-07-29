# AWS AI Cloud Support Assistant

An AI-powered cloud troubleshooting assistant that helps diagnose common AWS infrastructure issues by analyzing customer support tickets and inspecting AWS resources.

The system uses Amazon Bedrock (Claude Opus 4.5) for AI reasoning, AWS Lambda for serverless processing, API Gateway for request handling, DynamoDB for ticket history, and AWS SDK (boto3) to retrieve infrastructure information from AWS services.

---

# Project Overview

Cloud support engineers frequently troubleshoot issues such as:

* EC2 instances becoming unreachable
* High CPU utilization
* IAM permission failures
* Application downtime
* Network connectivity problems

This project simulates a cloud support workflow where a customer submits an infrastructure issue and the AI assistant:

1. Receives the support request
2. Analyzes the issue using Amazon Bedrock (Claude Opus 4.5)
3. Retrieves AWS resource information
4. Identifies possible root causes
5. Provides troubleshooting recommendations
6. Stores the incident history for future reference

---
