# Tunnelling

## Local port forwarding

Use ssh to forward everything sent to our local port 5432 on to 10.123.32.1's port 1234

```bash
nc -lvnp 1234
ssh -L 1234:localhost:5432 user@10.123.32.1
```