
# Monitoring Docker Daemon

1. Mengaktifkan Metric Docker Daemon
```bash
sudo vi /etc/docker/daemon.json
```

2. Isi file dengan konfigurasi berikut 
```bash
{
  "metrics-addr" : "127.0.0.1:9323",
  "experimental" : true
}
```

3. Simpan file dan restart Docker
```bash
sudo systemctl restart docker
```

4. Konfigurasi Prometheus untuk Scrape Docker 
```bash
sudo vi /etc/prometheus/prometheus.yml
```

5. Tambahkan Job baru dibawah kode "scrape_configs"
```bash
  # Jangan Hapus Job di atasnya
  # TAMBAHKAN JOB BARU DI BAWAH INI
  - job_name: 'docker'
    static_configs:
      - targets: ['localhost:9323']
```

6. Simpan file lalu restart Prometheus untuk menerapkan perubahan
```bash
sudo systemctl restart prometheus
```

7. Import Dashboard Grafana 
- Buka Grafana di Browser pada port 3000, Lalu Klik menu Dashboard klik Import
![ss-1](./image/image1.png)

8. Buka Web https://grafana.com/ lalu klik menu Search ketik "193", Setelah itu Klik pilihan paling atas bernama Docker Monitoring.Lalu Klik "Copy ID to clipboard"
![ss-2](./image/2.png)

9. Lanjutkan Klik Import, Masukan ID setelah itu klik tombol LOAD 
![ss-3](./image/3.png)

10. Pilih Prometheus yang telah dimasukan, Klik import
![ss-4](./image/4.png)

11. Setelah itu akan muncul tampilan dashboard Grafana yang berisi Metric monitoring Docker dan Containernya
![ss-5](./image/5.png)

12. Setelah itu Save tampilan Dashboard: save dashboard --> Save


