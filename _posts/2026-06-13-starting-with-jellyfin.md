---
layout: default
title: Starting with Jellyfin
date: 2026-06-13
categories: Software
---

# Starting with Jellyfin

A friend of my showed me his Jellyfin system a few years ago and ever since I was convinced I wanted to build my own.

Today is that day.

We are going to install Jellyfin on our Proxmox server as a LXC container.

## What is Jellyfin

Jellyfin is a free, open-source media server to stream your media to your TV and other devices, (serving as an alternative to proprietary services like **Plex**).

Have a look at [jellyfin.org](https://jellyfin.org/)

## 1. Create Jellyfin container

- Login to your Proxmox webinterface
- Open the Proxmox shell (Datacenter > node > Shell)
- Run the helper script

```
bash -c "$(wget -qLO - https://github.com/community-scripts/ProxmoxVE/raw/main/ct/jellyfin.sh)"
```

Follow the prompts

- Default or Advanced settings
- Container ID, hostname, disk size (default: 8GB)
- RAM (default: 2048MB), CPU cores
- Network settings (DHCP or static IP)

## 2. Adding data disk

We are going to add our data disk.

Our datadisk lives under /mnt/data and our container ID = 105.

```
# Make a media directory
mkdir /mnt/data/media

# Open the jellyfin container config file
nano /etc/pve/lxc/105.conf

# Add this to the bottom of the file:
mp0: /mnt/data/media,mp=/media

# reboot container
pct reboot 105

# login to container
pct enter 105

# ls /media folder inside container
ls /media

# Make these directories:
mkdir /media/movies
mkdir /media/shows
```

## 4. Directory structure

Jellyfin expect these directory structures:

```
movies/
  └── Movie Name (2024)/
      └── Movie Name (2024).mkv

shows/
  └── Show Name/
      └── Season 01/
          ├── Show Name S01E01.mkv
          └── Show Name S01E02.mkv
```

Keeping the naming consistent helps Jellyfin's metadata scraper match everything correctly.

## 3. Login Jellyfin webinterface

Jellyfin will be available at:

http://container-ip:8096

Work through the first time wizard and add your folders /media/movies

## 4. How to access your media folders?

To make your media folder accessable on the network we are going to run a second container with Samba for a SMB network share.

## 5. Create Samba container




