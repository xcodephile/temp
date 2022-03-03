---
title: 'Bikin Visual Studio Code Jadi Lebih Minimalis dan Canggih [WIP]'
date: 2022-03-01 22:13:00 +0700
categories: []    # max 2 elements
tags: [vscode, ide, windows, wsl, git, shell, terminal, zsh]     # should always be lowercase. min = 0, max = infinity
---

> "Posting ini masih ditandai sebagai WIP (work in progress)."
{: .prompt-danger }

Mirip seperti posting sebelumnya yang berjudul [Percantik Tampilan Windows Terminal WSL Ubuntu Menggunakan Zsh](https://xcodephile.github.io/posts/percantik-windows-terminal-menggunakan-zsh), kali ini yang menjadi kelinci percobaan beralih dari Windows Terminal ke VS Code alias Visual Studio Code.

![Sebelum](https://raw.githubusercontent.com/xcodephile/xcodephile.github.io/main/assets/img/posts/vscode-0.jpg){: width="607" height="341" }_Sebelum_

![Sesudah](https://raw.githubusercontent.com/xcodephile/xcodephile.github.io/main/assets/img/posts/vscode-1.png){: width="607" height="341" }_Sesudah_

Siapa yang tidak mengenal VS Code? Salah satu [IDE](https://en.wikipedia.org/wiki/Integrated_development_environment) terbaik besutan Microsoft ini dibekali dengan sejuta fitur dan plugin yang membuat kita betah untuk menggunakannya. IDE ini bisa digunakan untuk banyak tujuan seperti membuat website, web apps, web services, mobile apps, hingga desktop apps. Tidak heran ia dapat mendukung banyak bahasa seperti C++, Java, Swift, Visual Basic, Python, Go, JavaScript, PHP, CSS, SQL, PowerShell, BASH, dan lainnya.

Di posting kali ini, saya akan menjabarkan bagaimana merombak VS Code menjadi IDE yang minimalis dan juga canggih.

## Yang Kamu Butuhkan

- [Git bash](https://git-scm.com/download/win)
- Shell: [Zsh](https://github.com/zsh-users/zsh)
  - Framework: [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh)
  - Theme: [Powerlevel10k](https://github.com/romkatv/powerlevel10k)
- Theme: [GitHub Theme](https://marketplace.visualstudio.com/items?itemName=GitHub.github-vscode-theme)
- Icon packs: [Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)
- [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
- [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)
- [Customize UI](https://marketplace.visualstudio.com/items?itemName=iocave.customize-ui)
