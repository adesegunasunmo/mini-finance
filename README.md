## Mini Finance App Deployment (Azure + Terraform + Ansible)

###  Project Overview
This project demonstrates a complete DevOps workflow for deploying a static web application (Mini Finance App) on Microsoft Azure using:

- **Terraform** for infrastructure provisioning  
- **Ansible** for configuration management and deployment  

The goal is to achieve a **repeatable, automated, and production-style deployment** with clear separation of concerns.

---

###  Architecture

- Azure Resource Group
- Virtual Network (10.0.0.0/16)
- Subnet (10.0.1.0/24)
- Network Security Group (NSG)
  - SSH (Port 22)
  - HTTP (Port 80)
- Ubuntu 22.04 Virtual Machine
- Public IP for external access

---

###  Tools & Technologies

- Terraform
- Ansible
- Microsoft Azure
- Nginx
- Git & GitHub

---

###  Project Structure

```bash
mini-finance/
├── terraform/
│ ├── providers.tf
│ ├── main.tf
│ ├── variables.tf
│ └── outputs.tf
├── ansible/
│ ├── inventory.ini
│ └── site.yml
└── README.md
```

---

###  Deployment Steps

### 1. Provision Infrastructure (Terraform)

```bash
cd terraform
terraform init
terraform plan
terraform apply
```
Output:
```
public_ip = <your_public_ip>
```
---
### 2. Configure SSH Access
```bash
ssh azureuser@<public_ip>
```
Ensure passwordless authentication works using your SSH key.

---
### 3. Configure & Deploy (Ansible)
```bash
cd ../ansible
ansible-playbook -i inventory.ini site.yml
```
---
### Ansible Workflow

**Play 1: Install & Configure Nginx**
- Update package cache
- Install nginx and git
- Start and enable nginx service

**Play 2: Deploy Application**
- Clone repository:
  ```bash
  https://github.com/adesegunasunmo/mini-finance.git
  ```
- Copy files to `/var/www/html`
- Set correct ownership
- Restart nginx using handler

**Play 3: Verify Deployment**
- Send HTTP request using Ansible uri module
- Validate response status code = 200
---

### Application Access

Open in browser:
```bash
http://<public_ip>
```

---
### Expected Outcome
- Infrastructure provisioned successfully
- Passwordless SSH configured
- Ansible playbook runs without errors
- Nginx serves the application
- HTTP verification returns status 200

---

### Challenges Faced
- SSH authentication issues across different systems
- Incorrect Ansible inventory configuration
- DNS resolution issues affecting connectivity
---

### Solutions
Ensured correct SSH key usage and permissions
Fixed inventory file formatting and variables
Resolved DNS issues in WSL environment

---

### Key Learnings
- Infrastructure as Code (Terraform)
- Configuration Management (Ansible)
- Debugging real-world deployment issues
- Importance of automation and idempotency
- Clean separation of concerns in DevOps workflows
---

### Future Improvements
- Add CI/CD pipeline (GitHub Actions)
- Use dynamic inventory for Azure
- Implement HTTPS with SSL
- Containerize application using Docker
---


### ⭐ Acknowledgements

Mini Finance App Source:

https://github.com/pravinmishraaws/mini-finance-project
