# Common enum stuff run on remote host

## Services

* Check what services are listening

```bash
# -n flag switches off auto service identification, e.g. displaying :22 as :ssh
~$ ss -tln
State       Recv-Q      Send-Q                 Local Address:Port              Peer Address:Port      Process      
LISTEN      0           50                [::ffff:127.0.0.1]:35951                        *:*                      
LISTEN      0           50                [::ffff:127.0.0.1]:8080                         *:* 
```