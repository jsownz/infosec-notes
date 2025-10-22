---
icon: magnifying-glass
---

# Enumeration

#### DNS

```sh
dnsenum --dnsserver [target ip] --enum -p 0 -s 0 -o subdomains.txt -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt [TLD domain]
```

```sh
dnsrecon -r [range] -n [dns host ip] -d [domain]
```

* range should be the network, so something like 127.0.0.0/24 when on the same network
* `-d` is not really useful here but it a needed flag - can flll with garbage

***

#### Nmap

* network scan
  * `sudo nmap [CIDR ADDR] -sn -oA tnet | grep for | cut -d" " -f5`
  * using list of hosts
    * `-iL [host list]`
* `-sT` is the most stealthy scan, as it uses the entire TCP handshake to check ports
* `-sA` to bypass many IPS and IDS
* `-Pn` disable ping
* `-sU` UDP scan
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

```sh
smbclient -N -L //[target ip]
```

```sh
crackmapexec smb [target ip] --shares -u '' -p ''
```

```sh
smbmap -H [target ip]
```

* can add directory recursion with `-r --depth [num]`
* can pass the hash with -p (password or hash)

```sh
rpcclient -U "" [target ip]
```

```sh
smbget -R //[target ip]/[share name]
```

```sh
enum4linux-ng [target ip]
```

***

#### SMTP

```sh
smtp-user-enum -U [username file] -M VRFY -t [target ip] -D [domain]
```

***

#### SNMP

```sh
snmpwalk -v2c -c [community string] [target ip] 
```

```sh
onesixtyone -c /usr/share/wordlists/seclists/Discovery/SNMP/snmp.txt [target ip]
```

```sh
braa [community string]@[target ip]:.1.3.6.*
```

***

#### SSL Certs

* [crt.sh](https://crt.sh/) to get cert information (goes down often)

```sh
curl -s https://crt.sh/\?q\=[domain]\&output\=json | jq .
```

* Pipe this string of commands to grep, cut and awk the unique domain names

```sh
grep name | cut -d":" -f2 | grep -v "CN=" | cut -d'"' -f2 | awk '{gsub(/\\n/,"\n");}1;' | sort -u
```

* Example: find all dev subdomains on facebook.com:

```sh
curl -s "https://crt.sh/?q=facebook.com&output=json" | jq -r '.[]
 | select(.name_value | contains("dev")) | .name_value' | sort -u
```

* [https://search.censys.io/](https://search.censys.io/)

