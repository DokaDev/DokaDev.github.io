---
title: How to Install GitHub Desktop on Ubuntu
date: 2024-02-14 14:25 +0900
categories: [Git, GitHub]
tags: [linux, git, github]     # TAG names should always be lowercase
---

GitHub Desktop is a graphical user interface (GUI) tool that makes using Git and GitHub easier. As of the current date (February 14, 2024), this tool is available only for Windows and Mac environments. Users of these environments can install GitHub Desktop through the link below.

[GitHub Desktop | Simple collaboration from your desktop](https://desktop.github.com/)

However, GitHub Desktop is not natively available for Linux environments. Therefore, we need to use a different method to install GitHub Desktop on Ubuntu. This involves the following steps:


## Installation Using Debian Package

A developer named **Brendan Forster** has created an unofficial version of GitHub Desktop for Linux users. We will use this to install GitHub Desktop.

[![Repository](assets/post/git/3.png){: .w-75 .shadow .rounded-10 }](https://github.com/shiftkey/desktop)click image to visit repository

Click on the area indicated in the image. The latest release as of now is 3.3.8 RC2. Select the latest release at the time of your installation.

Download the `*.deb` package suitable for your architecture. If you are using a different architecture or a system not based on Debian like Ubuntu, you should download the file appropriate for your system.

![Package](assets/post/git/4.png){: .w-75 .shadow .rounded-10 }

Navigate to the directory where the package was downloaded using the terminal, and then use `apt` to perform the installation.

![Install](assets/post/git/5.PNG){: .w-75 .shadow .rounded-10 }

```bash
# Check the filename of the downloaded package
ls

# Perform the installation
sudo apt install ./GitHubDesktop-linux-amd64-3.3.8-linux2.deb 
```
After completing the installation, you can use the GitHub Desktop client normally.

![Run](assets/post/git/6.PNG){: .w-75 .shadow .rounded-10 }

> Please note that the installation environment mentioned here is based on Ubuntu 23.10, release 3.3.8 RC2. The installation method may change with future improved releases.
{: .prompt-warning }
