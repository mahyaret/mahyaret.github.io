---
layout: post
title: NFS on Windows
date: '2025-08-06T01:10:00.002-04:00'
author: Mahyar
tags:
- linux
- photography
---

I'm editing my photos directly from my NAS, and I’ve found that NFS, with its smaller overhead, performs better than Samba—even on Windows.

On the Linux part - make sure your NFS Server Configuration is correct:
- `sudo chmod -R 775 /srv/nfs/shared`
- `sudo apt install nfs-kernel-server`
- `sudo apt install nfs-common`
- edit `/etc/exports`
- add `/srv/nfs/shared *(rw,sync,no_subtree_check,no_root_squash)`
- `sudo systemctl start nfs-server`
- `sudo systemctl enable nfs-server`
- use `id` to get the UID and GID of the user you plan to use
- edit the default config: `/etc/default/nfs-kernel-server`
- change: `RPCMOUNTDOPTS="--port 13025"`
- edit or create `/etc/modprobe.d/lockd.conf`
- change: `options lockd nlm_tcpport=13026 nlm_udpport=13027`
- `sudo reboot`
- get the proper ports with `rpcinfo -p`
- for ufw:
    - `sudo ufw allow from 192.168.0.0/24 to any port 111`
    - `sudo ufw allow from 192.168.0.0/24 to any port 13025`
    - `sudo ufw allow from 192.168.0.0/24 to any port 13026`
    - `sudo ufw allow from 192.168.0.0/24 to any port 2049`

On the windows part:
- Press `Windows + S` and type `Turn Windows features on or off`, then select it.
- In the Windows Features dialog box, locate `Services for NFS`.
- Expand `Services for NFS` and check both `Client for NFS` and `Server for NFS`.
- Click `OK` and wait for the features to be installed.
- you now need to match the UID and GID that pulled earlier (1001 in the linux part example) on both the Server and the Client
- regedit to `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ClientForNFS\CurrentVersion\Default`
- You will need to make two new DWORD (32-bit) entries by right clicking inside the Default key. They should be named “AnonymousGid” and “AnonymousUid”. They should both have a decimal value matching your user’s GID and UID that you got earlier (1001 in the example)
- restart NFS service on the Windows Client side by using:
- `nfsadmin client HOSTNAME config casesensitive=yes`
- `nfsadmin client HOSTNAME stop`
- `nfsadmin client HOSTNAME start`
- run `cmd` as administrator, make your mount: `mount -o anon \\192.168.0.3\srv\nfs\shared X:`
- right click `This PC` and click on `Map network drive...`
- select `X` for Drive.
- enter `\\192.168.0.3\srv\nfs\shared` for Folder

Bonus

- `sudo mkdir /Volumes/cloud`
- `sudo mount -t nfs -o vers=3,resvport cloud:/media/storage/shared /Volumes/cloud`
