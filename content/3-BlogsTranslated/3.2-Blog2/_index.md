---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

{}

# Cara Pioneers Domain-Specific AI for Enterprise Insurance Brokerages with AWS

The global insurance industry is valued at $8 trillion and is heavily burdened by manual processes and a growing talent shortage. **Cara**, an AI-native solution built on AWS, is transforming how insurance brokerages operate by automating complex back-office workflows.

This blog explores Cara’s journey in building a domain-specific AI platform for the insurance brokerage industry, its technical architecture, and the business impact it delivers.

---

## The Challenge in Insurance Brokerage

Insurance agents spend countless hours on repetitive tasks such as:
- Completing insurance applications
- Analyzing and comparing policy coverages
- Re-keying data across multiple systems
- Coordinating information between clients and carriers

With a persistent talent shortage, brokerages need to scale revenue without proportionally increasing headcount. Generic AI tools fall short in this highly regulated industry, where precision, auditability, compliance, and handling of sensitive data (PII, financial records, and underwriting details) are non-negotiable.

---

## Cara’s Origin Story

Cara’s founders — Vic Yeh, Nikhil Kansal, and Jon Patel — previously built and successfully sold a digital insurance brokerage to The McGowan Companies. During that journey, they developed an internal AI copilot powered by large language models (LLMs). The tool significantly reduced turnaround times, improved accuracy, and streamlined agent workflows. Encouraged by its success, they turned the concept into a standalone product: **Cara**.

---

## Solution Architecture on AWS

Cara was designed with a strong focus on **security, scalability, and regulatory compliance**. Its architecture includes the following key components:

### 1. Compute and Orchestration
- Powered by **Amazon Elastic Kubernetes Service (Amazon EKS)** for container orchestration across multiple Availability Zones.
- Supports elastic scaling to handle peak periods such as policy renewals.
- Each customer (tenant) runs in isolated namespaces for strong data separation.

### 2. AI and Inference Layer
- Uses **Amazon Bedrock** to access foundation models through a fully managed API — eliminating the need to manage GPU infrastructure.
- Key AI capabilities include:
  - Coverage and quote intelligence (comparing carrier quotes and highlighting gaps)
  - Automated form filling for ACORD and supplemental forms
  - Generation of branded proposals and renewal documents
  - Knowledge-driven workflows referencing agency guidelines, carrier appetites, and historical data

### 3. Security and Data Isolation
- Account-level isolation for each brokerage
- Complete data and workload separation
- Encryption at rest and in transit
- Integration with AWS Identity and Access Management (IAM)

### 4. System Integrations
Cara seamlessly integrates with leading Agency Management Systems (AMS) and CRM platforms, reducing duplicate data entry.

> *Figure 1. High-level architecture of Cara on AWS.*

---

## Business Outcomes

Cara has delivered impressive measurable results for enterprise insurance brokerages:

| Metric                        | Result |
|-------------------------------|--------|
| Time saved per user           | ~10 hours per week |
| Onboarding speed              | Brokerages onboarded in hours, custom workflows live in days |
| Concurrent capacity           | Thousands of concurrent users and workflows |
| Adoption                      | Used by hundreds of leading insurance agencies and brokerages |

These outcomes are driven by deep domain-specific automation and contextual knowledge retrieval tailored to each organization.

---

## Looking Forward

The insurance industry is still in the early stages of AI adoption. Cara continues to expand its intelligent workflows across sales, servicing, and operations.

> “We are thrilled to push the boundaries of domain-specific AI in real-world insurance use cases with AWS,” says Vic Yeh, CEO of Cara. “Our goal is to help insurance professionals return to the core of our industry — building relationships.”

---

## Conclusion

Cara demonstrates the power of combining domain expertise with cloud-native AI services. By leveraging **Amazon EKS** for orchestration and **Amazon Bedrock** for inference, Cara has built a secure, scalable, and highly effective AI platform tailored for enterprise insurance brokerages.

This solution not only reduces operational costs and manual effort but also allows insurance professionals to focus on what matters most: client relationships.

To learn more about Cara, visit [www.getcara.ai](https://www.getcara.ai/). Organizations interested in building AI-powered applications on AWS can get started with Amazon Bedrock and Amazon EKS.

---