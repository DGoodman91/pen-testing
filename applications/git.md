## Git Dumper

If we suspect a webserver has missing/misconfigured access rules, we can try dumping the git repository with

```bash
git-dumper http://10.10.123.321/ ./output-directory/
```

[Git Dumper](https://github.com/arthaud/git-dumper) actually reconstructs the source from the .git directory, so it's easy to navigate.