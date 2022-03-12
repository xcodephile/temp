---
title: 'Install Aplikasi GUI Ubuntu di WSL Windows [WIP]'
date: 2022-03-06 00:24:00 +0700
categories: []    # max 2 elements
tags: [vscode, ide, windows, wsl, git, shell, terminal, zsh]     # should always be lowercase. min = 0, max = infinity
---


Prasyarat
- Windows 11 (build 22000.*) atau Windows 11 Insider Preview (builds 21362+)
- WSL 2


https://chuckdries.medium.com/installing-gitkraken-in-wsl-2-15bf6459f823
https://github.com/microsoft/wslg?WT.mc_id=-blog-scottha




wsl --update
wsl --shutdown
Buka terminal ubuntu untuk menyalakan WSL
wsl --list --verbose

wget https://release.gitkraken.com/linux/gitkraken-amd64.deb
sudo apt install ./gitkraken-amd64.deb
sudo apt --fix-broken install # jalankan ini jika ada error dependencies

