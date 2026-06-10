---
title: "Week 2 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---



### Objectives for this week:

* **Knowledge Objectives:**
  * Gain a thorough understanding of identity and access management, permission boundaries, and advanced account security practices using **AWS IAM**.
  * Comprehend the technical support scopes and Service Level Agreements (SLA) across different **AWS Support** tiers.
  * Master the architecture of **VPC (Virtual Private Cloud)**, including subnet partitioning, traffic routing principles, and network security layers.
  * Deepen theoretical knowledge regarding **Amazon EC2** virtual server families, resource allocation, and persistent storage mechanics with **Amazon EBS**.

* **Practical Skills:**
  * Successfully implement fine-grained IAM Policies for user groups and demonstrate secure cross-account/cross-role assumption (AssumeRole).
  * Provision EC2 compute instances, allocate static public IPs (Elastic IPs), and maintain secure remote management via cryptographic SSH keys.
  * Deploy advanced cloud network routing: provision network address translation via **NAT Gateways**, establish encrypted **Site-to-Site VPN** tunnels, and set up isolated administration access using **EC2 Instance Connect Endpoints**.

### Tasks to be carried out this week:

#### WEEK 2 (From 24/04/2026 to 30/04/2026)

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - Learn about **AWS Support**: Analyze tier levels (Developer, Business, Enterprise) based on business cases <br> - Research supported request types, tier switching processes, and AWS response times (SLA) | 24/04/2026 | 24/04/2026 | <https://000009.awsstudygroup.com/> |
| 3 | - Study fine-grained resource access control using **AWS IAM** <br> - Research core concepts: Users, Groups, Policies, and Roles <br> - **Practice:** Implement account security, create IAM Groups, attach IAM Policies for access management, manage IAM Users, and configure secure IAM Role assumption | 25/04/2026 | 26/04/2026 | <https://000002.awsstudygroup.com/> |
| 4 | - Research the architectural design and deployment of a **VPC (Virtual Private Cloud)** following *AWS Well-Architected Framework* standards <br> - Configure network security components and establish secure connectivity between on-premises environments and the AWS cloud | 27/04/2026 | 27/04/2026 | <https://000003.awsstudygroup.com/> |
| 5 | - Explore **Amazon EC2** cloud compute services: Instance types, AMIs, and EBS volumes <br> - **Practice:** Launch an EC2 compute instance, attach an additional EBS storage volume, and establish a secure SSH connection | 28/04/2026 | 29/04/2026 | <https://000024.awsstudygroup.com/> |
| 6 | - **Advanced Network Infrastructure Practice:** <br>&emsp; + Create and configure a NAT Gateway <br>&emsp; + Use an EC2 Instance Connect Endpoint to securely access servers within private subnets <br>&emsp; + Configure a Site-to-Site VPN tunnel connection and establish VPC firewalls <br> - Review progress, evaluate outcomes, and wrap up the Week 2 internship report | 30/04/2026 | 30/04/2026 | <https://000003.awsstudygroup.com/> |

---

### Week 2 Achievements:
* Distinguished scope of support and Service Level Agreements (SLA) across different AWS Support tiers (Developer, Business, Enterprise).
* Gained proficiency in **AWS IAM** management: Implemented the Principle of Least Privilege, created groups, attached permissions via policies, and verified role assumptions (AssumeRole).
* Acquired an in-depth understanding of **VPC** network topologies, separating public/private subnets, and managing traffic flow via Route Tables and Internet Gateways.
* Provisioned and managed **Amazon EC2** instances, bound persistent storage with EBS volumes, assigned Elastic IPs, and maintained secure shell access via Key Pairs.
* Successfully deployed advanced secure network routing: Configured Network Address Translation via NAT Gateways, established encrypted Site-to-Site VPN tunnels, and restricted threat vectors using Security Groups and Network ACLs.