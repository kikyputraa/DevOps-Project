
# Instalasi Prometheus dan Grafana

Panduan ini menjelaskan cara menginstal **Prometheus** dan **Grafana** secara manual di sistem **Ubuntu/Debian**.

Anda bisa menggunakan tutorial ini atau Menggunakan Skrip Ansible.

---

## 1. Install dan Konfigurasi Prometheus

### Download dan Ekstrak Prometheus

```bash
wget https://github.com/prometheus/prometheus/releases/download/v2.51.2/prometheus-2.51.2.linux-amd64.tar.gz -O /tmp/prometheus.tar.gz
tar -xzf /tmp/prometheus.tar.gz -C /opt/
sudo mv /opt/prometheus-2.51.2.linux-amd64 /opt/prometheus
```

### Buat User Khusus Prometheus

```bash
sudo useradd --no-create-home --shell /sbin/nologin prometheus
```

### Atur Hak Akses

```bash
sudo chown -R prometheus:prometheus /opt/prometheus
```

### Buat Direktori Data (opsional)

```bash
sudo mkdir -p /data
sudo chown prometheus:prometheus /data
sudo chmod 755 /data
```

### Tambahkan Konfigurasi `prometheus.yml`

Buat file `/opt/prometheus/prometheus.yml` dengan isi (contoh minimal):

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: "prometheus"
    static_configs:
      - targets: ["localhost:9090"]
```

> Atur owner:

```bash
sudo chown prometheus:prometheus /opt/prometheus/prometheus.yml
```

### Buat Service Systemd untuk Prometheus

```bash
sudo nano /etc/systemd/system/prometheus.service
```

Isi dengan:

```ini
[Unit]
Description=Prometheus Monitoring
After=network.target

[Service]
User=prometheus
WorkingDirectory=/opt/prometheus
ExecStart=/opt/prometheus/prometheus --config.file=/opt/prometheus/prometheus.yml
Restart=always

[Install]
WantedBy=multi-user.target
```

Aktifkan dan mulai servicenya:

```bash
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
sudo systemctl start prometheus
sudo systemctl enable prometheus
```

---

## 2. Instalasi Grafana

### Tambahkan GPG Key & Repository Grafana

```bash
wget -q -O - https://packages.grafana.com/gpg.key | gpg --dearmor | sudo tee /usr/share/keyrings/grafana-keyring.gpg > /dev/null

echo "deb [signed-by=/usr/share/keyrings/grafana-keyring.gpg] https://packages.grafana.com/oss/deb stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
```

### Update APT dan Install Grafana

```bash
sudo apt update
sudo apt install -y grafana
```

### Start dan Enable Grafana

```bash
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
```

---

## 3. Tambahkan Dashboard di Grafana (Opsional)

### Buat Direktori Dashboard

```bash
sudo mkdir -p /var/lib/grafana/dashboards
sudo chown grafana:grafana /var/lib/grafana/dashboards
```

### Tambahkan File Provisioning

**File: `/etc/grafana/provisioning/dashboards/dashboard.yml`**

```yaml
apiVersion: 1

providers:
  - name: 'default'
    orgId: 1
    folder: ''
    type: file
    disableDeletion: false
    editable: true
    options:
      path: /var/lib/grafana/dashboards
```

**File: `/var/lib/grafana/dashboards/default.json`**  
(Salin file JSON dashboard dari template yang telah kamu buat)

```bash
sudo cp dashboard.json /var/lib/grafana/dashboards/default.json
sudo chown grafana:grafana /var/lib/grafana/dashboards/default.json
```

Lalu restart Grafana:

```bash
sudo systemctl restart grafana-server
```

---

## 4. Buka Port Firewall (UFW)

```bash
sudo ufw allow 9090/tcp   # Prometheus
sudo ufw allow 3000/tcp   # Grafana
sudo ufw reload
```

---

## 5. Akses Web

- **Prometheus**: http://localhost:9090  
- **Grafana**: http://localhost:3000 (login default: `admin` / `admin`)

---
