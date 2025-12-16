---
icon: virus-slash
---

# AV Enumeration

## Service Control

```bash
sc query windefend
sc queryex type= service
```

## Firewall

```bash
netsh advfirewall firewall dump
netsh firewall show state
netsh firewall show config
```

