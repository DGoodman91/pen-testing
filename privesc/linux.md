## Enumeration Scripts

[Linpeas](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS) is a super comprehensive and commonly used script to identify possible priv-esc vectors.

## Common

List your user's sudo priveleges with

```bash
~$ sudo -l
```

Also check for permit-nopass rules in the **doas.conf** file if it exists.

The rule

```shell
# /etc/doas.conf or /usr/local/etc/doas.conf
permit nopass player as root cmd /usr/bin/dstat
```

allows us to run

```shell
doas /usr/bin/dstat
# OR
doas /usr/bin/dstat --some-args
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