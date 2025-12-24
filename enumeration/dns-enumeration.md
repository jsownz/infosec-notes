---
icon: globe
---

# DNS Enumeration

## dig - DNS Zone Transfers

### Find nameservers
```bash
dig ns [domain]
dig ns [domain] @[dns-server]
```

### Attempt zone transfer (AXFR)
```bash
dig axfr @[dns-server] [domain]
dig axfr @[nameserver] [domain]
```

**Example:**
```bash
dig axfr @10.10.10.13 megacorpone.com
```

### Query specific record types
```bash
dig @[dns-server] [domain] ANY
dig @[dns-server] [domain] A
dig @[dns-server] [domain] AAAA
dig @[dns-server] [domain] MX
dig @[dns-server] [domain] TXT
dig @[dns-server] [domain] SOA
dig @[dns-server] [domain] CNAME
dig @[dns-server] [domain] NS
dig @[dns-server] [domain] PTR
```

### Reverse DNS lookup
```bash
dig -x [ip-address] @[dns-server]
```

### Short output (just the answer)
```bash
dig +short [domain]
dig +short @[dns-server] [domain]
```

### Trace DNS path
```bash
dig +trace [domain]
```

### Verbose output
```bash
dig +trace +additional [domain]
```

## dnsenum

### Basic enumeration with wordlist
{% code overflow="wrap" %}
```bash
dnsenum --dnsserver [target ip] --enum -p 0 -s 0 -o subdomains.txt -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt [TLD domain]
```
{% endcode %}

### Attempt zone transfer
```bash
dnsenum --enum [domain]
```

### Full enumeration
```bash
dnsenum [domain]
```

## dnsrecon

### Basic reconnaissance
```bash
dnsrecon -d [domain]
```

### Reverse DNS lookup for range
```bash
dnsrecon -r [range] -n [dns host ip] -d [domain]
```

* Range should be the network, so something like 127.0.0.0/24 when on the same network
* `-d` is not really useful here but it's a required flag - can fill with garbage

### Attempt zone transfer
```bash
dnsrecon -d [domain] -t axfr
```

### Zone transfer against all NS records
```bash
dnsrecon -d [domain] -a
```

### Bruteforce subdomains
```bash
dnsrecon -d [domain] -D /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -t brt
```

### Standard record enumeration
```bash
dnsrecon -d [domain] -t std
```

### Google enumeration
```bash
dnsrecon -d [domain] -t goo
```

## host

### Simple lookup
```bash
host [domain]
host [domain] [dns-server]
```

### Specific record type
```bash
host -t ns [domain]
host -t mx [domain]
host -t txt [domain]
```

### Zone transfer attempt
```bash
host -l [domain] [dns-server]
```

## nslookup

### Interactive mode
```bash
nslookup
> server [dns-server]
> set type=any
> [domain]
```

### Command line
```bash
nslookup [domain]
nslookup [domain] [dns-server]
```

### Zone transfer
```bash
nslookup
> server [dns-server]
> set type=any
> ls -d [domain]
```

## fierce

### Basic domain scan
```bash
fierce --domain [domain]
```

### With DNS server
```bash
fierce --domain [domain] --dns-servers [dns-server]
```

### Subdomain bruteforce
```bash
fierce --domain [domain] --subdomain-file /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt
```

## Zone Transfer Attack Workflow

1. **Identify DNS servers:**
```bash
dig ns [domain]
nslookup -type=ns [domain]
host -t ns [domain]
```

2. **Attempt zone transfer on each nameserver:**
```bash
dig axfr @[nameserver1] [domain]
dig axfr @[nameserver2] [domain]
```

3. **If successful, save output:**
```bash
dig axfr @[nameserver] [domain] > zone_transfer.txt
```

4. **Parse results for hosts/IPs:**
```bash
cat zone_transfer.txt | grep -E "^[a-zA-Z0-9]" | awk '{print $1}' | sort -u
```

## Subdomain Enumeration

### Using dig with wordlist
```bash
for sub in $(cat subdomains.txt); do dig +short $sub.[domain]; done
```

### Using host with wordlist
```bash
for sub in $(cat subdomains.txt); do host $sub.[domain]; done | grep "has address"
```

## DNS Cache Snooping

```bash
dig @[dns-server] [domain] +norecurse
```

## Common DNS Record Types

| Record Type | Description |
|------------|-------------|
| A | IPv4 address |
| AAAA | IPv6 address |
| CNAME | Canonical name (alias) |
| MX | Mail exchange servers |
| NS | Nameservers |
| TXT | Text records (often SPF, DKIM, etc.) |
| SOA | Start of authority |
| PTR | Pointer for reverse DNS |
| SRV | Service records |
| CAA | Certificate authority authorization |

## Tips

- Always try zone transfers first - it's the easiest way to get complete DNS data
- If zone transfer fails, use subdomain bruteforcing
- Check multiple nameservers - misconfiguration might exist on one but not others
- Look for interesting TXT records (might contain sensitive info)
- Check for wildcard DNS entries
- Verify reverse DNS for discovered IPs
