# Virtual Private Cloud (VPC)

## What is a VPC?

A **private, isolated network within a public cloud provider's infrastructure** where you can define and control your virtual network environment e.g. IP address ranges, subnets, route tables and network gateways

(Like building a private data centre inside the cloud, but with the scalability and flexibility benefits that come with cloud computing)

![VPC Overview](./images/vpc_overview.png)

## How do VPCs help a business?

VPCs provide businesses with **full control over their cloud networking environment, enabling them to securely launch and manage resources** (like EC2 instances) in a private, isolated space that mirrors their on-premises network.

Some benefits include:
- **Enhanced Security and Isolation**: Allows control over their network boundaries. Can segregate environments within the same cloud account e.g. dev, staging, production
- **Customisable Network Architecture**: Can create private subnets for databases and public subnets for web servers
- **Cost Efficiency**: Only pay for resources that are used
- **Secure Connectivity to Other Networks**: VPC Peering allows secure communication between different VPCs supporting multi-team setups
- **Improved Agility and Speed**: Can experiment without affecting production environments encouraging faster innovation
- **Compliance and Governance**: Easier to audit, log and monitor network activity for compliance purposes

## How do VPCs help DevOps?

VPCs help DevOps by **providing secure, customisable, and isolated network environments that support automated infrastructure and smooth CI/CD workflows**. They enable safe testing, efficient scaling, and controlled access, all of which are essential for reliable and agile DevOps practices.

Some key points are:
- **Automation** - Fully scriptable network setup as VPC configurations can be defined as code using Terraform or AWS CloudFormation
- **Isolation** - Safe testing and deployment environments
- **Security** - Fine-grained access controls e.g. security groups
- **Scalability** - Auto-scaling and elastic networking
- **Observability** - VPC flow logs and integrated monitoring e.g. AWS CloudWatch
- **Deployment Speed** - Fast provisioning and tear-down of environments

## Why did Amazon Web Services (AWS) introduce VPCs?

AWS introduced Virtual Private Cloud (VPC) in August 2009 to **address growing customer demands for greater control, security, and customisation over their cloud-based infrastructure**. This was to bridge the gap between traditional on-prem networking and cloud, giving businesses the confidence and capability to adopt cloud infrastructure on their own terms.

## VPC Components

### Subnets 

A subnet is a **segment of a VPC’s IP address range where you can launch resources** like EC2 instances. It essentially divides your VPC into smaller networks, each typically aligned to a specific function e.g. web servers, databases
 
### Public vs Private Subnets

- **Public Subnets**: Connected to the internet via an Internet Gateway. Resources here can be accessed from the internet (if allowed by security settings).
- **Private Subnets**: No direct internet access. Usually used for sensitive resources like databases or internal services. Outbound access can be provided via a NAT Gateway/Instance.
 
### Classless Inter-Domain Routing (CIDR) Blocks

A CIDR block **defines the IP address range of a VPC or subnet**. It's written like this: 10.0.0.0/16, which means:
- IPs will range from 10.0.0.0 to 10.0.255.255 (about 65,536 IPs).
- The /16 is the subnet mask, defining how many bits are fixed for the network.

Examples:
- VPC: 10.0.0.0/16 (big block)
- Subnet 1: 10.0.1.0/24 (256 IPs)
- Subnet 2: 10.0.2.0/24
 
### Internet Gateways (IGW)

An Internet Gateway is a horizontally scaled, redundant component that **connects your VPC to the internet**.

- Required for public subnets to allow internet access.
- Must be attached to your VPC and referenced in the route table
 
### Route Tables

A route table **defines how traffic is directed within your VPC and outside it**.

- Each subnet must be associated with one route table.
- Routes tell traffic where to go — e.g. 0.0.0.0/0 to the internet gateway.
- Private subnets don’t have a route to an internet gateway (only to a NAT gateway, if needed).
 
### Security Groups (SG) and how SGs work on an INSTANCE level

A Security Group is a **virtual firewall that controls inbound and outbound traffic to/from EC2 instances**.

- **Attached at the instance level**, not at the subnet.
- **Stateful**: if you allow incoming traffic on port 22 (SSH), the response is automatically allowed back out.
- Rules are based on:
  - Protocol (e.g. TCP)
  - Port range (e.g. 80, 443)
  - Source/destination (e.g. 0.0.0.0/0 or another SG)

You can **assign multiple SGs to an instance and modify rules without restarting the instance**.
