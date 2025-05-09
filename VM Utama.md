# Konfigurasi VM Utama

## 1.1 Install Terraform
### 1. Tambahkan repositori HashiCorp:
```sh
sudo apt update && sudo apt install -y gnupg software-properties-common curl
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
```

### 2. Install Terraform:
```sh
sudo apt update && sudo apt install -y terraform
```

---

## 1.2 Install Ansible
### 1. Tambahkan repositori Ansible:
```sh
sudo apt update && sudo apt install -y software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
```

### 2. Install Ansible:
```sh
sudo apt install -y ansible
```

### 3. Pastikan versi Ansible dan Terraform:
```sh
terraform -version
ansible --version
```

---

## 1.3 Tambahkan Kunci SSH

### **Langkah 1: Membuat SSH Key Baru**
1. Pada VM utama, buka terminal dan buatlah kunci SSH publik:

   Install terlebih dahulu ssh server,
   ```sh
   sudo apt install openssh-server
   ```

   ```sh
   ssh-keygen -t rsa -b 4096 -C "nama_anda@example.com"
   ```

3. Menampilkan Kunci SSH Publik:
   ```sh
   cat ~/.ssh/id_rsa.pub
   ```

   Catat Hasilnya.

### **Langkah 2: Buka Firewall dan Port**
```sh
sudo ufw allow 22/tcp
sudo ufw reload
```

### **Langkah 3: Masuk ke Template VM**
#### 1. Install SSH
```sh
sudo apt install openssh-server
```
#### 2. SSH ke template VM dari VM utama:
```sh
ssh <user>@<template-vm-ip>
```
#### 3. Ubah settingan sshd agar bisa permit login
```sh
sudo sed -i 's/^#PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config
sudo grep -E "^PermitRootLogin" /etc/ssh/sshd_config
sudo systemctl restart ssh
sudo systemctl status ssh
```

### **Langkah 4: Tambahkan Kunci ke `authorized_keys`**
#### 1. Buat direktori `.ssh` (jika belum ada):
```sh
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```
#### 2. Tambahkan kunci SSH publik ke file `authorized_keys`:
```sh
echo "<kunci-ssh-publik-yang-disalin>" >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```
Atau, jika ingin langsung dari file di VM utama:
```sh
ssh-copy-id <user>@<template-vm-ip>
```

### **Langkah 5: Uji Koneksi SSH**
#### 1. Keluar dari template VM:
```sh
exit
```
#### 2. Uji koneksi SSH dari VM utama ke template VM:
```sh
ssh <user>@<template-vm-ip>
```
Jika berhasil login tanpa diminta memasukkan password, konfigurasi sudah benar.

Dengan cara ini, template VM siap untuk dikelola oleh Ansible tanpa memerlukan password setiap kali SSH.

---
