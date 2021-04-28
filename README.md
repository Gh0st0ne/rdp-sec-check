# rdp-sec-check to get RDP service security settings

The rdp-sec-check tool checks which encryption algorithms and authentication methods are used, as well as some other security settings. At the end of the check, rdp-sec-check summarizes the potential security issues of the Remote Desktop Service.

Install rdp-sec-check on Kali Linux

```
sudo cpan
install Encoding::BER
Ctrl+d
wget https://raw.githubusercontent.com/portcullislabs/rdp-sec-check/master/rdp-sec-check.pl
chmod +x rdp-sec-check.pl
./rdp-sec-check.pl --help
```
 
 The command to run is very simple:
 
```
rdp-sec-check HOST
```
For example:

```
rdp-sec-check 192.168.0.101
```

In the screenshot you can see the security methods used on the remote RDP server. You can see that after the line [+] Summary of security issues there is nothing, then there are no obvious problems.

Let's check another, less secure host:

```
rdp-sec-check 192.168.0.89
```

Here we see the following RDP server security issues:

```
[+] Summary of security issues

[-] 192.168.0.89:3389 has issue NLA_NOT_SUPPORTED_DOS
[-] 192.168.0.89:3389 has issue SSL_SUPPORTED_BUT_NOT_MANDATED_MITM
```

They say that NLA is not used and therefore a DOS attack is possible. I’ll add from myself that if the NLA is not used, then a man-in-the-middle attack is also possible. It is further stated that SSL is supported, but not required, which makes the MITM (man-in-the-middle) attack possible. 
