
# Terraform AKS Cluster with Husky and GitHub Actions CI/CD Pipeline

## Overview

This project demonstrates Infrastructure as Code (IaC) for provisioning an Azure Kubernetes Service (AKS) cluster using Terraform. It integrates **Husky** pre-commit hooks for local code quality checks and **GitHub Actions** workflows for automated validation on pull requests.

---

## Setup Instructions

### 1. Auth0 Setup (If applicable)
> *Include here if your app uses Auth0, otherwise omit or customize.*

### 2. Azure Infrastructure

- Install [Terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli)
- Configure your Azure CLI and login (`az login`)
- The Terraform script in `infrastructure/main.tf` provisions at least one Azure resource (e.g., resource group).

### 3. Husky Pre-commit Hooks

- Initialize Node.js project:

  ```bash
  npm init -y
  ```

- Install Husky:

  ```bash
  npm install husky --save-dev
  npx husky install
  npx husky-init
  ```

- Update pre-commit hook to run:

  ```bash
  echo "terraform fmt -check -recursive" > .husky/pre-commit
  echo "terraform validate" >> .husky/pre-commit
  echo "tflint" >> .husky/pre-commit
  chmod +x .husky/pre-commit
  ```

- The pre-commit hook will prevent commits with formatting or validation errors.

### 4. GitHub Actions Workflow

- The workflow file `.github/workflows/action-terraform-verify.yml` automatically runs on pull requests to validate:

  - `terraform fmt` formatting
  - `terraform validate`

- It ensures Terraform code quality before merging.

---

## Logging Explanation

> *If applicable — describe what logs you capture locally or on Azure for monitoring infrastructure health and troubleshooting.*

---

## Monitoring & Detection (KQL Query Explained)

> *Include any Kusto Query Language (KQL) queries used in Azure Monitor or Log Analytics for detecting issues or security events.*

---

## Alert Setup

- Alerts are configured in Azure Monitor to watch for critical infrastructure metrics or logs.
- When alerts fire, automation or notifications are triggered to respond promptly.

---

## How to Test Locally and in CI/CD

1. Make a formatting or syntax error in your Terraform files.
2. Try to commit locally — Husky pre-commit hooks will block the commit.
3. Commit using `--no-verify` to bypass Husky and push the changes to a feature branch.
4. Create a pull request — GitHub Actions will run the validation workflow and fail on errors.
5. Fix the errors and push — the workflow should pass.

---

## Submission

Submit the GitHub repository URL containing:

- Terraform infrastructure code  
- Husky pre-commit setup  
- GitHub Actions workflow file  

---

## Author

Satyam Panseriya

---

