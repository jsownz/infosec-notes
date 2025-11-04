---
icon: microchip
---

# Techniques

### Tunneling

#### Chisel

#### SSH

```sh
ssh -D 127.0.0.1:9999 user@hostname
```

* Sets up a SOCKS proxy running on local machine at `9999` routing traffic through `hostname`
* Will need to use something like Proxychains for command line or FoxyProxy for web viewing
