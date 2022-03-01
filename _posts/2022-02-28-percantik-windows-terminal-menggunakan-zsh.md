---
title: 'Percantik Tampilan Windows Terminal WSL Ubuntu Menggunakan Zsh (Z shell)'
date: 2022-02-28 13:19:00 +0700
categories: []    # max 2 elements
tags: [linux, windows, wsl, shell, terminal, zsh]     # should always be lowercase. min = 0, max = infinity
---

Ingin rupa Windows Terminal kamu berubah dari yang super monoton old school menjadi lebih fresh seperti ini?

![Windows Terminal](https://raw.githubusercontent.com/xcodephile/xcodephile.github.io/main/assets/img/posts/windows-terminal-after-before.png)

## Yang Kamu Butuhkan
1. Terminal: [Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701#activetab=pivot:overviewtab) (tersedia gratis di Microsoft Store)
2. Font: [Cousine Nerd Font Mono](https://www.nerdfonts.com/font-downloads)
3. Shell: [Zsh](https://github.com/zsh-users/zsh)
4. Shell Framework: [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh)
4. Shell Theme: [Powerlevel10k](https://github.com/romkatv/powerlevel10k)
5. WSL Ubuntu ([Apa itu WSL?](https://xcodephile.github.io/posts/perintah-linux-di-windows))

## Instalasi

### Langkah 1 : Instal Windows Terminal

Buka Microsoft Store > cari aplikasi Windows Terminal > klik install.

![Windows Terminal](https://raw.githubusercontent.com/xcodephile/xcodephile.github.io/main/assets/img/posts/windows-terminal-store.png)

Kenapa harus Windows Terminal? Dibandingkan dengan terminal lain, aplikasi ini punya banyak keunggulan seperti dukungan multi tab, tema yang bisa diubah-ubah, dan bahkan kita bisa mengganti latarnya dengan gambar GIF. Selain itu, terminal ini juga sudah terkonfigurasi secara otomatis dengan PowerShell, CMD, dan WSL. Buka aplikasi dan kamu ready to go.

### Langkah 2 : Instal Font Monospace

Powerlevel10k banyak menggunakan simbol yang tidak umum sehingga kamu harus mengganti font bawaan di terminal agar tidak ada karakter kotak-kotak, tanda tanya, atau sebagainya yang menandakan bahwa suatu simbol tidak dapat dirender oleh font bawaan.

Perlu diingat bahwa jenis font yang harus diunduh adalah monospace. Contohnya pada gambar pertama, font yang saya gunakan adalah Cousine Nerd Font Mono. Kamu bisa mengunduh font gratis lainnya di [Nerd Fonts](https://www.nerdfonts.com/font-downloads), lalu ekstrak dan instal semua file font .otf.

### Langkah 3 : Ubah Font Bawaan

Langkah selanjutnya adalah mengubah font bawaan di Windows Terminal. Caranya yaitu buka Windows Terminal > Settings > Ubuntu > Appearance > Font Face > ganti dengan font yang barusan telah kamu instal > Save.

![Windows Terminal](https://raw.githubusercontent.com/xcodephile/xcodephile.github.io/main/assets/img/posts/windows-terminal-setting-font-face.png)

### Langkah 4 : Instal Zsh

Sekarang kita perlu menginstal Zsh di WSL. Buka Windows Terminal, pilih Ubuntu, lalu jalankan perintah ini untuk menginstal Zsh.

```shell
sudo apt update
```

```shell
sudo apt install zsh
```

Jika kamu menggunakan distro Linux yang berbeda, silahkan baca [dokumentasi Zsh](https://zsh.sourceforge.io/) atau dokumentasi package manager distro kamu. 

### Langkah 5 : Instal Oh My Zsh

Oh My Zsh adalah framework shell Zsh yang nantinya memudahkan kita untuk menyesuaikan apa saja, termasuk mengganti tema dan menambah plugin.

```shell
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Langkah 6 : Instal Powerlevel10k

Hal yang harus kita instal berikutnya adalah tema Powerlevel10k dengan perintah berikut.

```shell
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k
```

Tema ini juga punya fitur wizard setup-nya sendiri sehingga hanya cukup menekan beberapa tombol saja. Mirip seperti installation wizard Windows yang hanya next, next, i agree, install. 

Setelah proses setup telah selesai, kamu perlu mengedit file `~/.zshrc` dan mengganti `ZSH_THEME=` menjadi `ZSH_THEME="powerlevel10k/powerlevel10k"`. Tutup dan buka kembali Windows Terminal.

### Langkah 7: Ubah Default Profile 

Alih-alih PowerShell atau CMD, agar WSL Ubuntu terbuka tiap kali kamu membuka Windows Terminal, ubah pengaturannya degan cara: Buka Windows Terminal > Settings > Startup > Default Profile > pilih Ubuntu > Save.

### Langkah 8 (opsional): Edit file settings.json

> Penting! Silahkan backup file settings.json sebelum mengubahnya secara manual.
{: .prompt-danger }

Agar terminal kamu sama persis dengan yang di gambar paling atas, terutama di bagian transparansi dan warna latar teks, edit file `settings.json` dengan cara: Buka Windows Terminal > Settings > Open JSON File > cari di bagian pengaturan WSL Ubuntu (biasanya `"name": "Ubuntu"`) > lalu sesuaikan menjadi seperti berikut.

```json
{
    "guid": "{2c4de342-38b7-51cf-b940-2309a097f518}",
    "name": "Ubuntu",
    "hidden": false,
    "source": "Windows.Terminal.Wsl",
    "font": 
    {
        "face": "Cousine Nerd Font Mono"
    },
    "colorScheme": "xcodephile",
    "useAcrylic": true,
    "acrylicOpacity": 0.8
}
```

Masih di file `settings.json`, di bagian `schemes` tambahkan satu blok berikut:

```json
{
    "name": "xcodephile",
    "background": "#282C34",
    "black": "#282C34",
    "blue": "#0085CE",
    "brightBlack": "#5A6374",
    "brightBlue": "#0085CE",
    "brightCyan": "#56B6C2",
    "brightGreen": "#3AE872",
    "brightPurple": "#C678DD",
    "brightRed": "#E06C75",
    "brightWhite": "#DCDFE4",
    "brightYellow": "#E5C07B",
    "cursorColor": "#FFFFFF",
    "cyan": "#56B6C2",
    "foreground": "#DCDFE4",
    "green": "#3AE872",
    "purple": "#C678DD",
    "red": "#E06C75",
    "selectionBackground": "#FFFFFF",
    "white": "#DCDFE4",
    "yellow": "#E5C07B"
}
```

Simpan dan tutup file `settings.json`.

Jika semuanya lancar, seharusnya Windows Terminal kamu sudah sama persis dengan yang saya punya.