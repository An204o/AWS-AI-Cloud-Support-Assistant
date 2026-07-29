# AWS AI Cloud Support Assistant

An AI-powered cloud troubleshooting assistant that helps diagnose common AWS infrastructure issues by analyzing customer support tickets and inspecting AWS resources.

The system uses Amazon Bedrock for AI reasoning, AWS Lambda for serverless processing, API Gateway for request handling, DynamoDB for ticket history, and AWS SDK (boto3) to retrieve infrastructure information from AWS services.

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
2. Analyzes the issue using Amazon Bedrock
3. Retrieves AWS resource information
4. Identifies possible root causes
5. Provides troubleshooting recommendations
6. Stores the incident history for future reference

---

# Architecture

```
                 Customer
                    |
                    |
              API Gateway
                    |
                    |
                 Lambda
                    |
        -------------------------
        |                       |
        |                       |
 Amazon Bedrock             AWS SDK
    (AI Reasoning)          (boto3)
                                |
                                |
                    -----------------------
                    |          |          |
                  EC2       IAM       CloudWatch


                    |
                    |
                DynamoDB

             (Ticket History)
```

---

# AWS Services Used

## Amazon API Gateway

Purpose:

Provides an API endpoint where users submit cloud support issues.

Example request:

```json
{
  "issue": "My EC2 instance cannot connect through SSH"
}
```

---

## AWS Lambda

Purpose:

Serverless backend that processes incoming support requests.

Responsibilities:

* Receives API requests
* Calls Amazon Bedrock
* Queries AWS resources
* Returns troubleshooting recommendations

Benefits:

* No server management
* Automatic scaling
* Pay-per-use architecture

---

## Amazon Bedrock

Purpose:

Provides AI reasoning capabilities.

The model analyzes infrastructure problems and generates troubleshooting steps.

Example:

Input:

```
EC2 SSH connection failed
```

AI response:

```
Possible causes:

1. Security Group does not allow inbound port 22
2. Incorrect SSH key
3. Instance is stopped
4. Network ACL blocking traffic

Recommended actions:

- Verify security group rules
- Confirm instance status
- Check CloudWatch logs
```

---

## AWS SDK (boto3)

Purpose:

Allows the AI assistant to interact with AWS resources.

Examples:

Check EC2 instances:

```python
ec2.describe_instances()
```

Check CloudWatch alarms:

```python
cloudwatch.describe_alarms()
```

Check IAM permissions:

```python
iam.list_roles()
```

---

## Amazon DynamoDB

Purpose:

Stores support tickets and troubleshooting history.

Example data:

| Attribute | Example              |
| --------- | -------------------- |
| Ticket ID | 001                  |
| Issue     | EC2 SSH failure      |
| Solution  | Check security group |
| Timestamp | 2026-07-28           |

---

# Features

## AI-Based Troubleshooting

The assistant understands natural language cloud problems.

Example:

User:

```
My website is slow after deploying a new EC2 instance
```

Assistant:

```
Possible causes:

- High CPU utilization
- Insufficient instance type
- Database bottleneck
- Network latency

Recommended checks:

1. Review CloudWatch CPU metrics
2. Check EC2 instance type
3. Inspect application logs
```

---

## AWS Resource Inspection

The assistant can retrieve information about:

* EC2 instances
* CloudWatch alarms
* IAM roles
* Resource health

---

## Automated Diagnosis

Instead of manually checking multiple AWS services, the assistant provides a troubleshooting workflow.

Traditional process:

```
Customer issue
      |
      |
Engineer manually checks:
EC2
IAM
CloudWatch
Security Groups
      |
      |
Resolution
```

With AI assistant:

```
Customer issue
      |
      |
AI Analysis
      |
      |
AWS Resource Checks
      |
      |
Recommended Solution
```

---

# Project Structure

```
aws-cloud-support-assistant/

│
├── lambda/
│   ├── lambda_function.py
│   └── requirements.txt
│
├── api/
│   └── api_definition.json
│
├── infrastructure/
│   └── terraform/
│
├── database/
│   └── dynamodb_schema.md
│
├── prompts/
│   └── troubleshooting_prompt.txt
│
└── README.md
```

---

# Example Workflow

## Step 1: Customer submits issue

Request:

```
"My EC2 instance is running but I cannot SSH into it."
```

---

## Step 2: API Gateway receives request

API Gateway forwards request to Lambda.

---

## Step 3: Lambda analyzes issue

Lambda:

* Sends problem to Bedrock
* Queries AWS APIs
* Collects infrastructure information

---

## Step 4: AI generates diagnosis

Example output:

```
Issue Category:
Networking

Possible Causes:

1. Port 22 blocked in security group
2. Incorrect private key
3. Instance does not have public IP

Recommended Actions:

Check EC2 security group inbound rules.
```

---

## Step 5: Save ticket history

DynamoDB stores:

```
Problem:
SSH failure

Resolution:
Security group rule correction
```

---

# Security Design

The project follows AWS security best practices:

## IAM Least Privilege

Lambda receives only required permissions:

```
ec2:DescribeInstances

cloudwatch:DescribeAlarms

iam:GetRole
```

---

## No Hardcoded Credentials

Authentication uses:

* IAM roles
* AWS SDK credential provider

---

## Serverless Architecture

No public servers are exposed.

Architecture:

```
API Gateway
      |
      |
Lambda
      |
      |
AWS Services
```

---

# Future Improvements

## Automated Remediation

Automatically fix issues:

Examples:

* Restart unhealthy EC2 instances
* Add missing security group rules
* Create CloudWatch alarms

Architecture:

```
CloudWatch Alarm

       |

Lambda

       |

EC2 Recovery Action
```

---

## RAG Knowledge Base

Add AWS documentation and troubleshooting guides.

Architecture:

```
AWS Documentation
        |
        |
Vector Database
        |
        |
Bedrock Retrieval
        |
        |
Better Answers
```

---

## Multi-Agent Support System

Create specialized agents:

* EC2 troubleshooting agent
* Networking agent
* IAM security agent
* Database agent

---

# Technologies

## Languages

* Python

## AWS Services

* Amazon Bedrock
* AWS Lambda
* API Gateway
* DynamoDB
* EC2
* CloudWatch
* IAM

## AI

* Large Language Models
* Prompt Engineering
* Retrieval-Augmented Generation (RAG)

## Tools

* AWS SDK (boto3)
* Terraform (optional)

---

# Resume Description

**AWS AI Cloud Support Assistant**
*Python | AWS Lambda | Amazon Bedrock | API Gateway | DynamoDB | boto3*

* Built an AI-powered cloud troubleshooting assistant using Amazon Bedrock and AWS Lambda to analyze infrastructure issues and recommend remediation steps.
* Integrated AWS SDK APIs to inspect EC2, IAM, and CloudWatch resources, automating diagnosis of common cloud failures.

---

# Learning Outcomes

Through this project, I gained experience with:

* Designing serverless AWS architectures
* Troubleshooting cloud infrastructure
* Implementing IAM security practices
* Using AI models for cloud operations
* Automating AWS support workflows
