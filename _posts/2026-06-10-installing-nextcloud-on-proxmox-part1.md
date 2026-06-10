---
layout: default
title: Installing Nextcloud on Proxmox (part 1)
date: 2026-06-10
categories: Software
---

# Installing Nextcloud on Proxmox (part 1)

Today we are going to install Nextcloud on Proxmox on a Linux Ubuntu VM.

## 1. Preparing Ubuntu ISO image on Proxmox

Because we are starting from a fresh Proxmox server we first have to download the ISO image that serves as the base OS.

- Login to Proxmox web interface
- Click local > ISO Images > Download from URL
- Then paste the URL > Query URL > Download

```
https://releases.ubuntu.com/26.04/ubuntu-26.04-live-server-amd64.iso
```

## 2. Creating the VM

From within the Proxmox web interface:

- Click button: Create VM
- Name: nextcloud01
- Start at boot: YES
- ISO Image: Choose the Ubuntu 26.04 image from step 1
- System: Qemu agent: YES
- Disk 1: 50 GB for OS (I chose 100G B)
- Disk 2: 500+ GB for data (I chose 2048 GB)
- CPU: 4 cores
- Memory: 8192 MB (8 GB)

Creating the VM can take a while, I am going to get myself a coffee :)

## 3. Ubuntu 26.04 installation

After creating the VM we have to go through the Ubuntu installation wizard.

(I needed to lower my memory setting because my proxmox host did not have enough memory available to start the VM)

Stick to the defaults unless mentioned:

- Start the VM
- Select language, keyboard layout, etc.
- I configured a static IP but you can also just use DHCP and make it static in your router
- Choose your OS disk, not your data disk!
- Install OpenSSH server
- Do not install any snap packages!

That's it for now, your server is ready for Nextcloud installation in part 2.
