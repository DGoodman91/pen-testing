# Volatility3 for mem dump analysis

Get a list of running processes

```bash
python3 vol.py -f dump.raw windows.pslist
```

or get it in tree format

```bash
python3 vol.py -f dump.raw windows.pstree
```

Examine a specific process

```bash
python3 vol.py -f dump.raw  -o procdump.out windows.dumpfiles –pid 1234
```

List files and recover from memory

```bash
~$ python3 vol.py -f dump.raw windows.filescan
Volatility 3 Framework 2.4.2
Progress:  100 PDB scanning finished                                                                                                                                                                                                                                
Offset  Name    Size
0x103510        \Windows\System32\fdPnp.dll     128           
0x1438f8        \keysvc 128                                    
0x1439b0        \keysvc 128                                                           
0x1a9640        \Windows\System32\EhStorAPI.dll 128      
0x1a9980        \Windows\System32\spfileq.dll   128

~$ python3 vol.py -f dump.raw windows.dumpfiles --physaddr 0xbbf6158
```

Get a list of tcp connections

```bash
python3 vol.py -f dump.raw windows.netscan
```

Look for injected code

```bash
python3 vol.py -f dump.raw windows.malfind
```

## Links

https://book.hacktricks.xyz/generic-methodologies-and-resources/basic-forensic-methodology/memory-dump-analysis/volatility-cheatsheet

https://cryptome.org/0003/RAMisKey.pdf


