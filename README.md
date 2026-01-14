# DevOps Automation Project: Infrastructure as Code & Configuration Management

---

### 🏗️ Infrastructure & Automation
![Terraform](https://img.shields.io/badge/terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white)
![Ansible](https://img.shields.io/badge/ansible-%231A1918.svg?style=for-the-badge&logo=ansible&logoColor=white)

### 🌐 Services Automation
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white)
![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white)
![WordPress](https://img.shields.io/badge/WordPress-%2321759B.svg?style=for-the-badge&logo=WordPress&logoColor=white)
![Nextcloud](https://img.shields.io/badge/Nextcloud-%230082C9.svg?style=for-the-badge&logo=Nextcloud&logoColor=white)
![Owncloud](https://img.shields.io/badge/ownCloud-%231D2D44.svg?style=for-the-badge&logo=ownCloud&logoColor=white)

### 📊 Monitoring Stack
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=Prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/grafana-%23F46800.svg?style=for-the-badge&logo=grafana&logoColor=white)
![Node Exporter](https://img.shields.io/badge/Node%20Exporter-F46800?style=for-the-badge&logo=prometheus&logoColor=white)

---

This repository contains an infrastructure automation project leveraging **Infrastructure as Code (IaC)** methodologies. This project combines the power of **Terraform** for Virtual Machine (VM) provisioning and **Ansible** for configuration management and automated installation of various popular services.

## 🚀 Key Features

- **Automated Provisioning**: Automatically create and configure new VMs using Terraform.
- **Multi-Service Deployment**: Automated installation of various services via Ansible Playbooks:
  - **Web Server & CMS**: Nginx, WordPress.
  - **Cloud Storage**: Nextcloud, Owncloud.
  - **Containerization**: Docker, Kubernetes (K8s).
  - **Monitoring Stack**: Automated setup for system performance monitoring.
- **Monitoring Tutorial**: Includes a comprehensive guide for setting up Prometheus, Grafana, and Node Exporter.
- **VM Template Tutorial**: Documentation on setting up VM templates to be deployed via Terraform.

## 🛠️ Tools Used

| Tool | Purpose |
| --- | --- |
| **Terraform** | Infrastructure automation (VM Provisioning). |
| **Ansible** | Software configuration automation and application deployment. |
| **Prometheus** | Monitoring system and time-series database. |
| **Grafana** | Data visualization and monitoring dashboards. |
| **Docker** | Containerization platform. |
| **Kubernetes** | Container orchestration. |

## 📋 Prerequisites

Before running this project, ensure you have installed:

1. [Terraform](https://www.terraform.io/downloads) (Latest version recommended).
2. [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).
3. Configured **SSH Keys** for VM access.
4. A **Cloud/Virtualization Provider** (e.g., AWS, GCP, Azure, or Proxmox) with prepared credentials.

> **NOTE:** The author uses **Proxmox** running on an On-Premises server.
