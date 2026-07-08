---
title: "Blog 2"
date: 2026-06-29
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---


# Cara Pioneers Domain-Specific AI for Enterprise Insurance Brokerages with AWS

The insurance industry is a global market worth more than **$8 trillion**, yet it continues to face significant operational challenges caused by outdated manual processes and an increasing shortage of experienced professionals. To address these challenges, **Cara** has developed an AI-native platform built on AWS that automates complex back-office operations specifically for enterprise insurance brokerages.

This blog explores the industry's key challenges, the architecture of Cara's AI solution, and the measurable business outcomes achieved through its collaboration with AWS.

---

## Challenges in Enterprise Insurance

Insurance brokers and account managers spend a significant amount of time performing repetitive administrative tasks, including completing submission forms, comparing insurance quotes, reviewing policy coverage, entering information into legacy systems, and coordinating communication between clients and insurance carriers. As workforce shortages continue to grow, brokerages need ways to increase productivity without proportionally expanding their teams.

However, traditional general-purpose AI solutions struggle to meet the unique requirements of the insurance industry because of several factors:

1. **Strict regulatory compliance:** Insurance operations require high levels of accuracy, auditability, and compliance with industry regulations.

2. **Highly sensitive information:** AI systems must securely process personally identifiable information (PII), financial records, and complex insurance policy documents.

3. **Industry-specific knowledge:** Effective automation requires deep understanding of insurance terminology, underwriting guidelines, carrier-specific requirements, and different product lines.

---

## Cara's Vision and Journey

Cara's founding team has extensive experience building and operating one of the largest digital insurance brokerages. During that journey, they developed an internal AI copilot to streamline their own brokerage operations.

After witnessing significant improvements in operational efficiency, they recognized that many other brokerages faced similar challenges. This realization led to the creation of Cara as a **domain-specific AI platform** designed specifically for enterprise insurance brokerages rather than a general-purpose AI assistant.

By focusing exclusively on the insurance industry, Cara delivers AI capabilities that understand insurance workflows, documentation, and business processes at a much deeper level than traditional AI solutions.

---

## Solution Architecture on AWS

Cara is built using core AWS services to provide scalability, reliability, and enterprise-grade security.

### 1. Compute and Orchestration

Cara runs entirely on **Amazon Elastic Kubernetes Service (Amazon EKS)**, which orchestrates containerized microservices across multiple Availability Zones.

Key capabilities include:

- **Multi-tenant isolation:** Each insurance brokerage operates within dedicated Kubernetes namespaces, providing logical separation between customers.
- **Automatic scaling:** Kubernetes automatically adjusts compute resources based on workload demand, ensuring consistent performance during peak business periods.

### 2. Artificial Intelligence and Inference

Cara leverages **Amazon Bedrock** to access leading foundation models through a fully managed API without managing GPU infrastructure.

Amazon Bedrock powers several core AI capabilities, including:

- **Coverage comparison and quote analysis:** Automatically compares quotes from multiple insurance carriers, summarizes coverage differences, and highlights exclusions or policy gaps.
- **Form automation:** Extracts information from source documents and automatically populates ACORD forms and supplemental applications.
- **Renewal proposal generation:** Produces branded client proposals and renewal spreadsheets with minimal manual effort.

### 3. Enterprise Security and Data Isolation

Cara follows an **account-per-tenant** deployment model on AWS.

Each brokerage's environment is completely isolated, while all data is encrypted both **at rest** and **in transit**. Access to AWS resources is controlled through **AWS Identity and Access Management (AWS IAM)**, ensuring that every organization maintains a secure and independent environment.

### 4. System Integrations

Cara integrates seamlessly with industry-standard Agency Management Systems (AMS) and Customer Relationship Management (CRM) platforms.

These integrations automatically synchronize customer accounts, insurance policies, and supporting documents, eliminating duplicate data entry and improving operational efficiency.

---

## Infrastructure Automation with Terraform

To accelerate customer onboarding while maintaining infrastructure consistency, Cara provisions cloud resources using **Infrastructure as Code (IaC)** with Terraform.

The following example illustrates a simplified Terraform configuration used to provision tenant-specific resources.

```hcl
resource "kubernetes_namespace" "tenant_workspace" {
  metadata {
    name = "cara-tenant-${var.tenant_id}"

    labels = {
      environment = "production"
      tenant_type = "enterprise"
    }
  }
}

resource "aws_iam_role" "tenant_bedrock_access" {

  name = "cara-iam-role-${var.tenant_id}"

  assume_role_policy = jsonencode({

    Version = "2012-10-17"

    Statement = [

      {

        Action = "sts:AssumeRole"

        Effect = "Allow"

        Principal = {

          Service = "ec2.amazonaws.com"

        }

      }

    ]

  })

}
```

By combining a multi-AZ architecture with Kubernetes Horizontal Pod Autoscaler (HPA), Cara automatically scales compute capacity during peak business periods, such as annual insurance renewal seasons, ensuring high availability and uninterrupted service.

---

## Measurable Business Results

The combination of Cara's domain-specific AI platform and AWS cloud infrastructure has produced significant operational improvements.

| Metric | Business Outcome |
|--------|------------------|
| Time Savings | Saves an average of **10 hours per user each week** by automating repetitive administrative tasks and providing context-aware knowledge retrieval. |
| Customer Onboarding | Large enterprise customers can be provisioned within hours, while customized workflows are operational within days. |
| Scalability | Supports thousands of concurrent users and large-scale insurance processing workloads across multiple organizations. |
| Customer Adoption | Trusted by hundreds of leading enterprise insurance agencies and brokerages throughout the United States. |

---

## Conclusion

Cara demonstrates how **domain-specific AI** can transform enterprise insurance operations when combined with the scalability and security of AWS.

By leveraging **Amazon EKS** for container orchestration and **Amazon Bedrock** for AI inference, Cara has built a secure, scalable, and highly specialized platform capable of addressing the complex requirements of the insurance industry.

Rather than replacing insurance professionals, Cara enables them to spend less time on repetitive administrative work and more time building relationships with clients and delivering high-value advisory services.

Source: <https://aws.amazon.com/blogs/machine-learning/how-cara-pioneers-domain-specific-ai-for-enterprise-insurance-brokerages-with-aws/>
