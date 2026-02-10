# AWS Multi-Region Cloud Architecture Project

**End-to-end, production-style AWS architecture built across multiple labs using Terraform**

## Overview

This repository represents a **single cohesive cloud architecture project** developed through multiple labs that progressively build on one another. Each lab introduces additional layers of **security, scalability, global access, and regulatory compliance**, resulting in a realistic, enterprise-style AWS deployment.

Rather than isolated exercises, the labs together form a **unified system** that mirrors how real-world cloud platforms evolve over time—from foundational infrastructure to edge optimization and finally to multi-region, compliance-driven design.

---

## High-Level Architecture

![AWS Multi-Region Architecture Diagram](Lab%201/Lab%201a/screenshots/Armageddon-Class7-Diagram.jpeg)

At a high level, the project implements:

* A **private, security-first AWS environment** with no public SSH or hard-coded secrets
* A **global edge layer** using CloudFront and WAF
* A **multi-region architecture** designed around data residency and regulatory constraints
* **Infrastructure as Code (Terraform)** for repeatability and auditability

Traffic flows through a **single global entry point**, while data placement and compute responsibilities vary by region based on compliance requirements.

---

## Lab Breakdown

### Lab 1 — Core Infrastructure & Operations

**Goal:** Establish a secure, private, production-ready AWS foundation.

Key capabilities introduced:

* EC2 application tier integrated with RDS MySQL
* IAM roles with least privilege (no embedded credentials)
* AWS Secrets Manager and SSM Parameter Store for secret management
* Private subnets only, with VPC endpoints for AWS services
* Access via SSM Session Manager instead of SSH
* CloudWatch logging, metrics, alarms, and dashboards
* Application Load Balancer with TLS via ACM

This lab focuses on **baseline security, operational visibility, and correctness**—the foundation required before scaling outward.

---

### Lab 2 — Edge Security & Performance Optimization

**Goal:** Introduce a global edge layer to improve performance and security.

Enhancements added:

* CloudFront as the single public ingress point
* Origin cloaking to prevent direct access to the ALB
* AWS WAF deployed at the edge with managed rule sets
* Cache behaviors for static and dynamic content
* Custom security headers for origin validation

This lab shifts the architecture toward **internet-scale readiness**, protecting the origin while reducing latency for global users.

---

### Lab 3 — Multi-Region & Compliance Architecture

**Goal:** Extend the platform across regions while enforcing data residency rules.

Design highlights:

* Primary region: **Tokyo (ap-northeast-1)**
* Secondary region: **São Paulo (sa-east-1)**
* APPI-aligned data residency model

  * Regulated data stored only in Japan
  * Secondary region operates as stateless compute
* Secure inter-region networking using Transit Gateway
* Global DNS and routing with Route 53 and CloudFront
* Single global URL serving users across regions

This lab demonstrates how **legal and regulatory constraints directly influence cloud architecture decisions**.

---

## Security & Compliance Principles

The project was designed with a defense-in-depth mindset:

* No public SSH or database exposure
* IAM roles and policies scoped to least privilege
* Secrets stored and rotated using AWS-managed services
* Private networking with VPC endpoints
* WAF protection at both regional and edge layers
* TLS encryption using ACM-managed certificates
* Explicit enforcement of data residency boundaries

---

## Operational Excellence

Operational readiness is treated as a first-class concern:

* All infrastructure provisioned with Terraform
* Centralized logging and metrics via CloudWatch
* Alarms for failure and performance thresholds
* Backup and recovery mechanisms for stateful services
* Architecture designed to tolerate regional failure scenarios

---

## Technologies Used

* **Compute**: EC2, Auto Scaling, Application Load Balancer
* **Database**: RDS MySQL
* **Networking**: VPC, Transit Gateway, CloudFront, Route 53
* **Security**: IAM, Secrets Manager, WAF, KMS, Security Groups
* **Operations**: Systems Manager, CloudWatch, SNS
* **Infrastructure as Code**: Terraform
* **Compliance Focus**: APPI-aligned architectural controls

---

## Verification & Validation

The environment was validated using AWS CLI and service-level inspection to confirm:

* Secure service-to-service connectivity
* Correct IAM permissions and role usage
* Functional cross-region networking
* Enforcement of private access patterns
* Resilience during simulated failure conditions

---

## Learning Outcomes

By completing this project, the following skills are demonstrated:

1. Designing production-grade AWS architectures
2. Translating compliance requirements into technical controls
3. Building and securing global, multi-region systems
4. Applying Infrastructure as Code for complex environments
5. Operating cloud platforms with a security-first mindset

---

> 📌 This repository is intended as a **portfolio-grade architecture project**, reflecting real-world cloud design tradeoffs rather than a simplified tutorial.
