---
layout: default
title: Cross Platform USB Sticks
date: 2026-06-15
categories: Software
---

# Working with USB Sticks (on Linux and Windows)

Today I'm collecting all my USB sticks, check what data is on them, erase, format and throw the old ones away.

Also ordered a few new USB sticks, one 64GB and one 256GB.

## What filesystem to use? exFAT

When formatting a USB Stick to use on Linux and Windows what filesystem do you choose?

**ext4** Not supported on Windows  
**NTFS** Needs extra packages on Linux (apt install ntfs-3g)  
**FAT32** No, limited to 32GB disks and 4GB filesize  
**exFAT** YES!

## Using exFAT on Linux ZorinOS

Reading a USB stick with an exFAT filesystem is natively supported.

But the tools to format an USB stick with exFAT are not installed by default.

From the Terminal:
```
sudo apt install exfatprogs
```

Then you can use Gnome Disks to format your stick.

- Start menu > Disks
- Choose your USB disk
- Click on the gears icon for ¨Additional partition options¨
- Format partition...
- Type = Other
- Choose exFAT (Flash Storage Windows Filesystem, used on SDXC cards)
- Next, Format

## What about cross platform Disk Encryption?

Losing a USB stick with important documents is a nightmare, you need Disk Encryption!

But what if your USB stick travels between Linux and Windows PC's?

### LUKS? No

LUKS is the native Linux disk encryption software.

Not supported in Windows. Readable on Windows via WSL2 (Windows Subsystem for Linux), not easy!

### Bitlocker? Nah

Bitlocker is the Microsoft counterpart for Pro/Enterprise, not supported on Windows Home edition. 

Readable on Linux via ***dislocker***.

### Veracrypt? Mwah

Open-source and cross-platform (Linux, Windows, macOS). Works as an encrypted container or full disk encryption.

VeraCrypt looks dated and intimidating. Not available in default ZorinOS software repositories.

### Cryptomator? No, but looks promising

Open-source, Modern, clean interface, cross-platform (Linux, Windows, macOS, even mobile).

Cryptomator looks promising, install easy on ZorinOS via the GUI.

Originally designed for cloud storage, [cannot select my USB stick in the GUI :(](https://community.cryptomator.org/t/cryptomator-doesnt-see-any-aditional-disk-usb-external-hard-drive/11059)

You can use on Linux, but you have to copy from USB to your PC to unlock in the GUI.

Have a look at <cryptomator.org>

### Conclusion

There is no perfect solution yet for encrypted USB sticks that works seamlessly across Linux and Windows without compromises.


## Erasing a USB Stick on Linux ZorinOS (Terminal)

Use ***lsblk*** to determine which device is your USB stick.

```
paul@Linux:~$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda      8:0    0 238,5G  0 disk 
├─sda1   8:1    0   350M  0 part 
├─sda2   8:2    0 237,5G  0 part 
├─sda3   8:3    0   100M  0 part /boot/efi
└─sda4   8:4    0   509M  0 part 
sdb      8:16   0   3,6T  0 disk 
├─sdb1   8:17   0    16M  0 part 
└─sdb2   8:18   0   3,6T  0 part 
sdc      8:32   0 223,6G  0 disk 
├─sdc1   8:33   0   526M  0 part 
├─sdc2   8:34   0   512M  0 part 
├─sdc3   8:35   0     1K  0 part 
└─sdc5   8:37   0 222,6G  0 part /
sdd      8:48   0   1,9G  0 disk 
└─sdd1   8:49   0   1,9G  0 part /media/paul/USB DISK
sr0     11:0    1  1024M  0 rom
```

Then use ***shred*** to erase the disk.

-v => verbose
-n 1 => write one cycle of random values
-z => write all zeros

```
paul@Linux:~$ sudo shred -v -n 1 -z /dev/sdd
[sudo] password for paul:          
shred: /dev/sdd: pass 1/2 (random)...
shred: /dev/sdd: pass 1/2 (random)...25MiB/1,9GiB 1%
shred: /dev/sdd: pass 1/2 (random)...68MiB/1,9GiB 3%
shred: /dev/sdd: pass 1/2 (random)...1,9GiB/1,9GiB 100%
shred: /dev/sdd: pass 2/2 (000000)...
shred: /dev/sdd: pass 2/2 (000000)...27MiB/1,9GiB 1%
shred: /dev/sdd: pass 2/2 (000000)...72MiB/1,9GiB 3%
shred: /dev/sdd: pass 2/2 (000000)...1,9GiB/1,9GiB 100%
```

Well this takes a long time, if you are going to throw them away it's easier to physically destroy them.

