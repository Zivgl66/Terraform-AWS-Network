# Terraform AWS Network

## Overview
This repository contains Terraform scripts for creating and managing network infrastructure on AWS, including the setup of an EKS (Elastic Kubernetes Service) cluster. The primary purpose of this project is to automate the provisioning of networking resources such as VPCs, subnets, route tables, security groups, and Kubernetes infrastructure, providing a scalable, secure, and highly available environment.

## Table of Contents
1. [Features](#features)
2. [Prerequisites](#prerequisites)
3. [Getting Started](#getting-started)
4. [Usage](#usage)
5. [Project Structure](#project-structure)
6. [EKS Provisioning](#eks-provisioning)
7. [Best Practices](#best-practices)
8. [Contributing](#contributing)
9. [License](#license)

## Features
- **VPC Creation:** Define and create custom VPCs for isolating network environments.
- **Subnet Configuration:** Set up public and private subnets across multiple availability zones for high availability.
- **Routing:** Configure route tables and routing policies to control traffic flow.
- **Security Groups:** Define security groups for managing inbound and outbound traffic to resources.
- **NAT Gateways:** Set up NAT gateways for enabling internet access for private instances.
- **Elastic IPs:** Associate Elastic IPs for internet-facing resources.
- **Internet Gateways:** Deploy internet gateways for VPCs to allow external traffic.
- **EKS Cluster:** Automate the provisioning of EKS clusters, including worker nodes, to manage containerized applications at scale.

## Prerequisites
- [Terraform](https://www.terraform.io/downloads.html) (version 0.12+ recommended)
- AWS account with the necessary IAM permissions for creating network and EKS resources.
- AWS CLI configured with access and secret keys.
- Basic understanding of AWS networking concepts (VPC, subnets, security groups, etc.).
- Basic knowledge of Kubernetes and EKS.

## Getting Started

1. **Clone the Repository:**
    ```bash
    git clone https://github.com/Zivgl66/Terraform-AWS-Network.git
    cd Terraform-AWS-Network
    ```

2. **Initialize Terraform:**
    Run the following command to initialize the Terraform environment. This will download the required providers.
    ```bash
    terraform init
    ```

3. **Modify Variables:**
    Update the `variables.tf` file or create a `terraform.tfvars` file with your desired values. Here are some of the key variables you might want to set:
    - `region`: The AWS region where resources will be created.
    - `vpc_cidr`: CIDR block for the VPC.
    - `public_subnet_cidrs`: List of CIDR blocks for public subnets.
    - `private_subnet_cidrs`: List of CIDR blocks for private subnets.
    - `eks_cluster_name`: Name of the EKS cluster to be created.
    - `eks_node_instance_type`: Instance type for EKS worker nodes.
    - `eks_node_group_size`: Number of worker nodes in the EKS cluster.

4. **Plan the Infrastructure:**
    Generate and review an execution plan for your infrastructure.
    ```bash
    terraform plan
    ```

5. **Apply Changes:**
    Apply the changes to create the network infrastructure and EKS cluster.
    ```bash
    terraform apply
    ```

6. **Destroy Resources:**
    If you need to tear down the infrastructure, use:
    ```bash
    terraform destroy
    ```

## Project Structure

```plaintext
/
├── main.tf                   # Main configuration file for setting up the network and EKS
├── variables.tf              # Input variables definition
├── outputs.tf                # Outputs from the Terraform configuration
├── providers.tf              # Provider configuration (AWS)
├── eks/                      # Directory containing EKS-related Terraform configurations
│   ├── eks-cluster.tf        # EKS cluster and node group configurations
│   ├── eks-security-groups.tf # Security groups specific to EKS
│   └── eks-outputs.tf        # EKS related outputs
├── README.md                 # Project documentation
├── terraform.tfvars          # File for setting user-specific variable values (not version controlled)
└── modules/                  # Reusable Terraform modules (if applicable)
    ├── vpc/                  # Module for VPC creation
    ├── subnets/              # Module for subnets creation
    └── security-groups/      # Module for security groups
```

## EKS Provisioning
The Terraform configuration includes modules and resources for provisioning an EKS cluster on AWS. This setup allows you to deploy and manage Kubernetes clusters easily, providing scalability and high availability for containerized applications.

### EKS Cluster Setup
- **Cluster Creation:** Defines an EKS cluster with the specified name and version.
- **Node Groups:** Automatically provisions and scales worker nodes using AWS Auto Scaling groups.
- **IAM Roles:** Configures the necessary IAM roles and policies for EKS to interact with other AWS services securely.
- **Security Groups:** Sets up security groups to control access to the EKS cluster and nodes.
- **Kubeconfig:** Generates a kubeconfig file for authenticating and managing the EKS cluster using kubectl.

### Accessing the EKS Cluster
After provisioning, use the generated kubeconfig to access the EKS cluster:
```bash
aws eks --region <region-name> update-kubeconfig --name <eks-cluster-name>
kubectl get nodes
```

## Best Practices
- Use version control for managing changes to your Terraform code.
- Regularly review and update security group rules to ensure minimal exposure.
- Use `terraform plan` before applying changes to review potential modifications.
- Maintain backups of your state file and use remote state management for collaboration.
- Regularly update your EKS cluster to the latest supported Kubernetes version for security and new features.

## Contributing
Contributions are welcome! Please fork the repository, make your changes, and submit a pull request. Ensure that your code adheres to the repository's coding standards and includes appropriate documentation.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
```

### Notes:
- Replace `<region-name>` and `<eks-cluster-name>` with actual values.
- Ensure the directory structure matches what's described. Adjust any file names or paths as necessary.
- Update the `features`, `prerequisites`, and other relevant sections if there are specific requirements or configurations unique to your EKS setup.
