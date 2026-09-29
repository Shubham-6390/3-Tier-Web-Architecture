# 3-Tier Web Application Architecture on AWS

A secure, scalable, and highly available three-tier web application architecture built using Amazon Web Services (AWS). This project demonstrates the implementation of a multi-AZ infrastructure with load balancing, Auto Scaling, private database deployment, network isolation, and controlled access between application layers.

## Project Overview

The architecture separates the application into three logical layers:

1. **Presentation Layer:** Handles incoming HTTP/HTTPS requests through an internet-facing Application Load Balancer.
2. **Application Layer:** Runs application workloads on EC2 instances distributed across multiple Availability Zones and managed through Auto Scaling Groups.
3. **Database Layer:** Uses Amazon RDS for MySQL in private subnets, allowing database access only from authorized application resources.

The infrastructure follows AWS security best practices by restricting direct access to backend resources and controlling communication through Security Groups and routing configurations.

## Architecture Diagram

![AWS 3-Tier Architecture](images/3-tier-architecture.png)

> Replace the image path with your actual Draw.io architecture diagram.

## AWS Services Used

| AWS Service               | Purpose                                                       |
| ------------------------- | ------------------------------------------------------------- |
| Amazon VPC                | Isolated networking environment                               |
| Public Subnets            | Host internet-facing load balancer and NAT Gateway            |
| Private Subnets           | Host application and database resources                       |
| Amazon EC2                | Compute resources for web and application tiers               |
| Application Load Balancer | Distributes incoming application traffic                      |
| Auto Scaling Groups       | Maintains and adjusts EC2 capacity                            |
| Amazon RDS (MySQL)        | Managed relational database                                   |
| NAT Gateway               | Provides outbound internet connectivity for private resources |
| Internet Gateway          | Enables internet connectivity for public resources            |
| Security Groups           | Controls inbound and outbound traffic                         |
| IAM Roles                 | Provides controlled permissions to AWS resources              |
| Amazon CloudWatch         | Monitors infrastructure metrics and logs                      |

## Architecture Components

### 1. Networking Layer

* Created a custom Amazon VPC.
* Configured public and private subnets across multiple Availability Zones.
* Attached an Internet Gateway to the VPC.
* Configured route tables for public and private network traffic.
* Used NAT Gateway for outbound internet access from private subnets.

### 2. Presentation Layer

* Deployed an internet-facing Application Load Balancer.
* Configured listeners to receive incoming traffic.
* Distributed requests to registered backend targets.
* Configured target group health checks.

### 3. Application Layer

* Deployed EC2 instances in private subnets.
* Configured Auto Scaling Groups for application availability and capacity management.
* Used Security Groups to restrict traffic to authorized sources.
* Enabled controlled outbound connectivity through NAT Gateway.

### 4. Database Layer

* Deployed Amazon RDS for MySQL in private subnets.
* Configured database access through restricted Security Group rules.
* Allowed database connections only from the authorized application tier.
* Avoided direct public internet access to the database.

## Security Implementation

The architecture uses a layered security approach:

* Public-facing traffic is handled through the internet-facing ALB.
* Application instances are isolated in private subnets.
* Database instances are isolated from direct public access.
* Security Groups restrict communication between tiers.
* IAM roles provide controlled access to AWS services.
* NAT Gateway enables outbound connectivity without exposing private instances to unsolicited inbound internet traffic.

## Request Flow

```text
Internet User
     |
     v
Internet Gateway
     |
     v
Internet-facing ALB
     |
     v
Web / Application EC2 Instances
     |
     v
Internal Application Load Balancer
     |
     v
Application Tier
     |
     v
Amazon RDS (MySQL)
```

## Key Features

* Three-tier architecture with logical separation of responsibilities.
* Multi-AZ infrastructure design.
* Load balancing for incoming application requests.
* Auto Scaling for application capacity management.
* Private database deployment.
* Controlled communication between application layers.
* Secure network segmentation.
* Infrastructure monitoring through CloudWatch.

## Deployment Workflow

1. Create the VPC and define the CIDR block.
2. Create public and private subnets across Availability Zones.
3. Attach the Internet Gateway.
4. Configure route tables and NAT Gateway.
5. Create Security Groups for each tier.
6. Deploy the Application Load Balancer and target groups.
7. Launch EC2 instances and configure Auto Scaling Groups.
8. Deploy Amazon RDS for MySQL in private subnets.
9. Configure connectivity between the application and database.
10. Validate application reachability, target health, and network access.

## Challenges & Troubleshooting

| Challenge                        | Troubleshooting Approach                                                              |
| -------------------------------- | ------------------------------------------------------------------------------------- |
| ALB target health check failure  | Checked application service, health check path, port, and Security Groups             |
| EC2 connectivity issues          | Verified route tables, subnet configuration, and access rules                         |
| Database connection failure      | Checked RDS endpoint, database port, and application-to-database Security Group rules |
| Private instance internet access | Verified NAT Gateway and private route table configuration                            |

## Learning Outcomes

Through this project, I gained practical understanding of:

* AWS VPC networking and subnet design.
* Public and private network segmentation.
* Application Load Balancer configuration.
* EC2 and Auto Scaling.
* Amazon RDS deployment.
* Security Group-based access control.
* High availability and scalable cloud architecture.
* Infrastructure troubleshooting.

## Future Improvements

* Automate infrastructure deployment using Terraform.
* Implement HTTPS using AWS Certificate Manager.
* Configure CloudWatch alarms and dashboards.
* Integrate CI/CD using Jenkins or GitHub Actions.
* Improve infrastructure security using AWS Systems Manager and centralized logging.

## Author

**Shubham Dharmendra Gupta**

B.E. Information Technology | AWS Certified Solutions Architect – Associate

* GitHub: [Shubham-6390](https://github.com/Shubham-6390)
* LinkedIn: [Shubham Gupta](https://linkedin.com/in/shubham-gupta-cloud)
* Portfolio: [Personal Portfolio](https://shubham-6390.github.io/Shubham-Portfolio)

---

*This project was developed for hands-on learning and demonstration of AWS cloud infrastructure, networking, security, and high availability concepts.*
