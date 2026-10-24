# aws-s3-vs-ec2-hosting
Comparing managed vs self-managed web hosting on AWS
AWS S3 vs EC2 Hosting Comparison

# AWS Hosting Architecture Comparison: S3 Static Hosting vs. EC2 Self-Managed Server

## Overview

This project evaluates two distinct approaches to web hosting on Amazon Web 
Services — a fully managed, serverless solution (Amazon S3) and a 
self-administered compute solution (Amazon EC2) — to demonstrate practical 
understanding of cloud infrastructure, identity and access management, and 
network security configuration.

## Objective

To implement, secure, and compare two production-style hosting patterns, 
applying least-privilege access control and secure network configuration 
to each.

## Implementation

## Screenshots

**S3 Static Website Live**
![S3 website live](./screenshots/Screenshot%202026-10-04%20212535.png)

**EC2 Web Server Live**
![EC2 website live](./screenshots/Screenshot%202026-10-04%20212527.png)

**EC2 Instance Running (Status Checks Passed)**
![EC2 instance running](./screenshots/Screenshot%202026-10-04%20212546.png)

### Solution 1: Amazon S3 Static Website Hosting

- Provisioned a private-by-default S3 bucket
- Enabled static website hosting with a defined index document
- Authored and applied a least-privilege bucket policy, restricting public 
  access to the `s3:GetObject` action on a single, named resource
- Validated public accessibility while confirming no excess permissions 
  were granted

### Solution 2: Amazon EC2 Self-Managed Web Server

- Established a dedicated IAM administrator user, separate from the root 
  account, prior to resource provisioning — in accordance with AWS security 
  best practices
- Provisioned a t3.micro EC2 instance (Amazon Linux 2023)
- Designed a security group enforcing least-privilege network access:
  - SSH (port 22) restricted to authorized source IPs
  - HTTP (port 80) open to public traffic, consistent with the resource's 
    intended function
- Connected to the instance via EC2 Instance Connect; installed, configured, 
  and enabled the Apache HTTP Server (`httpd`)
- Deployed a static page served directly from the provisioned instance

## Technical Problem Resolution

During implementation, SSH connectivity via EC2 Instance Connect failed 
despite a correctly scoped "My IP" security group rule. Root-cause analysis 
identified that AWS's browser-based EC2 Instance Connect service initiates 
connections from AWS-owned IP ranges, not the end user's local IP address. 
The security group was subsequently updated to accommodate this distinction, 
restoring connectivity while maintaining an auditable access boundary.

## Core Competencies Demonstrated

- Identity and Access Management (IAM) — least-privilege principle, 
  separation from root account usage
- AWS S3 configuration and bucket policy authorship (JSON)
- EC2 provisioning and Linux system administration
- Security group design and network access control
- Independent troubleshooting of AWS service-level networking behavior

## Architecture Summary


