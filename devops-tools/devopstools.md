# Setting Up and Implementing a CI/CD Pipeline for Terraform and EKS

As part of my hands-on experience in DevOps, I successfully implemented a CI/CD pipeline for automating the deployment of an Amazon EKS cluster using Terraform and GitHub Actions. Here's a structured overview of the steps I undertook:

---

## Step 1: Preparing the GitHub Repository
I ensured my repository was hosted on GitHub and included all the necessary Terraform code to provision an EKS cluster. This included configurations for networking, cluster setup, and other AWS resources.

---

## Step 2: Setting Up the Workflows Directory
I created a `.github/workflows/` directory in my repository to define GitHub Actions workflows. This structure is essential for implementing CI/CD pipelines.

---

## Step 3: Defining the CI/CD Pipeline
I created a YAML file named `deploy.yml` in the workflows directory to define the pipeline. The pipeline consisted of two jobs:

1. **Terraform Job**:
   - Used the `actions/checkout` action to pull the code.
   - Configured Terraform with the `hashicorp/setup-terraform` action.
   - Initialized Terraform (`terraform init`) to set up the working environment.
   - Validated the configuration with **Terraform Plan**.
   - Applied infrastructure changes using **Terraform Apply**, provisioning the required AWS resources.

2. **Deployment Job**:
   - Configured Kubernetes CLI (`kubectl`) for the newly provisioned EKS cluster.
   - Deployed Kubernetes manifests (`kubernetes-deployment.yaml`) for the application.

Secrets such as `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` were securely injected using GitHub Secrets.

---

## Step 4: Configuring Secrets
I added the following secrets to the repository:
- **AWS_ACCESS_KEY_ID**: My AWS IAM access key.
- **AWS_SECRET_ACCESS_KEY**: The corresponding secret key.
- **KUBE_CONFIG**: Base64-encoded Kubernetes configuration file for EKS access.

---

## Step 5: Committing and Pushing Changes
I committed the `deploy.yml` file and pushed it to the repository, triggering the CI/CD workflow as defined.

---

## Step 6: Testing the Pipeline
I tested the pipeline by:
- Pushing changes to the `main` branch.
- Creating a pull request to validate workflow execution.

The pipeline provisioned the EKS cluster using Terraform and deployed the application on Kubernetes.

---

## Step 7: Reviewing Outputs
I monitored the logs in the "Actions" tab on GitHub to verify the success of each step:
- The Terraform job successfully provisioned the EKS cluster on AWS.
- Kubernetes manifests were applied correctly, deploying the application.

---

## Key Learnings and Achievements
- **Infrastructure Automation**: Streamlined EKS provisioning with Terraform and GitHub Actions.
- **CI/CD Principles**: Developed a robust pipeline combining infrastructure and application deployment.
- **Kubernetes Management**: Configured and deployed applications on EKS using Kubernetes.
- **Secrets Management**: Secured sensitive information using GitHub Secrets.

---

This project deepened my understanding of DevOps workflows, CI/CD pipelines, and cloud infrastructure automation, enhancing my knowledge of Terraform, GitHub Actions, and Kubernetes.
