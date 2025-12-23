---
icon: person-running-fast
---

# RunAs

Need to find the runas.exe binary - usually in windows/system32/

We need to have a saved credential:

```bash
cmdkey /list
[user we can use here]
```

Then we cna use the runas binary to execute a command as that user

```bash
C:\Windows\System32\runas.exe /user:[user] /savecred "[command to run]"
```
