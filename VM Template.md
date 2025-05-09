# Siapkan Template VM di Proxmox

### 1. Install Paket yang diperlukan pada VM template:
```sh
sudo apt update && sudo apt install -y \
    qemu-guest-agent \
    openssh-server \
    python3 \
    python3-pip \
    python3-apt \
    sudo \
    curl
sudo apt update && sudo apt install -y software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install -y ansible
ansible --version
```

### 2. Install Node Exporter di VM Template:
#### Download Node Exporter
```sh
wget https://github.com/prometheus/node_exporter/releases/download/v1.9.0/node_exporter-1.9.0.linux-amd64.tar.gz -O /tmp/node_exporter.tar.gz
```
#### Ekstrak dan Pindahkan File
```sh
tar -xzf /tmp/node_exporter.tar.gz -C /tmp/
sudo mv /tmp/node_exporter-* /opt/node_exporter
```
#### Buat User Node Exporter
```sh
sudo useradd -rs /bin/false node_exporter
```
#### Set Izin untuk Node Exporter
```sh
sudo chown -R node_exporter:node_exporter /opt/node_exporter
```
#### Buat Service File
```sh
sudo tee /etc/systemd/system/node_exporter.service > /dev/null <<EOF
[Unit]
Description=Node Exporter
After=network.target

[Service]
User=node_exporter
ExecStart=/opt/node_exporter/node_exporter
Restart=always

[Install]
WantedBy=multi-user.target
EOF

```
#### Reload systemd dan Jalankan Node Exporter
```sh
sudo systemctl daemon-reload
sudo systemctl enable --now node_exporter
```
#### Verifikasi Node Exporter Berjalan
```sh
systemctl status node_exporter
```
#### Setup SSH
##### 1. Install SSH
```sh
sudo apt install openssh-server
```
##### 2. SSH ke template VM dari VM utama:
```sh
ssh <user>@<template-vm-ip>
```
##### 3. Ubah settingan sshd agar bisa permit login
```sh
sudo sed -i 's/^#PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config
sudo grep -E "^PermitRootLogin" /etc/ssh/sshd_config
sudo systemctl restart ssh
sudo systemctl status ssh
```

##### 4. Buat direktori `.ssh` (jika belum ada):
```sh
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```
##### 5. Tambahkan kunci SSH publik ke file `authorized_keys`:
```sh
echo "<kunci-ssh-publik-yang-disalin>" >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```
Atau, jika ingin langsung dari file di VM utama:
```sh
ssh-copy-id <user>@<template-vm-ip>
```

##### 6. Keluar dari template VM:
```sh
exit
```
##### 7. Uji koneksi SSH dari VM utama ke template VM:
```sh
ssh <user>@<template-vm-ip>
```
Jika berhasil login tanpa diminta memasukkan password, konfigurasi sudah benar.

Dengan cara ini, template VM siap untuk dikelola oleh Ansible tanpa memerlukan password setiap kali SSH.

---

### 3. Konversi VM menjadi template:
#### Matikan VM:
```sh
qm shutdown <VM_ID>
```
#### Ubah Menjadi Template VM:
```sh
qm template <VM_ID>
```
