# Enumeration

#### DNS

```shell-session
dnsenum --dnsserver [target ip] --enum -p 0 -s 0 -o subdomains.txt -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt [TLD domain]
```

***

#### Nmap

* network scan
  * `sudo nmap [CIDR ADDR] -sn -oA tnet | grep for | cut -d" " -f5`
  * using list of hosts
    * `-iL [host list]`
* `-sT` is the most stealthy scan, as it uses the entire TCP handshake to check ports
* `-sA` to bypass many IPS and IDS
* `-Pn` disable ping
* `-n` disable DNS resolution
* `--disable-arp-ping` disable ARP ping, good for investigating further
* `--packet-trace` get more info on send and recv
* `--reason` get more info on the port state
* `-D` decoy - nmap inserts random IPs in the IP header of the scans
* `--source-port` specify a source port, often 53 to slide through dns port
  * can also specify this in netcat when connecting to a port

***

#### NFS

* list mounts:
  * `showmount -e [ip]`
* mount share:
  * `mount -t nfs -o nolock [ip]:[share] /mnt`

***

#### SMB

SMB shares can be enumerated many ways

```
smbclient -N -L //[target ip]
```

```
crackmapexec smb [target ip] --shares -u '' -p ''
```

```
smbmap -H [target ip]
```

* can add directory recursion with `-r --depth [num]`
* can pass the hash with -p (password or hash)

```
rpcclient -U "" [target ip]
```

```
smbget -R //[target ip]/[share name]
```

```
enum4linux-ng [target ip]
```

***

#### SMTP

```
smtp-user-enum -U [username file] -M VRFY -t [target ip] -D [domain]
```

***

#### SNMP

```shell-session
snmpwalk -v2c -c [community string] [target ip] 
```

```shell-session
onesixtyone -c /usr/share/wordlists/seclists/Discovery/SNMP/snmp.txt [target ip]
```

```
braa [community string]@[target ip]:.1.3.6.*
```

***

#### SSL Certs

* crt.sh to get cert information (goes down often)

```shell-session
curl -s https://crt.sh/\?q\=[domain]\&output\=json | jq .
```

* Add this string of commands to grep, cut and awk the unique domain names

```shell-session
grep name | cut -d":" -f2 | grep -v "CN=" | cut -d'"' -f2 | awk '{gsub(/\\n/,"\n");}1;' | sort -u
```
