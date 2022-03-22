---
title: 'Monitoring Kontainer Docker Menggunakan Prometheus dan Grafana'
date: 2022-03-22 21:36:00 +0700
categories: []    # max 2 elements
tags: [containerization, docker, docker-compose, monitoring, prometheus, grafana]     # should always be lowercase. min = 0, max = infinity
---

# Tech Stack

- [Prometheus](https://prometheus.io/docs/introduction/overview/)
- [Grafana](https://grafana.com/docs/grafana/latest/introduction/)
- [cAdvisor](https://github.com/google/cadvisor)
- [Docker](https://docs.docker.com/get-started/overview/)

![](../../assets/img/posts/grafana-prometheus-monitoring.gif)

# Prasyarat

Ini adalah lanjutan dari post sebelumnya, [Implementasi Kontainerisasi dan CI (Continuous Integration) Sederhana Menggunakan Jenkins](https://xcodephile.github.io/posts/implementasi-kontainerisasi-dan-ci-sederhana-menggunakan-jenkins-di-docker/). Agar lebih rapi, saya meletakkan Prometheus dan Grafana di satu jaringan Docker yang sama dengan kontainer yang dibuat di post sebelumnya, Jenkins dan Redis. Silahkan sesuaikan file `docker-compose.yml` jika ingin dibuat berbeda jaringan.

# Instalasi

## Cp. 1: Setup Kontainer

Simpan file `docker-compose.yml` dan file config `prometheus.yml` berikut ini di dalam satu direktori yang sama.

```yaml
# docker-compose.yml
version: '3.8'
services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    volumes:
    - ./prometheus.yml:/etc/prometheus/prometheus.yml
    command:
    - '--config.file=/etc/prometheus/prometheus.yml'
    - '--web.enable-lifecycle'
    depends_on:
    - cadvisor
    ports:
    - 9090:9090
    networks:
    - jenkins_network
  cadvisor:
    image: gcr.io/cadvisor/cadvisor:latest
    container_name: cadvisor
    ports:
    - 8080:8080
    volumes:
    - /:/rootfs:ro
    - /var/run:/var/run:ro
    - /sys:/sys:ro
    - /var/lib/docker/:/var/lib/docker:ro
    command:
      - privileged=true
    networks:
    - jenkins_network
  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    ports:
    - 9100:9100
    networks:
    - jenkins_network
  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    user: "1000"
    environment:
    - GF_SECURITY_ADMIN_PASSWORD=admin
    depends_on:
    - prometheus
    ports:
    - 3000:3000
    networks:
    - jenkins_network
networks:
  jenkins_network:
    external: true
## IMPORTANT:
## This project is designed to be on the same network as the Jenkins network: 'jenkins_network'.
## How to do that? Define name of jenkins network in every container (services.<container_name>.networks)
## and set networks.<network_name>.external to true.
```

```yaml
# prometheus.yml
global:
  scrape_interval: 15s
  external_labels:
    monitor: 'Monitoring'
scrape_configs:
  - job_name: 'prometheus' 
    static_configs: 
      - targets: ['localhost:9090']
  - job_name: 'cAdvisor' 
    static_configs:
      - targets: ['cadvisor:8080']
  - job_name: 'node-exporter' 
    static_configs: 
      - targets: ['node-exporter:9100']
```

Jalankan perintah berikut di dalam direktori di mana kedua file tersebut berada:

```shell
$ docker-compose up -d
```

Validasi bahwa kontainer telah berjalan dengan benar:

```shell
$ docker ps
```

## Cp. 2: Validasi cAdvisor

cAdvisor bertugas untuk mengumpulkan informasi mengenai semua kontainer yang sedang berjalan. Informasi ini nantinya diambil oleh Prometheus lalu diteruskan ke Grafana. Di Grafana inilah informasi disajikan dalam bentuk grafik.

Pastikan cAdvisor telah berjalan dengan baik dengan cara akses ke dashboard cAdvisor [http://localhost:8080/docker](http://localhost:8080/docker) melalui browser. Lihat di bagian Subcontainers. Semua kontainer yang sedang berjalan ditampikan di sini.

![](../../assets/img/posts/cadvisor-1.png)

Jika daftar kontainer dapat ditampilkan oleh cAdvisor, silahkan skip ke bagian [Setup Grafana](#setup-grafana).

Namun jika tidak ada kontainer yang muncul sedangkan perintah `docker ps` menampilkan sebaliknya, dan jika kamu menggunakan WSL 2, maka besar kemungkinan cAdvisor salah dalam mencari 'sumber' kontainer. Ketahui errornya terlebih dahulu dengan cara:

```
$ docker logs -f cadvisor
```

Jika ada banyak error yang bertuliskan `failed to identify the read-write layer ID for container ... open /rootfs/var/lib/docker ... no such file or directory`, maka jalankan perintah berikut ini.

> Secara default root directory Docker berada di /var/lib/docker. Khusus untuk WSL, lokasinya berada di tempat yang berbeda. Saya belum bisa menjamin apakah lokasinya selalu di wsl\\docker-desktop-data\\version-pack-data\\community\\docker. Mohon dipastikan terlebih dahulu. Link terkait: github.com/google/cadvisor/issues/2648.
{: .prompt-danger }

```
$ cd /mnt
$ sudo mkdir my-docker
$ sudo mount -t drvfs '\\wsl$\docker-desktop-data\version-pack-data\community\docker' /mnt/my-docker
```

Perintah di atas akan membuat direktori baru yang bernama `my-docker` lalu menyambungkan root directory Docker yang berada di luar Ubuntu ke direktori `/mnt/my-docker` yang berada di dalam Ubuntu.

Setelah menjalankan perintah di atas, ubah baris 27 di file `docker-compose.yml` dari ini:

```
- /var/lib/docker/:/var/lib/docker:ro
```

Menjadi ini:

```
- /mnt/my-docker/:/rootfs/var/lib/docker:ro
```

Lalu silahkan build ulang dengan cara:

```shell
$ docker-compose up -d
```

Validasi kembali melalui URL yang sama. Seharusnya cAdvisor sudah bisa memperoleh data kontainer.

## Setup Grafana 

Akses dashboard Grafana di [http://localhost:3000](http://localhost:3000). Login dengan username `admin` dan password `admin`.

![](../../assets/img/posts/grafana-ui-1.png)

Agar Grafana terhubung ke Prometheus, kita harus menambahkan data source baru dengan cara klik Data Sources lalu pilih opsi Prometheus. Grafana akan mengarahkan kita ke halaman pengaturan. Di sini cukup isi form URL `http://prometheus:9090`. Gulir ke paling bawah halaman dan klik Save & Test.

![](../../assets/img/posts/grafana-ui-1b.png)

> Baik Grafana dan Prometheus sama-sama berada di satu jaringan Docker yang sama. Docker secara otomatis menghubungkan nama service (lihat baris 4 di `docker-compose.yml`) ke alamat IP-nya. Karena itulah, hanya dengan menuliskan `prometheus`, Grafana bisa langsung tersambung ke kontainer Prometheus.
{: .prompt-tip }

Langkah selanjutnya adalah merancang layout dashboard. Agar jauh lebih praktis, kita gunakan saja dashboard yang tersedia di internet. Caranya, silahkan navigasi ke menu Create lalu klik Import.

![](../../assets/img/posts/grafana-ui-3.png)

Di form Import via Grafana.com, isikan `893`. Ini adalah ID dari dashboard [grafana.com/grafana/dashboards/893](https://grafana.com/grafana/dashboards/893). Jangan lupa klik Load. Selanjutnya, isi nama dashboard di form Name kemudian pilih Prometheus pada menu dropdown Select a Prometheus Data Source. Klik Import.

Selesai.

![](../../assets/img/posts/grafana.png)

# Tautan Eskternal

- [prometheus.io/docs/guides/cadvisor/#monitoring-docker-container-metrics-using-cadvisor](https://prometheus.io/docs/guides/cadvisor/#monitoring-docker-container-metrics-using-cadvisor)