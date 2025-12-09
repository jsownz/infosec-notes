---
icon: car-tunnel
---

# Tunneling / Pivoting

## Chisel

[https://github.com/jpillora/chisel](https://github.com/jpillora/chisel)

## SSH

```sh
ssh -D 127.0.0.1:9999 user@hostname
```

* Sets up a SOCKS proxy running on local machine at `9999` routing traffic through `hostname`
* Will need to use something like Proxychains for command line or FoxyProxy for web viewing

## Proxychains

Firstly we need to set up a SOCKS5 proxy throught he server we're pivoting through

```bash
ssh -f -N -D 9050 [ssh creds]@[host]
```

We can now use proxychains to route our traffic through that proxy

```bash
proxychains nmap -p- [secondary network]
```

* Many times you may need to use `-sT` flag for nmap for TCP connect scans

## SShuttle

This will make that secondary network accessible to you on your machine as long as this command is running:

{% code overflow="wrap" %}
```bash
sshuttle -r [user]@[pivot machine] [secondary network CIDR] --ssh-cmd "ssh [ssh id file if needed]"
```
{% endcode %}
