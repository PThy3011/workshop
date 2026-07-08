---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Automating Oracle Database@AWS Deployment with Terraform

Deploying Oracle database systems in the cloud always requires a balance between performance, scalability, and infrastructure management consistency. With Oracle Database@AWS (ODB@AWS), Oracle has brought the Exadata platform — a hardware system optimized specifically for Oracle Database — directly into AWS data centers. This allows businesses to leverage Oracle’s high performance while taking advantage of AWS’s rich ecosystem of services.

However, building a complete Oracle Database@AWS environment involves many configuration steps: setting up the ODB Network, deploying Exadata Infrastructure, creating VM Clusters, and connecting to Amazon VPC. Performing these steps manually through the AWS Console is complex, time-consuming, and prone to errors as the number of environments grows.

In this article, we will explore how to use Terraform to fully automate the deployment of Oracle Database@AWS. Through the Infrastructure as Code (IaC) model, organizations can standardize their infrastructure, minimize configuration errors, and deploy systems quickly and consistently.

---

## Architecture Overview

Oracle Database@AWS is designed to combine the performance of Oracle Exadata with the scalability and flexibility of AWS. Instead of running Oracle Database on separate infrastructure, businesses can deploy it directly within AWS while still utilizing Exadata’s optimized capabilities.

In this model, Terraform acts as the orchestration tool for the entire resource creation process. Infrastructure components are described in HCL code, and Terraform automatically deploys them in the correct dependency order, ensuring consistency across environments.

The solution consists of four main components:

- **ODB Network**: A dedicated network that connects AWS and Oracle Cloud Infrastructure (OCI), providing a private, low-latency connection.
- **Oracle Exadata Infrastructure**: Exadata hardware deployed directly in an AWS Availability Zone to deliver high-performance data processing.
- **Exadata VM Cluster**: A cluster of virtual machines running Oracle Grid Infrastructure and Oracle Database.
- **ODB Peering Connection**: A private network connection between Amazon VPC and the ODB Network, allowing applications on AWS to securely access the Oracle Database.

> *Figure 1. High-level architecture; colored boxes represent individual services.*

Once these components are successfully created, organizations can deploy Oracle Databases with full scalability, high availability, and seamless integration with AWS services.

---

## Why Use Terraform?

Terraform is one of the most popular Infrastructure as Code tools today. Instead of manually operating through the AWS Management Console, the entire infrastructure is defined as HCL (HashiCorp Configuration Language) source code. Terraform reads these configuration files and automatically provisions resources in the correct order.

Adopting Terraform brings many benefits:

- Complete automation of infrastructure deployment.
- Elimination of manual configuration tasks in the AWS Console.
- Consistent configuration across Development, Testing, and Production environments.
- Easy change management through Git.
- Reusable configurations across multiple projects.
- Ability to scale and update infrastructure without affecting existing resources.

For organizations deploying multiple Oracle Database systems or practicing DevOps, Terraform significantly reduces deployment time and improves infrastructure control.

---

## Prerequisites

Before running Terraform, ensure the following preparations are complete:

### 1. Register for Oracle Database@AWS

Organizations must subscribe to Oracle Database@AWS through AWS Marketplace and complete the onboarding process with Oracle.

### 2. Account Linking

The AWS Account must be linked with an Oracle Cloud Infrastructure (OCI) Tenancy so Terraform can manage resources across both platforms.

### 3. Configure Terraform Providers

Terraform requires configuration of two providers:
- AWS Provider
- OCI Provider

These providers allow Terraform to communicate with the APIs of both AWS and Oracle Cloud.

### 4. Set Up IAM Permissions

The account used by Terraform must have sufficient permissions to create, update, and delete resources on both AWS and Oracle Cloud.

Once these prerequisites are met, administrators can begin deploying Oracle Database@AWS infrastructure using Terraform.

---

## Deployment Process with Terraform

Terraform creates Oracle Database@AWS components in the correct dependency order. Each component is defined as a Terraform Resource.

### Step 1: Create ODB Network

The first step is to create the Oracle Database Network, which establishes a private connection between AWS and Oracle Cloud Infrastructure.

Example Terraform configuration:

```hcl
resource "aws_odb_network" "example" {
  display_name         = "odb-my-net"
  availability_zone_id = "use1-az6"
  client_subnet_cidr   = "10.2.0.0/24"
  backup_subnet_cidr   = "10.2.1.0/24"
  s3_access            = "DISABLED"
  zero_etl_access      = "DISABLED"
  tags = {
    "env" = "dev"
  }
}
...
```
VM Cluster is the environment where Oracle Database is deployed and operated.

Within the VM Cluster, administrators can configure:

- Number of CPU cores
- Memory allocation
- Oracle Grid Infrastructure
- Oracle Home
- Oracle Database version

By defining these configurations in Terraform, the infrastructure becomes reusable, version-controlled, and easier to maintain across multiple environments.

### Step 4. Configure the ODB Peering Connection

After the Oracle Database Infrastructure has been provisioned, the final step is to establish a network connection between the Amazon VPC and the ODB Network.

```hcl
resource "aws_odb_network_peering_connection" "example" {
  display_name    = "example-peering"
  odb_network_id  = "<odb-network-id>"
  peer_network_id = "<vpc-id>"

  tags = {
    "env" = "dev"
  }
}
```

