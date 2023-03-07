# nmap

## Common commands

Check TCP ports 1-1000 on a single IP for listening services and perform service identification

```bash
nmap -sV 10.123.32.1
```

Check **all** TCP ports 

```bash
nmap -p- 10.123.32.1
```

Run the default set of scripts - things like testing ftp services for anonymous login

```bash
nmap -sV -sC 10.123.32.1
```

## Links

- [Quick reference guide](https://hackertarget.com/nmap-cheatsheet-a-quick-reference-guide/)