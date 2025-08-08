---
layout: post
title: (WIP) NFS on Windows
date: '2025-08-06T01:10:00.002-04:00'
author: Mahyar
tags:
- linux
- photography
---

On the Linux part - make sure your NFS Server Configuration is correct:

    nfs-utils and nfs-utils-lib should be installed

    rpcbind, nfs-server, nfs-lock, nfs-idmap should be enabled

    rpcbind, nfs-server, nfs-lock, nfs-idmap should be started

    Choose the directories you want to share

    make sure your user can access everything inside his directory

    get the UID and GID of the user you plan to use

    get the IP address of your Windows 10 NFS client

    edit the exports file (etc/exports) and add the user you will use to it: /home/user   192.168.1.2(rw,sync,root_squash,all_squash,anonuid=1001,anongid=1001) - note: the IDs are the ones obtained previously

    restart the service with systemctl restart nfs-server

    get the proper ports with rpcinfo -p

    add them to the firewall

On the windows part:

    make sure you installed Client for NFS

    you now need to match the UID and GID that pulled earlier (1001 in the linux part example) on both the Server and the Client

    regedit to HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ClientForNFS\CurrentVersion\Default

    You will need to make two new DWORD (32-bit) entries by right clicking inside the Default key. They should be named “AnonymousGid” and “AnonymousUid”. They should both have a decimal value matching your user’s GID and UID that you got earlier (1001 in the example)

    restart NFS service on the Windows 10 Client side by using :

    nfsadmin client HOSTNAME config casesensitive=yes

    nfsadmin client HOSTNAME stop

    nfsadmin client HOSTNAME start

    finally, make your mount: mount -o anon \\192.168.1.3\home\storage\ X:


for ufw:
sudo ufw allow from 192.168.0.0/24 to any port 111
sudo ufw allow from 192.168.0.0/24 to any port 13025
sudo ufw allow from 192.168.0.0/24 to any port 13026
sudo ufw allow from 192.168.0.0/24 to any port 13027
sudo ufw allow from 192.168.0.0/24 to any port 2049
Thanks for checking — it looks like **`mountd` was successfully locked to port 13025**, but **`nlockmgr` and `statd` are still using dynamic ports**. That’s expected unless you explicitly lock them too.

Let’s finish the job by **locking `nlockmgr` and `statd`** ports properly.

---
 Lock mountd:

Edit the default config:

sudo nano /etc/default/nfs-kernel-server

RPCMOUNTDOPTS="--port 32767"

## ✅ Step 1: Lock `nlockmgr` ports

This is done via a kernel module parameter.

### Edit or create:

```bash
sudo nano /etc/modprobe.d/lockd.conf
```

Add:

```ini
options lockd nlm_tcpport=13026 nlm_udpport=13027
```

This tells the kernel to bind `nlockmgr` to port 32768 for both TCP and UDP.

> `lockd` is the kernel module that handles NFS locking via `nlockmgr`.

---

## ✅ Step 2: Lock `statd` ports

### Edit:

```bash
sudo nano /etc/default/nfs-common
```

Add or modify:

```ini
STATDOPTS="--port 32765 --outgoing-port 32766"
```

This locks:

* `statd`'s **incoming port** to `32765`
* **Outgoing lock callbacks** to `32766`

---

## ✅ Step 3: Update initramfs (for `lockd` to stick)

Since `lockd` is a kernel module, you should rebuild the initramfs:

```bash
sudo update-initramfs -u
```

Then reboot:

```bash
sudo reboot
```