The ODB Peering Connection enables applications running on Amazon EC2, Amazon ECS, or Amazon EKS to securely access Oracle Database through a private network connection, reducing latency while enhancing security.

Once this step is completed, the Oracle Database@AWS infrastructure is fully provisioned and ready for database deployment.

---

## Architecture After Deployment

After Terraform completes the provisioning process, the entire Oracle Database@AWS infrastructure is created automatically according to the dependency relationships defined in the configuration. Terraform manages these dependencies internally, eliminating the need for manual configuration through the AWS Management Console.

The deployed architecture consists of the following components:

| Component | Description |
|-----------|-------------|
| ODB Network | Establishes a private network connection between AWS and Oracle Cloud Infrastructure (OCI). |
| Oracle Exadata Infrastructure | Provides the Exadata hardware infrastructure required to run Oracle Database. |
| Oracle Exadata VM Cluster | Hosts Oracle Grid Infrastructure and Oracle Database instances. |
| ODB Peering Connection | Connects the Amazon VPC to the ODB Network, enabling secure database access. |
| AWS Provider | Manages AWS resources during deployment. |
| OCI Provider | Manages Oracle Cloud Infrastructure resources. |

All resources are tracked through the **Terraform State**, allowing administrators to monitor infrastructure status, apply updates, and scale the environment efficiently.

---

## Deploying the Solution with Terraform

AWS provides a sample Terraform project that simplifies the deployment of Oracle Database@AWS resources.

First, clone the sample repository:

```bash
git clone https://github.com/aws-samples/sample-odb-launch-using-terraform.git

cd sample-odb-launch-using-terraform
```

Next, initialize Terraform:

```bash
terraform init
```

This command downloads the required providers, including the AWS Provider and OCI Provider.

Before provisioning the infrastructure, review the execution plan:

```bash
terraform plan
```

Terraform analyzes the configuration files and displays the resources that will be created, modified, or destroyed.

If the plan is correct, deploy the infrastructure using:

```bash
terraform apply
```

Terraform provisions the resources in the following order:

1. Create the ODB Network.
2. Provision the Oracle Exadata Infrastructure.
3. Create the Oracle Exadata VM Cluster.
4. Configure the ODB Peering Connection.
5. Update the Terraform State.

After the deployment is complete, the Oracle Database@AWS environment is ready for database provisioning and application connectivity.

---

## Best Practices for Using Terraform

For enterprise Oracle Database deployments, AWS recommends following several best practices to improve infrastructure reliability and maintainability.

### 1. Always Run `terraform plan` Before `terraform apply`

Reviewing the execution plan helps identify unexpected infrastructure changes before they affect production environments.

### 2. Store Terraform State Remotely

Avoid storing the `terraform.tfstate` file on a local machine.

Instead, use:

- Amazon S3 to store the Terraform State.
- Amazon DynamoDB for state locking.

This approach enables multiple team members to collaborate safely without causing state conflicts.

### 3. Manage Infrastructure as Source Code

Store Terraform configurations in a version control system such as GitHub or GitLab to:

- Track infrastructure changes.
- Perform code reviews.
- Restore previous configurations when necessary.
- Integrate with CI/CD pipelines.

### 4. Separate Deployment Environments

Use Terraform variables or workspaces to isolate different environments, including:

- Development
- Testing
- Staging
- Production

Separating environments reduces deployment risks and simplifies infrastructure management.

### 5. Avoid Manual Changes in the AWS Console

Once Infrastructure as Code has been adopted, infrastructure changes should be made exclusively through Terraform instead of directly in the AWS Management Console. This helps prevent **configuration drift** and ensures that deployed resources remain consistent with the source code.

---

## Target Audience

The Oracle Database@AWS and Terraform solution is well suited for several technical roles:

- **Database Administrators (DBAs):** Automate Oracle Database deployment and administration.
- **Cloud Engineers:** Standardize Oracle infrastructure using Infrastructure as Code.
- **DevOps Engineers:** Integrate database deployment into CI/CD pipelines.
- **Enterprise Architects:** Design scalable, maintainable Oracle Database infrastructure.
- **Enterprise Organizations:** Migrate Oracle Database workloads from on-premises environments to AWS while maintaining the high performance of Oracle Exadata.

---

## Conclusion

Oracle Database@AWS introduces a modern approach to deploying Oracle Database on AWS by combining the performance of Oracle Exadata with the flexibility and scalability of AWS services. However, provisioning the required infrastructure involves multiple interconnected components and requires a consistent deployment process.

Terraform addresses these challenges through the **Infrastructure as Code (IaC)** approach, allowing infrastructure to be defined, deployed, and managed using code rather than manual configuration. By automating resource provisioning, version-controlling infrastructure, and enabling configuration reuse, Terraform significantly reduces deployment time while improving operational consistency and reliability.

For organizations building new Oracle Database environments or modernizing existing infrastructure on AWS, combining Oracle Database@AWS with Terraform provides a scalable, repeatable, and efficient deployment strategy that simplifies long-term infrastructure management.

To learn more about this solution and access the sample Terraform project, refer to the official AWS Database Blog and the AWS sample repository on GitHub.
