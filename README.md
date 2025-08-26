AI Assistant App Infrastructure
This repository contains the Infrastructure as Code (IaC) using Terraform to automatically provision and manage the AI Assistant application's infrastructure on AWS.

This project deploys all necessary components, from the networking foundation and database to the machine learning environment and monitoring system.

⚙️ Technology Stack
Infrastructure as Code: Terraform

Cloud Provider: AWS (Amazon Web Services)

CI/CD: GitLab CI

Key AWS Services:

Networking: VPC, Subnets, Security Groups

Database: RDS for PostgreSQL

Compute: Lambda, SageMaker

Storage: S3 (for data and Terraform state)

Security: IAM, Secrets Manager

Monitoring: CloudWatch, SNS

📂 Project Structure
The project is organized using a modular and multi-environment approach.

modules/: Contains reusable Terraform modules for each logical infrastructure component (e.g., vpc, rds, sagemaker). Each module is self-contained and responsible for its set of resources.

envs/: Contains the configuration for each environment (test, prod). The root files in these folders call the modules from modules/ and pass the required variables, assembling the infrastructure for a specific environment.

🚀 Deployment
The infrastructure deployment is fully automated via GitLab CI/CD.

Prerequisites
AWS Account: Access to an AWS account is required.

GitLab Repository: The project is configured to work with GitLab.

CI/CD Configuration
For the pipeline to execute successfully, navigate to Settings -> CI/CD -> Variables in your GitLab repository and add the following variables:

AWS_ACCESS_KEY_ID: Your AWS access key.

AWS_SECRET_ACCESS_KEY: Your AWS secret key (mark as Masked).

TF_VAR_db_username: The master username for the RDS database.

TF_VAR_db_password: The master password for the RDS database (mark as Masked and Protected).

TF_VAR_alarm_email: The email address to receive CloudWatch alarm notifications.

Deployment Process
Make the desired changes to the Terraform code.

Commit and push to your feature branch.

Create a Merge Request into the main branch.

Once the Merge Request is approved and merged, the GitLab CI pipeline will automatically trigger, running terraform plan and terraform apply for the target environment.

✨ Key Features
Secure Secret Management: 🔑 Database credentials are not stored in the codebase. They are passed via GitLab CI/CD variables and securely stored in AWS Secrets Manager. SageMaker and other services access them on-the-fly using IAM Roles.

Automated Monitoring: 🚨 An automated monitoring system is created for each Lambda function using CloudWatch. If a function produces at least one error within a 5-minute window, a notification is sent to the specified alarm_email.

Isolated Environments: 🌐 The project structure allows for easy maintenance of multiple environments (e.g., test and prod) with different configurations, all based on the same reusable modules.

Data Science Environment: 🤖 A SageMaker Notebook Instance is deployed within a private subnet with pre-configured access to the database and S3, providing a secure and ready-to-use environment for ML model development.
