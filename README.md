# ADDA – End-to-End DevOps Portfolio Project

<p align="center">
  <strong>Automating, Deploying, Monitoring and Managing a Portfolio Application</strong>
</p>

## Project Overview

ADDA is an end-to-end DevOps project that demonstrates how a web application can be containerized, deployed, managed, monitored, and maintained using modern DevOps tools and practices.

The project uses a portfolio web application as its practical implementation. It brings together Docker, Kubernetes, AWS EC2, Terraform, Ansible, GitHub Actions, Grafana Cloud, and the ELK Stack.

The main objective is to understand the complete DevOps workflow through practical implementation rather than only theoretical concepts.

## Live Application

- **Live Portfolio:** https://maneeshareddy.duckdns.org
- **Application Source Code:** [Portfolio Simple – GitHub](https://github.com/ManeeshaVeeramreddy/portfolio-simple)
- **DevOps Repository:** [ADDA – GitHub](https://github.com/ManeeshaVeeramreddy/adda)

## Project Architecture

```text
             Developer
                 |
                 v
           GitHub Repository
                 |
                 v
          Docker Container
                 |
                 v
             Docker Hub
                 |
                 v
          AWS EC2 – Ubuntu
                 |
          +------+------+
          |             |
          v             v
       Caddy         Portfolio
       HTTPS         Container
          |
          v
     Live Website

  Infrastructure Inspection
          |
       Terraform

  Configuration and Deployment
          |
        Ansible

  Local Container Orchestration
          |
      Kubernetes
       (Minikube)

  CI Validation
          |
     GitHub Actions

  Website Availability
          |
     Grafana Cloud
  Synthetic Monitoring

  Application Logs
          |
       Filebeat
          |
    Elasticsearch
          |
       Kibana
```

## Technologies and Tools

| Technology | Purpose |
|---|---|
| Git and GitHub | Version control and source management |
| Docker | Containerization of the portfolio application |
| Docker Hub | Container image storage |
| AWS EC2 | Cloud hosting |
| Ubuntu | Server operating system |
| Caddy | HTTPS and reverse proxy |
| Kubernetes | Container orchestration using Minikube |
| Terraform | Infrastructure inspection using AWS data sources |
| Ansible | Server configuration and deployment automation |
| GitHub Actions | Automated Terraform validation |
| Grafana Cloud | Website availability monitoring |
| Filebeat | Application log collection |
| Elasticsearch | Log storage and indexing |
| Kibana | Log searching and visualization |

## Implementation Details

### 1. Version Control – Git and GitHub

- Maintained project files using Git.
- Used GitHub repositories for source code and DevOps configurations.
- Organized the project into separate directories for different DevOps tools.

### 2. Docker – Application Containerization

- Created a Docker image using the Nginx Alpine base image.
- Copied portfolio application files into the Nginx web directory.
- Exposed port 80 for HTTP traffic.
- Built and pushed the Docker image to Docker Hub.

**Docker Hub Image:** `maneesha0805/portfolio:v1`

### 3. AWS EC2 – Cloud Deployment

- Deployed the portfolio application on an existing AWS EC2 instance.
- Used Ubuntu as the server operating system.
- Ran the application inside a Docker container.
- Configured Caddy as a reverse proxy with HTTPS.
- Made the application accessible through a public domain.

### 4. Kubernetes – Container Orchestration

- Installed and configured Minikube.
- Created Kubernetes Deployment and Service manifests.
- Deployed the portfolio Docker image inside a Kubernetes pod.
- Exposed the application using a NodePort service.
- Verified the deployment and service using `kubectl`.

**Kubernetes environment:** Local Minikube cluster.

### 5. Terraform – Infrastructure as Code

- Configured the AWS provider.
- Used an AWS EC2 data source to inspect an existing instance.
- Retrieved instance details such as instance ID, type, public IP, and state.
- Executed Terraform initialization, validation, planning, and application.

**Important:** This Terraform configuration reads information about an existing EC2 instance. It does not create, modify, or destroy AWS infrastructure.

### 6. Ansible – Configuration Management and Automation

Created Ansible playbooks to automate and verify server operations.

Implemented playbooks:

- `first-playbook.yml` – Checks the local Ansible controller.
- `check-services.yml` – Checks Docker and Caddy service status locally.
- `deploy-portfolio.yml` – Pulls the Docker image and ensures the portfolio container is running on AWS EC2.
- `portfolio-health-check.yml` – Generates a local Docker and Caddy service health report.

Used SSH connectivity to communicate with the AWS EC2 instance.

### 7. GitHub Actions – Continuous Integration

Created a GitHub Actions workflow to validate Terraform configuration.

The workflow performs:

- Repository checkout.
- Terraform setup.
- Terraform initialization.
- Terraform formatting verification.
- Terraform configuration validation.

The workflow executes automatically on pushes and pull requests targeting the main branch.

### 8. Grafana Cloud – Synthetic Monitoring

Implemented website availability monitoring using Grafana Cloud Synthetic Monitoring.

Configuration:

- Check type: API / HTTP
- HTTP method: GET
- Target: Portfolio website
- Check frequency: Every minute

The dashboard displays uptime, reachability, and response-time information.

The monitoring screenshot is available in the `monitoring/screenshots/` directory.

### 9. ELK Stack – Centralized Logging

Implemented application log collection and visualization using:

- **Filebeat:** Collects portfolio Docker container logs.
- **Elasticsearch:** Stores and indexes collected logs.
- **Kibana:** Provides a graphical interface for searching and analyzing logs.

Logging workflow:

`Portfolio Docker Container → Filebeat → Elasticsearch → Kibana`

Created a Kibana data view named `Portfolio Logs` to explore the indexed application logs.

## Repository Structure

```text
adda/
│
├── .github/
│   └── workflows/
│       └── terraform-check.yml
│
├── ansible/
│   ├── README.md
│   ├── first-playbook.yml
│   ├── check-services.yml
│   ├── deploy-portfolio.yml
│   └── portfolio-health-check.yml
│
├── docker/
│   └── README.md
│
├── kubernetes/
│   ├── README.md
│   ├── deployment.yaml
│   └── service.yaml
│
├── terraform/
│   ├── README.md
│   ├── provider.tf
│   └── main.tf
│
├── monitoring/
│   ├── README.md
│   └── screenshots/
│
├── logging/
│   ├── README.md
│   └── kibana-portfolio-logs.png
│
└── README.md
```

## Key Learning Outcomes

Through this project, I gained practical experience in:

- Version control and repository management.
- Containerizing web applications using Docker.
- Publishing container images to Docker Hub.
- Deploying applications on AWS EC2.
- Configuring HTTPS using Caddy.
- Deploying containers using Kubernetes.
- Inspecting cloud infrastructure using Terraform.
- Automating deployment and server checks using Ansible.
- Implementing CI validation using GitHub Actions.
- Monitoring website availability using Grafana Cloud.
- Collecting and analyzing application logs using the ELK Stack.

## Security Practices

- Excluded Terraform state files and variable files from Git.
- Kept SSH private keys outside the repository.
- Excluded Ansible inventory files containing server connection details.
- Avoided committing credentials and environment secrets.

## Author

**Maneesha Veeramreddy**

---

<p align="center">
  <strong>Learning DevOps Through Practical Implementation</strong>
</p>
