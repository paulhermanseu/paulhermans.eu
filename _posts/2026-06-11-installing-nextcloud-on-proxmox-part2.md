---
layout: default
title: Installing Nextcloud on Proxmox (part 2)
date: 2026-06-11
categories: Software
---

# Installing Nextcloud on Proxmox (part 2)

In [part 1 of this blog series](https://www.paulhermans.eu/software/2026/06/10/installing-nextcloud-on-proxmox-part1.html) we prepared an Ubuntu 26.04 server with a second disk on **/mnt/datadisk**.

Today we are going to install Nextcloud.

SSH into your server to get started.

## 1. Install docker

First we have to install docker because Nextcloud needs it.

See the [Docker documentation](https://docs.docker.com/engine/install/ubuntu/#installation-methods)

For lazy people do this:

```
# Download and execute the Docker installer script
curl -fsSL https://get.docker.com | sudo sh

# Add our user to the docker group
sudo usermod -aG docker $USER

# Verify installation
docker --version

# Logout and login again to activate the docker group for our user
logout
```

## 2. Install Nextcloud

Ok now we are going to install Nextcloud:

```
# Prepare working folder
mkdir ~/nextcloud && cd ~/nextcloud

# Download compose.yaml template
curl -o compose.yaml https://raw.githubusercontent.com/nextcloud/all-in-one/main/compose.yaml

# Edit compose.yaml
nano compose.yaml
```

We need to configure our datadisk, uncomment and edit these two lines:

```
environment:
 NEXTCLOUD_DATADIR: /mnt/datadisk
```

Save and exit

```
docker compose up -d
docker compose logs -f
```

## 3. Login to Nextcloud

Open your browser and login to **https://internal.ip.of.this.server:8080**

That's it for now, configuring Nextcloud in the third part of the series.
