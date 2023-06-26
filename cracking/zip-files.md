# John The Ripper

Grab the zip file's password hash

```bash
~$ zip2john backup.zip > hash.out
ver 2.0 efh 5455 efh 7875 backup.zip/index.php PKZIP Encr: 2b chk, TS_chk, cmplen=1201, decmplen=2594, crc=3A41AE06
ver 2.0 efh 5455 efh 7875 backup.zip/style.css PKZIP Encr: 2b chk, TS_chk, cmplen=986, decmplen=3274, crc=1B1CCD6A
NOTE: It is assumed that all files in each archive have the same password.
If that is not the case, the hash may be uncrackable. To avoid this, use
option -o to pick a file at a time.

~$ cat hash.out 
backup.zip:$pkzip2$2*2*1*0*8*24*3a41*5722*543fb39ed1b97ad04bb562db282c223667af8ad907466b88e7052072d6968acb7258fb8846da057b1448a2a9699ac0e5592e369fd6e87d677a1fe91c0d0155fd237bfd2dc49*$/pkzip2$::backup.zip:style.css, index.php:backup.zip
```

Crack with john

```bash
~$ john hash.out  --show
backup.zip:741852963::backup.zip:style.css, index.php:backup.zip

1 password hash cracked, 0 left
```


Speciy a wordlist

```bash
john -wordlist=/usr/share/wordlists/rockyou.txt hash.out
```

# Known-Plaintext Attacks

If it's not possible to brute force the password in sensible time using a wordlist, and the ZIP file is encrypted with the older encryption scheme (ZipCrypto) rather than the newer AES scheme, then we may be able to use a plain-text attack to recover the contents and/or password.

https://github.com/kimci86/bkcrack

We just need to know 12 or more bytes of the unencrypted plaintext. This is considerably easier if there are files within the archive that are not compressed (compression type Store), since otherwise we need to guess the pre-encryption compressed plaintext. 