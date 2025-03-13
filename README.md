# Ansible Demo

This repository contains Ansible playbooks and configurations for provisioning and managing cloud infrastructure across
AWS, Azure, and GCP. Automation is designed to ensure consistent setup and maintenance of cloud resources using Ansible,
integrated with GitHub Actions for the CI/CD.

Integrations run via a trigger sent by [Terraform repository](https://github.com/leo-ely/terraform-demo) every time it
gets successfully deployed in all cloud providers. Also, it can be manually run, for testing scenarios.

The users needed for correct Ansible provisioning can be created using the same steps as in Terraform configuration (
refer to link above).

## Features

* **Multi-cloud support**: automates provisioning and configuration for the 3 major cloud providers.
* **GitOps Workflow**: uses GitHub Actions to deploy Ansible playbooks.
* **Dynamic Inventory management**: fetches live cloud inventory from Terraform-managed storage resources.
* **Secure Credentials management**: uses GitHub Secrets and cloud-native secret stores.
* **Role-based structure**: modular Ansible roles for scalability and maintainability.

## GitHub Actions integration

Each cloud provider has a dedicated GitHub Actions workflow under `.github/workflows/`.

Access credentials and necessary variables are provided by GitHub Secrets and Variables.

### Dynamic Inventory

The inventory files are dynamically updated using Terraform and its managed storage.

* **AWS**: fetches inventory from a S3 Bucket.
* **Azure**: fetches inventory from a Azure Storage Blob.
* **GCP**: fetches inventory from a Cloud Storage Bucket.

### Security & Best Practices

* **Secrets Management**: use GitHub Secrets for API keys and credentials.
* **IAM Roles**: prioritize IAM roles over hardcoded credentials.
* **State management**: store Inventory state in Cloud Storage instead of version control.

---

## Repository file tree

```
├── inventories/
│   ├── aws.yml      # AWS dynamic inventory
│   ├── azure.yml    # Azure dynamic inventory
│   ├── gcp.yml      # GCP dynamic inventory
│
├── playbooks/
│   ├── aws.yml      # AWS-specific playbook
│   ├── azure.yml    # Azure-specific playbook
│   ├── gcp.yml      # GCP-specific playbook
│
├── roles/
│   ├── aws/
│   │   ├── tasks/
│   │   │   ├── ec2_instances.yml       # EC2 Instances configuration
│   │   │   ├── main.yml
│   │
│   ├── azure/
│   │   ├── tasks/
│   │   │   ├── virtual_machines.yml    # Virtual Machines configuration
│   │   │   ├── main.yml
│   │
│   ├── gcp/
│   │   ├── tasks/
│   │   │   ├── compute_instances.yml   # Compute Engine VM Instances configuration
│   │   │   ├── main.yml
│
├── vars/
│   ├── aws.yml      # AWS credentials and variables
│   ├── azure.yml    # Azure credentials and variables
│   ├── gcp.yml      # GCP credentials and variables
│
├── .github/workflows/
│   ├── ansible-lint.yml     # Ansible linter
│   ├── aws-ansible.yml      # Actions workflow for AWS
│   ├── azure-ansible.yml    # Actions workflow for Azure
│   ├── gcp-ansible.yml      # Actions workflow for GCP
│   ├── main.yml             # Actions workflow for orchestration
```
