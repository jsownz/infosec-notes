# Enumeration

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
