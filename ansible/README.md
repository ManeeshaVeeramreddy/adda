# Ansible – Portfolio Server Configuration and Deployment

## 1. Introduction

Ansible is an open-source automation tool used to configure servers, manage services, install dependencies, and deploy applications.

In this project, Ansible automates the deployment and basic service checks of a portfolio website. VMware Ubuntu acts as the Ansible controller, while an existing AWS EC2 Ubuntu instance acts as the managed node.

The portfolio application is packaged as a Docker container and deployed using Ansible.

## 2. Project Architecture

| Component | Configuration |
|---|---|
| Ansible Controller | VMware Ubuntu |
| Managed Node | AWS EC2 Ubuntu |
| Communication | SSH |
| Container Platform | Docker |
| Docker Image | `maneesha0805/portfolio:v1` |
| Container Name | `my-portfolio` |
| Container Port Mapping | `127.0.0.1:8080:80` |
| Reverse Proxy | Caddy |
| HTTPS | DuckDNS domain with Caddy |

### Deployment Workflow

1. Ansible runs on VMware Ubuntu.
2. It connects to the AWS EC2 instance through SSH.
3. It checks the Docker installation on EC2.
4. It pulls the portfolio image from Docker Hub.
5. It ensures that the portfolio container is running.
6. Caddy forwards web requests to the container and provides HTTPS access.

## 3. Installation and Configuration

### Install Ansible

On the VMware Ubuntu controller:

```bash
sudo apt update
sudo apt install ansible -y
```

Verify:

```bash
ansible --version
```

### Install the Docker Collection

```bash
ansible-galaxy collection install community.docker
```

### Configure SSH Access

The EC2 private key is stored securely on the controller.

Set its permissions:

```bash
chmod 400 ~/.ssh/portfolio.pem
```

Test SSH access:

```bash
ssh -i ~/.ssh/portfolio.pem ubuntu@EC2_PUBLIC_IP
```

Replace `EC2_PUBLIC_IP` with the current EC2 public IP.

## 4. Ansible Inventory

The inventory identifies the remote machines managed by Ansible.

Example `inventory.ini`:

```ini
[portfolio]
aws-portfolio ansible_host=EC2_PUBLIC_IP ansible_user=ubuntu ansible_ssh_private_key_file=/home/USERNAME/.ssh/portfolio.pem
```

The actual inventory file is kept locally and excluded from GitHub because it contains environment-specific connection information.

Test connectivity from the project root:

```bash
ansible -i ansible/inventory.ini portfolio -m ping
```

Expected result:

```text
"ping": "pong"
```

## 5. Playbooks Implemented

### 5.1 first-playbook.yml

This introductory playbook runs locally on the controller.

- Displays a success message.
- Collects operating system information.
- Demonstrates Ansible facts and the debug module.

Execute:

```bash
ansible-playbook ansible/first-playbook.yml
```

### 5.2 check-services.yml

This playbook checks local services on the VMware Ubuntu controller.

- Checks Docker service status.
- Checks Caddy service status.
- Displays both service results.

Execute:

```bash
ansible-playbook ansible/check-services.yml
```

### 5.3 portfolio-health-check.yml

This playbook produces a combined local service health report.

- Checks Docker.
- Checks Caddy.
- Displays both statuses together.

Execute:

```bash
ansible-playbook ansible/portfolio-health-check.yml
```

### 5.4 deploy-portfolio.yml

This is the main remote deployment playbook.

It connects to the AWS EC2 instance using the `portfolio` inventory group.

Tasks performed:

1. Checks Docker installation on EC2.
2. Displays the installed Docker version.
3. Pulls `maneesha0805/portfolio:v1` from Docker Hub.
4. Ensures that the `my-portfolio` container is running.
5. Configures the container to restart automatically unless stopped.
6. Publishes the container on `127.0.0.1:8080`, forwarding to container port 80.

Execute:

```bash
ansible-playbook -i ansible/inventory.ini ansible/deploy-portfolio.yml
```

## 6. Dependencies

The following components are required:

- Ansible on VMware Ubuntu.
- SSH connectivity to AWS EC2.
- Docker installed on EC2.
- Python Docker SDK on EC2.
- `community.docker` collection on the controller.

Install the Python Docker SDK on EC2 if required:

```bash
ansible -i ansible/inventory.ini portfolio -b -m apt -a "name=python3-docker state=present update_cache=yes"
```

## 7. Deployment Verification

Check the Docker container on EC2:

```bash
ansible -i ansible/inventory.ini portfolio -b -m command -a "docker ps"
```

Expected container details:

- Image: `maneesha0805/portfolio:v1`
- Name: `my-portfolio`
- Status: Running
- Port mapping: `127.0.0.1:8080->80/tcp`

The deployed portfolio is accessible through:

https://maneeshareddy.duckdns.org

## 8. Security Practices

- Never upload SSH private keys to GitHub.
- Keep the real inventory file out of version control.
- Store SSH keys securely on the controller.
- Use SSH for communication with EC2.
- Use Ansible privilege escalation (`become: true`) for administrative tasks.
- Never commit AWS credentials or passwords.

## 9. Result

Ansible was successfully used to connect from VMware Ubuntu to an existing AWS EC2 instance.

The deployment playbook checked Docker, pulled the portfolio Docker image, and ensured that the application container was running.

The tested deployment completed with zero failed and zero unreachable tasks.

This project demonstrates practical server automation, SSH-based remote management, Docker deployment, and basic service monitoring using Ansible.
