# AWS EKS Project

This project implements a web application using a microservices architecture deployed on Amazon EKS (Elastic Kubernetes Service). The infrastructure is managed using Infrastructure as Code (IaC) with Terraform, ensuring reproducible and scalable deployments.

## Project Overview

This web application is designed to provide a robust e-commerce platform with the following key features:

### Business Features
- Product catalog browsing and management
- Order processing and accounting
- Real-time inventory updates
- Scalable and resilient architecture

### Technical Implementation
The application is built using a microservices architecture, with each service handling specific business capabilities:

1. **Product Catalog Service (Go)**
   - Manages product inventory and catalog
   - Provides product search and filtering capabilities
   - Handles product metadata and pricing information
   - Uses gRPC for efficient service-to-service communication
   - Stores product data in a scalable database

2. **Accounting Service (.NET Core)**
   - Processes orders and financial transactions
   - Handles payment processing and reconciliation
   - Manages customer billing information
   - Implements event-driven architecture using message queues
   - Provides audit logging for financial transactions

3. **Frontend Proxy**
   - Acts as an API Gateway
   - Handles request routing and load balancing
   - Implements security and authentication
   - Manages cross-origin resource sharing (CORS)
   - Provides API rate limiting and monitoring

### Infrastructure Design
The application is deployed on AWS EKS, providing:
- High availability across multiple availability zones
- Auto-scaling capabilities based on demand
- Container orchestration with Kubernetes
- Secure network isolation using AWS VPC
- Load balancing and traffic management

### Architecture Components

1. **Infrastructure (Terraform)**
   - VPC Module: Network infrastructure
   - EKS Module: Kubernetes cluster management
   - Backend configuration for state management

2. **Kubernetes Resources**
   - Service deployments
   - Ingress configurations
   - Service accounts
   - Load balancer services

3. **Microservices**
   - **Accounting Service**
     - Built with .NET Core
     - Message consumer implementation
     - Logging functionality
     - Containerized deployment
   
   - **Product Catalog Service**
     - Built with Go
     - gRPC implementation
     - Product management
     - Containerized deployment

## Prerequisites

- AWS CLI configured with appropriate credentials
- Terraform installed
- kubectl installed
- Docker installed
- .NET Core SDK
- Go development environment

## Project Structure

```
.
├── docker-compose.yaml          # Local development container orchestration
├── main.tf                     # Main Terraform configuration
├── output.tf                   # Terraform outputs
├── variables.tf                # Terraform variables
├── backend/                    # Backend state configuration
├── kubernetes/                 # Kubernetes manifests
│   ├── complete-deploy.yaml
│   ├── service-account.yaml
│   ├── frontendproxy/
│   └── productcatalog/
├── modules/                    # Terraform modules
│   ├── eks/                   # EKS cluster configuration
│   └── vpc/                   # Network configuration
└── src/                       # Application source code
    ├── accounting/           # .NET Core accounting service
    └── product-catalog/      # Go product catalog service
```

## Getting Started

1. **Initialize Terraform**
   ```bash
   terraform init
   ```

2. **Plan Terraform Changes**
   ```bash
   terraform plan
   ```

3. **Apply Infrastructure**
   ```bash
   terraform apply
   ```

4. **Configure kubectl**
   ```bash
   aws eks update-kubeconfig --name <cluster-name> --region <region>
   ```

5. **Deploy Applications**
   ```bash
   kubectl apply -f kubernetes/complete-deploy.yaml
   ```

## Local Development

Use Docker Compose for local development:
```bash
docker-compose up
```

## Service Details

### Accounting Service
- Location: `src/accounting/`
- Framework: .NET Core
- Features:
  - Message consumption
  - Logging
  - Docker containerization

### Product Catalog Service
- Location: `src/product-catalog/`
- Language: Go
- Features:
  - gRPC implementation
  - Product management
  - Docker containerization

## Infrastructure Details

### VPC Module
- Private and public subnets
- NAT gateways
- Internet gateway
- Route tables

### EKS Module
- Managed node groups
- IAM roles and policies
- Security groups
- Cluster configuration

## Deployment

The project uses a combination of Terraform for infrastructure provisioning and Kubernetes manifests for application deployment.

### Infrastructure Deployment
1. Configure AWS credentials
2. Initialize and apply Terraform configurations
3. Configure kubectl for cluster access

### Application Deployment
1. Build Docker images
2. Push to container registry
3. Apply Kubernetes manifests

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit changes
4. Push to the branch
5. Create a Pull Request

## Release Notes

See [CHANGELOG.md](CHANGELOG.md) for detailed release notes.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
