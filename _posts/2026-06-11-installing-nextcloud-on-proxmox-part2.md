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
```

## 2. Prepare Nextcloud user, group, directory

Prepare the foundations for Nextcloud installation:

```
# Create dedicated system user and group
sudo useradd --system --no-create-home --shell /usr/sbin/nologin nextcloud

# Add nextcloud user to the docker group
sudo usermod -aG docker nextcloud

# Prepare nextcloud installation folder
sudo mkdir /opt/nextcloud

# Set correct ownership
sudo chown -R nextcloud:nextcloud /opt/nextcloud
sudo chmod 750 /opt/nextcloud
```

## 3. Prepare Nextcloud configuration

Download the Nextcloud configuration template and edit it:

```
# Change directory
cd /opt/nextcloud

# Download compose.yaml template
sudo -u nextcloud curl -o compose.yaml https://raw.githubusercontent.com/nextcloud/all-in-one/main/compose.yaml

# Edit compose.yaml
sudo nano compose.yaml
```

Enable hardware acceleration and configure our datadisk, uncomment and edit these lines:

```
devices: ["/dev/dri"]

environment:
 NEXTCLOUD_DATADIR: /mnt/datadisk
```

Save and exit nano.

## 4. Prepare Nextcloud system service

To run Nextcloud under the nextcloud system user we create a system service:

```
# Create systemd service
sudo nano /etc/systemd/system/nextcloud.service
```

nextcloud.service content:
```
[Unit]
Description=Nextcloud AIO
Requires=docker.service
After=docker.service network-online.target
Wants=network-online.target

[Service]
Type=oneshot
RemainAfterExit=yes
User=nextcloud
Group=nextcloud
WorkingDirectory=/opt/nextcloud
ExecStart=/usr/bin/docker compose up -d
ExecStop=/usr/bin/docker compose down
TimeoutStartSec=300

[Install]
WantedBy=multi-user.target
```

Save and exit nano.

## 5. Run nextcloud

Enable and start the nextcloud service.

```
# Let systemd find the new service
sudo systemctl daemon-reload

# Enable and start the service
sudo systemctl enable nextcloud.service
sudo systemctl start nextcloud.service

# Verify Nextcloud is running
sudo systemctl status nextcloud.service
```

## 6. Access docker commands

To access the docker logs and other commands:

```
# Change directory to where the compose.yaml file is
cd /opt/nextcloud

# Check the logs
docker compose logs

# Check the logs and keep following
docker compose logs -f

# See which containers are running
docker compose ps
```


## 6. Login to Nextcloud

Open your browser and login to **https://internal.ip.of.this.server:8080**

That's it for now, configuring Nextcloud in the third part of the series.
