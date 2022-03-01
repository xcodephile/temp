---
title: 'WSL, Solusi Menjalankan Perintah Linux di Windows'
date: 2022-02-26 17:12:00 +0700
categories: []    # max 2 elements
tags: [linux, windows, wsl, shell, terminal]     # should always be lowercase. min = 0, max = infinity
---

Apakah kamu seorang programmer, content creator, dan gamer sekaligus, yang dituntut untuk punya sistem operasi yang mendukung pengembangan perangkat lunak dan juga menawarkan banyak aplikasi dan game? Atau setidaknya, apakah kamu tertarik akan keseksian command Linux namun tidak bisa lepas dari kepraktisan Windows?

Jika iya, kamu berada di tempat yang benar. Lanjut scroll ke bawah.

![Windows vs Linux](https://www.argeweb.nl/blog/wp-content/uploads/2017/11/windows_vps.png)_Sumber: argeweb.nl_

Ada beberapa solusi yang bisa kita pilih agar bisa menyicipi Linux. Beberapa di antaranya: menjalankan Linux secara virtual di atas Windows atau cara kedua, menginstal kedua sistem operasi secara terpisah di dalam satu komputer.

Cara pertama walau terdengar mudah dengan hanya menginstal VirtualBox, namun akan muncul ketergantungan karena Windows harus dihidupkan terlebih dahulu jika ingin menjalankan Linux. Cara kedua, dual boot, akan lebih ribet lagi karena komputer harus dinyalakan ulang jika ingin berganti sistem operasi. Windows dan Linux masih berjalan di sistem yang berbeda.

## Windows Subsystem for Linux (WSL)

Windows Subsystem for Linux adalah compatibility layer yang bertugas untuk menangani operasi tingkat kernel, menerjemahkannya ke instruksi yang dipahami Windows. Dengan adanya layer ini, file executable Linux (dalam format ELF) dapat dijalankan di Windows 10 dan 11. 

![WSL v1](https://raw.githubusercontent.com/xcodephile/xcodephile.github.io/main/assets/img/posts/wsl1-arch.png)

Linux tidak pernah tahu bahwa sebenarnya kernel Windows-lah yang menangani semua permintaannya.

Jika ada permintaan yang tidak dapat dipahami kernel Windows, akan ada fallback logic untuk menjalankan perintah di lingkungan Windows. Misalnya mengetik notepad.exe di prompt Linux, maka yang akan terjadi adalah program Notepad akan terbuka dari Windows.

WSL bisa jadi pengantar ideal bagi mereka yang masih asing dengan Linux tanpa harus menginstal sistem operasi baru sepenuhnya. Dengan cara ini, kamu bisa menggunakan perintah Linux untuk mengelola serta mengedit file yang biasanya diakses dari File Explorer, mengubah konfigurasi sistem, ngoding (Python dan Git paket bawaan di hampir semua distro Linux), dsb. Windows dan Linux benar-benar berjalan di satu sistem. 

## Prasyarat

* Windows 11, atau
* Windows 10 versi 2004+ (Build 19041+)

> Untuk mengetahui build number, tekan tombol <kbd>Windows</kbd> dan <kbd>R</kbd> bersamaan, ketik `winver`, lalu klik <kbd>OK</kbd>.
{: .prompt-tip }

## Instalasi

Hanya diperlukan beberapa klik dan ketik saja untuk memperoleh fitur ini.

### 1. Aktifkan fitur WSL

![Instal WSL](https://raw.githubusercontent.com/xcodephile/xcodephile.github.io/main/assets/img/posts/wsl-1.png)

Buka Pengaturan > Aplikasi > Fitur Opsional > Fitur Windows Lainnya > Windows Features. Centang Windows Subsystem for Linux lalu klik OK. Windows akan mengunduh beberapa file yang diperlukan secara otomatis. Jika sudah selesai, nyalakan ulang komputer agar WSL bisa diaktifkan.

### 2. Unduh Linux

![Unduh Linux](https://raw.githubusercontent.com/xcodephile/xcodephile.github.io/main/assets/img/posts/wsl-2.png)

Buka aplikasi Microsoft Store lalu instal distro Linux yang kamu inginkan, misalnya Ubuntu. Besar ukuran Ubuntu sekitar 200 MB.

Setelah selesai mengunduh, Klik Launch untuk memulai proses instalasi Ubuntu. Ini akan membuka jendela command line interface. Di awal instalasi, sistem akan meminta nama pengguna dan sandi yang nantnya digunakan di Ubuntu. Samakan saja dengan akun Windows kamu agar mudah diingat.

### 3. Selesai

Yup, selesai. Silahkan buka aplikasi terminal favoritmu. Di sini saya menggunakan Windows Terminal.

![Windows Terminal](https://raw.githubusercontent.com/xcodephile/xcodephile.github.io/main/assets/img/posts/wsl-3.png)

Saya merekomendasikan Windows Terminal karena punya banyak fitur dan tampilannya mudah dikostumisasikan. Aplikasi ini tersedia gratis di Microsoft Store.

![Instal WSL](https://raw.githubusercontent.com/xcodephile/xcodephile.github.io/main/assets/img/posts/wsl-4.png)

## Kenapa Harus WSL?

1. Agar juga bisa menginstal Docker (butuh upgrade ke versi WSL 2).
2. Lanjutan dari poin 1, dapat mengembangkan perangkat lunak beserta ekosistemnya dengan lebih leluasa, misalnya menggunakan Kubernetes.
3. Posting ini adalah pendahuluan untuk posting selanjutnya mengenai [Percantik Tampilan Windows Terminal WSL Menggunakan Zsh (Z Shell)](/). WSL sudah terkonfigurasi otomatis sehingga langsung dapat digunakan di Windows Terminal.

## Windows Subsystem for Linux version 2 (WSL 2)

WSL 2 bekerja dengan cara yang benar-benar berbeda dari pendahulunya, WSL 1. Ia menjalankan kernel Linux di dalam VM yang sangat ringan. Bukan seperti WSL 1 yang hanya menambahkan layer tambahan.

![WSL v2](https://raw.githubusercontent.com/xcodephile/xcodephile.github.io/main/assets/img/posts/wsl2-arch.png)

### Perbandingan

| Fitur                              | WSL 1 | WSL 2 |
|:-----------------------------------|:------|-----:|
| Integrasi antara Windows dan Linux |  ✅  |  ✅  |
| Waktu booting yang cepat           |  ✅  |  ✅  |
| Managed VM                         |  ❌  |  ✅  |
| Kernel Linux lengkap               |  ❌  |  ✅  |
| Kompatibilitas full system call    |  ❌  |  ✅  |
| Peforma sistem file antar OS       |  ✅  |  ❌  |

### Instalasi WSL 2

> Jika sebelumnya kamu sudah menjalankan WSL dan ingin memastikan versi WSL yang sedang digunakan, ketik perintah berikut di PowerShell atau CMD: `wsl --list --verbose`. Perhatikan di kolom Version. 
{: .prompt-tip }

Setelah menyelesaikan [langkah instalasi di atas](#instalasi), ketik perintah `wsl --set-version <DISTRIBUTION_NAME> <VERSION>` (contoh: `wsl --set-version ubuntu 2`) di PowerShell atau CMD. Pastikan sebelumnya kamu telah mencentang fitur opsional Windows yang bernama Virtual Machine Platform (checkbox-nya berada di lokasi yang sama dengan [yang ini](#1-aktifkan-fitur-wsl)). Cukup lakukan itu saja untuk mengganti versi. Verifikasi dengan menjalankan perintah `wsl --list --verbose`.

## Perintah Dasar

Jalankan perintah-perintah dasar WSL berikut di PowerShell atau di CMD.

* Buka WSL terminal
    ```console
wsl
    ```

* Lihat semua distro Linux yang tersedia untuk diunduh
    ```console
wsl --list --online
    ```

* Instal distro
    ```console
wsl --install --distribution <DISTRIBUTION_NAME>
    ```

* Lihat semua distro yang telah terinstal
    ```console
wsl --list --verbose
    ```

* Ubah versi WSL
    ```console
wsl --set-version <DISTRIBUTION_NAME> <VERSION>
    ```

* Ubah versi default WSL
    ```console
wsl --set-default-version <VERSION>
    ```

* Lihat status WSL saat ini
    ```console
wsl --status
    ```

## Tautan Eksternal

* [docs.microsoft.com/en-us/windows/wsl/install](https://docs.microsoft.com/en-us/windows/wsl/install)

* [docs.microsoft.com/en-us/windows/wsl/compare-versions](https://docs.microsoft.com/en-us/windows/wsl/compare-versions)

* [docs.microsoft.com/en-us/windows/wsl/basic-commands](https://docs.microsoft.com/en-us/windows/wsl/basic-commands)