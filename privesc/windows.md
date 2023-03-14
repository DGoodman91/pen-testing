# Windows privilege escalation

## Common

List current user's privileges with

```shell
dave@MYCOMPUTER C:\Users\dave\Desktop>whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                    State
============================= ============================== =======
SeChangeNotifyPrivilege       Bypass traverse checking       Enabled
SeIncreaseWorkingSetPrivilege Increase a process working set Enabled
```

List scheduled tasks with

```shell
schtasks
```

Check current processes with

```shell
powershell -c ps
```

## winpeas

