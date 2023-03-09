# Subdomain enumeration




# Directory enumeration

gobuster in directory/file mode

```bash
gobuster dir --url http://10.123.32.1/ --wordlist=/usr/share/dirbuster/wordlists/directory-list-1.0.txt
```

Look for specific extensions

```bash
gobuster dir --url http://10.123.32.1/ --wordlist=/usr/share/dirbuster/wordlists/directory-list-1.0.txt -x php,js
```
