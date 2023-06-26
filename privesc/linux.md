## Enumeration Scripts

[Linpeas](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS) is a super comprehensive and commonly used script to identify possible priv-esc vectors.

## setuid bit

The setuid bit simply indicates that when running the executable, it will set its permissions to that of the owner, instead of setting it to the user who launched it.

We can search for all files with the bit set with

```bash
www-data@50bca5e748b0:/var/www/html$ find / -perm -u=s -type f 2>/dev/null
```

It's worth checking the results against [GTFOBins](https://gtfobins.github.io/).

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