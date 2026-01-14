# DevOps Automation Project: Infrastructure as Code & Configuration Management

![Terraform](https://img.shields.io/badge/terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white)
![Ansible](https://img.shields.io/badge/ansible-%231A1918.svg?style=for-the-badge&logo=ansible&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=Prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/grafana-%23F46800.svg?style=for-the-badge&logo=grafana&logoColor=white)

Repositori ini berisi proyek automasi infrastruktur menggunakan metodologi **Infrastructure as Code (IaC)**. Proyek ini menggabungkan kekuatan **Terraform** untuk penyediaan (provisioning) Virtual Machine dan **Ansible** untuk manajemen konfigurasi serta instalasi berbagai layanan populer secara otomatis.

## 🚀 Fitur Utama

- **Automated Provisioning**: Membuat dan mengonfigurasi VM baru secara otomatis menggunakan Terraform.
- **Multi-Service Deployment**: Automasi instalasi berbagai layanan melalui Ansible Playbook:
  - **Web Server & CMS**: Nginx, WordPress.
  - **Cloud Storage**: Nextcloud, Owncloud.
  - **Containerization**: Docker, Kubernetes (K8s).
  - **Monitoring Stack**: Setup otomatis untuk monitoring performa sistem.
- **Tutorial Monitoring**: Dilengkapi dengan panduan setup Prometheus+, Grafana, dan Node Exporter.
- **Tutorial Membuat VM Template**: Panduan setup vm template untuk dijalankan oleh Terraform.

## 🛠️ Tools yang Digunakan

| Tool | Kegunaan |
| --- | --- |
| **Terraform** | Automasi pembuatan infrastruktur (Provisioning VM). |
| **Ansible** | Automasi konfigurasi software dan deployment aplikasi. |
| **Prometheus** | Sistem monitoring dan time-series database. |
| **Grafana** | Visualisasi data dan dashboard monitoring. |
| **Docker** | Platform containerization. |
| **Kubernetes** | Orchestration untuk container. |

## 📋 Prasyarat (Prerequisites)

Sebelum menjalankan proyek ini, pastikan Anda telah menginstal:

1. [Terraform](https://www.terraform.io/downloads) (Versi terbaru direkomendasikan).
2. [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).
3. SSH Key yang sudah terkonfigurasi untuk akses ke VM.
4. Provider Cloud/Virtualisasi (seperti AWS, GCP, Azure, atau Proxmox) yang kredensialnya sudah disiapkan.
*NOTE: Author menggunakan Proxmox yang dijalankan di server On-Premises

