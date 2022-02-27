---
title: 'WSL, Solusi Menjalankan Perintah Linux di Windows [WIP]'
date: 2022-02-26 17:12:00 +0700
categories: []    # max 2 elements
tags: [linux, windows, wsl, shell]     # should always be lowercase. min = 0, max = infinity
---

> Posting ini masih ditandai sebagai WIP (Work in Progress), yang berarti ada bagian yang belum lengkap atau bahkan tidak akurat. 
{: .prompt-danger }

Apakah kamu seorang programmer, content creator, dan gamer sekaligus, yang dituntut untuk punya sistem operasi yang mendukung pengembangan perangkat lunak sumber terbuka dan juga menawarkan banyak aplikasi dan game yang dapat diinstal? Atau setidaknya, apakah kamu tertarik akan keseksian command Linux namun tidak bisa lepas dari kepraktisan Windows?

Jika iya, kamu berada di tempat yang benar. Lanjut scroll ke bawah.

![Windows vs Linux](https://www.argeweb.nl/blog/wp-content/uploads/2017/11/windows_vps.png)_Sumber: argeweb.nl_

Ada beberapa solusi yang bisa kita pilih agar bisa menyicipi Linux. Beberapa di antaranya: menjalankan Linux secara virtual di atas Windows dan menginstal kedua sistem operasi secara terpisah di dalam satu komputer.

Cara pertama walau terdengar mudah dengan hanya menginstal VirtualBox, namun akan muncul ketergantungan karena Windows harus dihidupkan terlebih dahulu jika ingin menjalankan Linux. Cara kedua, dual boot, akan lebih ribet lagi karena komputer harus dinyalakan ulang jika ingin berganti sistem operasi. Windows dan Linux masih berjalan di sistem yang berbeda.

## Windows Subsystem for Linux

Windows Subsystem for Linux (WSL) adalah compatibility layer yang bertugas untuk menangani operasi tingkat kernel, menerjemahkannya ke instruksi yang dipahami Windows. Dengan adanya layer ini, file executable Linux (dalam format ELF) dapat dijalankan di Windows 10 dan 11. 

(GAMBAR ARSITEKTUR WSL-1)

Linux tidak pernah tahu bahwa sebenarnya kernel Windows-lah yang menangani semua permintaannya.

Jika ada permintaan yang tidak dapat dipahami kernel Windows, akan ada fallback logic untuk menjalankan perintah di lingkungan Windows. Misalnya mengetik notepad.exe di prompt Linux, maka yang akan terjadi adalah program Notepad akan terbuka dari Windows.

WSL bisa jadi pengantar ideal bagi mereka yang masih asing dengan Linux tanpa harus menginstal sistem operasi baru sepenuhnya. Dengan cara ini, kamu bisa menggunakan perintah Linux untuk mengelola serta mengedit file yang biasanya diakses dari File Explorer, mengubah konfigurasi sistem, ngoding (Python dan Git adalah dua dari sekian program bawaan Linux), dsb. Windows dan Linux benar-benar berjalan di satu sistem. 

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

Buka aplikasi Windows Store lalu instal distro Linux yang kamu inginkan, misalnya Ubuntu. Besar ukuran Ubuntu sekitar 200 MB.

Setelah selesai mengunduh, Klik Launch untuk memulai proses instalasi Ubuntu. Ini akan membuka jendela command line interface. Di awal instalasi, sistem akan meminta nama pengguna dan sandi yang nantnya digunakan di Ubuntu. Samakan saja dengan Windows punyamu agar tidak lupa.

### 3. Selesai

Yup, selesai. Silahkan buka aplikasi terminal favoritmu. Di sini saya menggunakan Windows Terminal.

![Instal WSL](https://raw.githubusercontent.com/xcodephile/xcodephile.github.io/main/assets/img/posts/wsl-3.png)

Saya merekomendasikan Windows Terminal karena punya banyak fitur dan tampilannya mudah dikostumisasikan. Aplikasi ini tersedia gratis di Microsoft Store.

![Instal WSL](https://raw.githubusercontent.com/xcodephile/xcodephile.github.io/main/assets/img/posts/wsl-4.png)

## Kenapa Harus WSL?

1. Agar dapat sekalian menginstal Docker (butuh upgrade ke versi WSL 2).
2. Lanjutan dari poin 1, dapat mengembangkan perangkat lunak beserta ekosistemnya dengan lebih leluasa, misalnya menggunakan Kubernetes.
3. Posting ini adalah pendahuluan untuk posting selanjutnya mengenai [Kustomisasi Tampilan Windows Terminal Menggunakan Zsh (Z Shell)](/). WSL sudah terkonfigurasi otomatis sehingga langsung terintegrasi ke Windows Terminal.

## Tautan Eksternal

* [docs.microsoft.com/en-us/windows/wsl/install](https://docs.microsoft.com/en-us/windows/wsl/install)

* [docs.microsoft.com/en-us/windows/wsl/compare-versions](https://docs.microsoft.com/en-us/windows/wsl/compare-versions)