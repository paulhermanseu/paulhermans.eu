---
layout: default
title: Starting my Homelab
date: 2026-06-09
categories: Software
---

# Starting my Homelab

For years I had ideas for my own Homelab to host my own stuff instead of paying for third party services.

Today I made a start with this idea.

## 1. Getting the hardware

My old office pc with Intel cpu 4 cores, 8GB RAM, 1TB SSD and a 4TB HDD is my starting device.

With a 1000mbit network interface this will be ok.

## Power Usage

I tested the power usage of this PC to see if it's not too much:

- PC idle = 20 ~ 30 watt
- 100% cpu = 60 ~ 65 watt

Pretty good I would say.

## 2. Installing Proxmox

Downloaded [Proxmox VE (Virtual Environment)](https://proxmox.com/en/downloads) and put it on a USB stick.

From my Linux Zorin OS desktop I used Gnome Disks (Disks from the start menu) and option "Restore Disk Image..."

Boot up and follow instructions, use your favorite AI chat if you have questions 

## Why Proxmox?

I want to be able to host multiple servers on this pc => Virtualization

- Migrate a server to another Proxmox pc for easy maintenance
- Quick restore when a server fails
- Proxmox Backup Server for backup procedure

## What software am I planning to run?

I want to test with the following software:

- AdGuard (DNS and DHCP)
- TrueNAS for general File Storage
- Home Assistant + Music Assistant
- Immich for photos (Get rid of Google Photos)
- NextCloud for files (Get rid of Dropbox)
- Jellyfin for video streaming
- Tailscale VPN
- Project NOMAD

The old office PC will not be able to run all of this but we will start anyway.
