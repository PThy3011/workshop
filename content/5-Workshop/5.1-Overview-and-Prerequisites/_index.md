---
title: "Overview and Prerequisites"
date: 2026-04-18
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

### 1. Overview
In this Workshop, we will practice deploying a simple Numerology system called **LunaGenZ** to AWS.

The goal of this lab is to help you get familiar with deploying Infrastructure as Code (IaC) using the **Serverless Framework**. With this tool, creating complex resources like Lambda, API Gateway, DynamoDB, or S3 becomes incredibly simple and automated, and cleaning up (Clean-up) takes just one command.

### 2. Prerequisites
To get started, you need to prepare:
- **AWS Account:** Activated and configured with AWS CLI (run `aws configure`).
- **Development Environment:**
  - Install [Node.js](https://nodejs.org/en) (version 18 or 20).
  - Install **Serverless Framework** via command: `npm install -g serverless`
- **Source Code:**
  - The `LunaGenZ` sample project includes the backend (`be`) and frontend (`fe`) directories.
