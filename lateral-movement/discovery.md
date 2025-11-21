---
icon: folders
---

# Discovery

### FTP

If we have access to FTP, we can use a Bounce Attack to scan networks that the server has access to. From our attacking machine:

{% code overflow="wrap" %}
```shellscript
nmap [nmap flags] -b [login]:[password]@[target] [internal host to scan]
```
{% endcode %}
