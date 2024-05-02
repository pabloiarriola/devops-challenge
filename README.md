# Secure API Deployment with AWS Lambda and API Gateway

This project demonstrates a secure and efficient cloud-based API service using AWS Lambda and API Gateway, managed via Infrastructure as Code (IaC) with AWS CloudFormation and automated through a GitHub Actions CI/CD pipeline.

## Overview

The solution is designed to leverage AWS services to host a public HTTP API. The deployment uses roles instead of user credentials for enhanced security and implements environment-specific access controls to minimize privilege, adhering to the principle of least privilege.

## Architecture

- **AWS API Gateway**: Manages incoming API requests and interfaces with Lambda functions.
- **AWS Lambda**: Handles backend processing of API requests with minimum necessary permissions for security.
- **AWS CloudFormation**: Deploys and manages AWS resources declaratively using SAM for the transformation of the template.
- **GitHub Actions**: Automates updates and deployment across multiple environments (development, staging, production).

## Repository Structure

- `lambda_api_publico/`: Contains the source code for the Lambda functions.
- `template.yaml`: AWS CloudFormation template for infrastructure setup.
- `README.md`: Documentation of the project setup and workflows.
- `.github/workflows/`: Contains the CI/CD pipeline configuration for GitHub Actions.

## Key Features

- **Role-Based Deployment**: Utilizes IAM roles for deploying resources, enhancing security by avoiding the use of user credentials.
- **Environment-Specific Branches**: Configures development, staging, and production environments with specific branches, allowing for controlled updates and testing before production deployment.
- **Granular Control with API Gateway**: Manages API Gateway as a separate resource for better control
- **Canary Deployments**: Implements canary deployments for the production environment, ensuring safe rollouts through phased updates.

## Local Development Setup

### Prerequisites

- AWS account
- GitHub account
- Python 3 installed on your local machine
- AWS CLI and AWS SAM CLI installed

### Steps

1. **Clone the repository:**

   ```bash
   git clone https://github.com/pabloiarriola/devops-challenge
   cd devops-challenge

2. **Install dependencies:**

    ```bash
    pip install -r requirements.txt

3. **Set up AWS credentials:**

    ```bash
    aws configure

4. **Start local development server:**

    ```bash
    sam local start-api

## CI/CD Pipeline
 **GitHub Actions Workflows:**
 - **deployment**: Deploys to AWS on push to development, staging and production branches. Only production branch uses canary deployments. It also mocks code analysis when pr is created for staging and production

## Monitoring and Logging
The role it has can send logs to cloudwatch and you can use the specific lambda metrics 


## Common Issues
**IAM Permissions:** Ensure that the IAM roles and policies are correctly configured to avoid deployment errors.

**SAM VERSION:** check if there are any breaking changes in new sam releases, the pipelines shows which version its using

## Future implementations
**Specific SAM:** use a specific sam version in the runner, this is to standardize the versions thought the company.

**Deployment to different aws accounts:** deploy to a different account depending on the env variable, to close permissions

**Code analysis:** implement a static code analysis like for example sonar cloud 

**Define development deployments:** define how the deployments  to development will work, you could use sam local invoke in their local machines for them to try as having to wait for each commit to deploy can be time consuming. Normally development deployment is handled by the developers. 

**Use separate yml for api gateway:** this is to not have circular dependencies with the lambdas and to be able to close the invoke permissions on them 
