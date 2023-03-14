# Subdomain enumeration

```bash
gobuster vhost --append-domain -w /home/kali/Documents/tools/dnscan/subdomains-10000.txt -u http://domain.net
```


# Directory enumeration

gobuster in directory/file mode

```bash
gobuster dir --url http://10.123.32.1/ --wordlist=/usr/share/dirbuster/wordlists/directory-list-1.0.txt
```

Look for specific extensions

```bash
gobuster dir --url http://10.123.32.1/ --wordlist=/usr/share/dirbuster/wordlists/directory-list-1.0.txt -x php,js
```
