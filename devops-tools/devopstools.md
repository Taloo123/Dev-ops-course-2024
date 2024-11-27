# Setting Up and Implementing a CI/CD Pipeline for Terraform and EKS

As part of my hands-on experience in DevOps, I implemented a CI/CD pipeline to automate the provisioning of an Amazon EKS cluster using Terraform and GitHub Actions. Below is a detailed and structured description, including the commands and YAML code used.

# Step 1: Preparing the GitHub Repository

I ensured that my GitHub repository contained the necessary Terraform code for provisioning an EKS cluster. This included configurations for networking, cluster creation, and other dependent AWS resources.

# Step 2: Setting Up the Workflows Directory

To define GitHub Actions workflows, I created the following directory structure in the repository:

bash
Copy code
mkdir -p .github/workflows
Step 3: Defining the CI/CD Pipeline
I created a YAML file, deploy.yml, in the .github/workflows/ directory. The pipeline had two main jobs: Terraform and Deployment.

YAML Code
yaml
Copy code
name: CI/CD Pipeline for Terraform EKS Cluster

on:
  push:
    branches:
      - main  # Trigger workflow on pushes to the main branch
  pull_request:
    branches:
      - main  # Trigger workflow on pull requests to the main branch

jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Terraform
        uses: hashicorp/setup-terraform@v1
        with:
          terraform_version: 1.3.7

      - name: Terraform Init
        run: terraform init

      - name: Terraform Plan
        run: terraform plan

      - name: Terraform Apply
        run: terraform apply -auto-approve
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_REGION: us-west-2  # Update to your desired AWS region

  deploy:
    runs-on: ubuntu-latest
    needs: terraform
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up kubectl
        uses: azure/setup-kubectl@v1

      - name: Configure kubectl
        run: kubectl config use-context <your-cluster-name>
        env:
          KUBE_CONFIG: ${{ secrets.KUBE_CONFIG }}

      - name: Deploy application to EKS
        run: |
          kubectl apply -f kubernetes-deployment.yaml  # Replace with the path to your manifest files
# Step 4: Configuring Secrets
I securely added the required secrets in the GitHub repository under Settings > Secrets and Variables > Actions:

AWS_ACCESS_KEY_ID: The AWS IAM access key.
AWS_SECRET_ACCESS_KEY: The corresponding secret access key.
KUBE_CONFIG: The base64-encoded Kubernetes configuration file for accessing the EKS cluster.
To encode the kubeconfig file:

bash
Copy code
cat ~/.kube/config | base64
Step 5: Committing and Pushing Changes
I committed and pushed the workflow to the repository:

bash
Copy code
git add .github/workflows/deploy.yml
git commit -m "Add CI/CD pipeline for Terraform and EKS"
git push origin main
Step 6: Testing the Pipeline
I tested the pipeline by performing the following:

Push a change to the main branch, triggering the workflow.
Create a pull request, observing the workflow execution in the "Actions" tab on GitHub.
The logs confirmed the successful execution of Terraform and Kubernetes steps.

Commands Used
Terraform Commands:

bash
Copy code
terraform init
terraform plan
terraform apply -auto-approve
Kubernetes Deployment:

bash
Copy code
kubectl apply -f kubernetes-deployment.yaml
Key Learnings and Achievements
Infrastructure Automation: Automated the provisioning of an EKS cluster using Terraform.
CI/CD Workflow Development: Created a GitHub Actions workflow for infrastructure and application deployment.
Kubernetes Management: Deployed applications on an EKS cluster using Kubernetes manifests.
Secure Secrets Management: Used GitHub Secrets for managing sensitive information.
This project reinforced my understanding of CI/CD pipelines, Terraform for infrastructure as code, and Kubernetes for container orchestration, preparing me for more advanced DevOps challenges.











