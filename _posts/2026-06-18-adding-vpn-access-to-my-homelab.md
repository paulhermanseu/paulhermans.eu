---
layout: default
title: Adding VPN access to my Homelab
date: 2026-06-09
categories: Homelab, Software
---

# Adding VPN access to my Homelab

Today I wanted to connect my home network to a VPN network so I can access my homelab servers from abroad.

You can do this with an oldskool VPN but choosing for a VPN tunneling software is way easier and more flexible.

## Why I did not choose Tailscale

Tailscale is the most famous brand in this field, based in Canada.

But starting to create an account with Tailscale became already a problem for me.

You cannot simply create an account on the Tailscale website, they outsource this to external login services like Google, Microsoft, Github, Apple, etc.

Because I do not want to rely on Big Tech companies for my Tailscale account this is not an option.

I tried OIDC (OpenID Connect) with my [codeberg.org](https://codeberg.org/) account but could not get it to work.

The only European option seems to be to host your own OpenID service, I did not want to setup my own OpenID Connect server just to create a Tailscale account.

## Tailscale alternatives

So I had to look for Tailscale alternatives:

- NetBird (Open-source, [built in Europe](https://netbird.io/careers)
- Headscale (Open-source, self-hosted, Tailscale clients compatible)
- Twingate (USA)
- Netmaker (USA)
- ZeroTier (USA)

## Choosing NetBird over Tailscale

The choice for NetBird was easy: build in Europe, open-source and [a free cloud option](https://netbird.io/pricing).

## 1. Create NetBird account

Go to [app.netbird.io](https://app.netbird.io/) and create your NetBird account using your email address (do not sign up using third party services).

## 2. Install NetBird client app

Go to the app store (Android, IOS) of your phone and install the NetBird app, login with your NetBird account and your first device is connected!

## 3. Install NetBird on my Proxmox

Then the more complicated stuff.

### Prepare NetBird container

- Login Proxmox
- Create CT
- I chose default options, debian 13 container with static IP address.

My container ID = 108

Now go to the Shell of the server and to this:

```
# Edit configuration of container
nano /etc/pve/lxc/108.conf

# Add these two lines at the bottom:
lxc.cgroup2.devices.allow: c 10:200 rwm
lxc.mount.entry: /dev/net dev/net none bind,create=dir

# Start container
pct start 108

# Login container
pct enter 108

# Inside container
apt update && apt upgrade -y && apt install curl -y
```

### Connect Server to NetBird cloud

Follow the instructions from NetBird to install and add your server:

- Login to Netbird
- Peers > Server > Add Peer
- Install software:

```
curl -fsSL https://pkgs.netbird.io/install.sh | sh
```

- Click "Generate Key"
- Copy link to server: netbird up --setup-key SETUP_KEY

### Make your home network available for clients

- Login to NetBird
- Network Routing > Networks > Add Network
- Follow the Wizard add your Home network subnet (for example 192.168.1.0/24)
- Create a policy which devices can connect
- Add Routing Peer = server

## 4. Try it out

Now disable your WiFi on your phone and try to access your proxmox webinterface in the browser of your phone.

It works! Amazing! :)
