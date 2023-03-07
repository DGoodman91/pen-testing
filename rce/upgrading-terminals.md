# Upgrading a dumb terminal to an interactive one

## Using python

Use python to upgrade a dumb terminal to an interactive shell

```python
python -c 'import pty;pty.spawn("/bin/bash")'
```

# Adding autocomplete

If we have a functional terminal with prompt and cursor, but don't yet have autocomplete or command history, we can upgrade to a fully functional one.

* Send the dumb shell to the background with CTRL+Z
* Grab the details of our own terminal - note the row and column counts
```bash
~$ echo $TERM
xterm-256color

~$ stty -a
speed 38400 baud; rows 65; columns 115; line = 0;
intr = ^C; quit = ^\; erase = ^H; kill = ^U; eof = ^D; eol = <undef>; eol2 = <undef>; swtch = <undef>; start = ^Q;
stop = ^S; susp = ^Z; rprnt = ^R; werase = ^W; lnext = ^V; discard = ^O; min = 1; time = 0;
-parenb -parodd -cmspar cs8 -hupcl -cstopb cread -clocal -crtscts
-ignbrk -brkint -ignpar -parmrk -inpck -istrip -inlcr -igncr icrnl -ixon -ixoff -iuclc -ixany -imaxbel iutf8
opost -olcuc -ocrnl onlcr -onocr -onlret -ofill -ofdel nl0 cr0 tab0 bs0 vt0 ff0
isig icanon iexten echo echoe echok -echonl -noflsh -xcase -tostop -echoprt echoctl echoke -flusho -extproc

```

Set the input mode to raw, allowing us to tab, up/down, and preventing e.g. CTRL+C from ending the process ([more details](https://stackoverflow.com/questions/22832933/what-does-stty-raw-echo-do-on-os-x))
```bash
stty raw -echo
```

Bring the remote shell to the foreground and reset it (note that after *stty raw* your key inputs aren't visible), and set the terminal type to match our own
```bash
fg
reset

reset: unknown terminal type unknown
Terminal type? xterm-256color

# if the color terminal is unavailable, use plain xterm
# reset: unknown terminal type xterm-256color
# Terminal type? xterm
```

Set up the environment

```bash
~$ export TERM=xterm
~$ export SHELL=bash
~$ stty rows 65 columns 115 # match ours from above
```

