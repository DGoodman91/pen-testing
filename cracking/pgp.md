## Example: Cracking passphrase for a private key

Assume we have the public and private key, protected w/ unknown passphrase. We have a PGP-encrypted message that we wish to read.

```shell
# we have `keys`, which contains both public and private, and have split out the private key
$ cat private.key 
-----BEGIN PGP PRIVATE KEY BLOCK-----

lQUBBGK4V9YRDADENdPyGOxVM7hcLSHfXg+21dENGedjYV1gf9cZabjq6v440NA1
...
=7Uo6
-----END PGP PRIVATE KEY BLOCK-----

# check its file type to confirm
$ file private.key 
private.key: PGP private key block
```

Use john to brute force it

```shell
# convert to a john-crackable hash
$ gpg2john private > private-hash

# brute force!
$ john private-hash
Using default input encoding: UTF-8
Loaded 1 password hash (gpg, OpenPGP / GnuPG Secret Key [32/64])
Cost 1 (s2k-count) is 65011712 for all loaded hashes
Cost 2 (hash algorithm [1:MD5 2:SHA1 3:RIPEMD160 8:SHA256 9:SHA384 10:SHA512 11:SHA224]) is 2 for all loaded hashes
Cost 3 (cipher algorithm [1:IDEA 2:3DES 3:CAST5 4:Blowfish 7:AES128 8:AES192 9:AES256 10:Twofish 11:Camellia128 12:Camellia192 13:Camellia256]) is 7 for all loaded hashes
Will run 8 OpenMP threads
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Warning: Only 6 candidates buffered for the current salt, minimum 8 needed for performance.

Almost done: Processing the remaining buffered candidate passwords, if any.
Warning: Only 5 candidates buffered for the current salt, minimum 8 needed for performance.
Proceeding with wordlist:/usr/share/john/password.lst, rules:Wordlist
blink182         (Passpie)       # <---------------------------------- passphrase
1g 0:00:10:24 DONE 2/3 (2023-04-02 16:10) 0.001601g/s 87.43p/s 87.43c/s 87.43C/s hahaha..passw0rd
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

Now we have the passphrase, we can import them into a keychain

```shell
$ gpg --import --batch .keys 
gpg: directory '/home/kali/.gnupg' created
gpg: keybox '/home/kali/.gnupg/pubring.kbx' created
gpg: /home/kali/.gnupg/trustdb.gpg: trustdb created
gpg: key 387775C35745D203: public key "Passpie (Auto-generated by Passpie) <passpie@local>" imported
gpg: key 387775C35745D203: "Passpie (Auto-generated by Passpie) <passpie@local>" not changed
gpg: key 387775C35745D203: secret key imported
gpg: Total number processed: 2
gpg:               imported: 1
gpg:              unchanged: 1
gpg:       secret keys read: 1
gpg:   secret keys imported: 1
```

And finally, decrypt our encrypted message

```shell
$ cat message.enc
-----BEGIN PGP MESSAGE-----

hQEOA6I+wl+LXYMaEAP/T8AlYP9z05SEST+Wjz7+IB92uDPM1RktAsVoBtd3jhr2
...
lpF0RatbxQGWBks5F3o==uh1B
-----END PGP MESSAGE-----

$ gpg -d message.enc
gpg: encrypted with 1024-bit ELG key, ID A23EC25F8B5D831A, created 2022-06-26
      "Passpie (Auto-generated by Passpie) <passpie@local>"
p7qfAZt4_A1xo_0x # <----------------------- decrypted message
```

There's a similar example in [this CTF walkthrough](https://0xcaretaker.github.io/posts/Vault/) 