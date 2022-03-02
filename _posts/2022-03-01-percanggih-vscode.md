---
title: 'Bikin Visual Studio Code Kamu Jadi Lebih Minimalis Namun Canggih [WIP]'
date: 2022-03-01 22:13:00 +0700
categories: []    # max 2 elements
tags: [vscode, ide, windows, wsl, git, shell, terminal, zsh]     # should always be lowercase. min = 0, max = infinity
---

> "Posting ini masih ditandai sebagai WIP (work in progress)."
{: .prompt-danger }

Mirip seperti posting sebelumnya yang berjudul [Percantik Tampilan Windows Terminal WSL Ubuntu Menggunakan Zsh](https://xcodephile.github.io/posts/percantik-windows-terminal-menggunakan-zsh), kali ini yang menjadi kelinci percobaan beralih dari Windows Terminal ke VS Code alias Visual Studio Code.

![Sebelum](https://raw.githubusercontent.com/xcodephile/xcodephile.github.io/main/assets/img/posts/vscode-0.jpg)_Sebelum_

![Sesudah](https://raw.githubusercontent.com/xcodephile/xcodephile.github.io/main/assets/img/posts/vscode-1.png)_Sesudah_

Siapa yang tidak mengenal VS Code? Salah satu [IDE](https://en.wikipedia.org/wiki/Integrated_development_environment) terbaik besutan Microsoft ini dibekali dengan sejuta fitur dan plugin yang membuat kita betah untuk menggunakannya. VS Code digunakan dalam banyak tujuan, baik membuat website, web apps, web services, mobile apps, hingga desktop apps. Tidak heran ia dapat mendukung banyak bahasa seperti C++, Java, Swift, Visual Basic, Python, Go, JavaScript, PHP, CSS, SQL, PowerShell, BASH, dsb. Namun kadang kita merasa jenuh dengan tampilan dan tema yang itu-itu saja.

Di posting kali ini, tidak hanya tampilan yang akan saya ubah menjadi lebih sederhana dan flat, namun saya juga menginstal beberapa plugin yang menurut saya krusial.

## Daftar

* Git bash
* Zsh, Oh My Zsh, dan Powerlevel10K
* Github Theme
* Material Icon Theme
* Plugin: GitLens
* Plugin: Remote Explorer
* Plugin: Customize UI

## Tampilan Minimalis