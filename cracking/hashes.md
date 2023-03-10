# Hashes

Identify possible hash types with

```bash
~$ hashid 2cb42f8734ea607eefed3b70af13bbd3
Analyzing '2cb42f8734ea607eefed3b70af13bbd3'
[+] MD2 
[+] MD5 
[+] MD4 
[+] Double MD5 
[+] LM 
[+] RIPEMD-128 
[+] Haval-128 
[+] Tiger-128 
[+] Skein-256(128) 
[+] Skein-512(128) 
[+] Lotus Notes/Domino 5 
[+] Skype 
[+] Snefru-128 
[+] NTLM 
[+] Domain Cached Credentials 
[+] Domain Cached Credentials 2 
[+] DNSSEC(NSEC3) 
[+] RAdmin v2.x
```

Use hashcat and a wordlist to brute force it. -a is the attack mode (e.g. straight, brute force, wordlist + mask) and -m is the hash type (0 is md5)

```bash
hashcat -a 0 -m 0 hash.out /usr/share/wordlists/rockyou.txt
```