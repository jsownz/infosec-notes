---
icon: solar-system
---

# Getsystem

Multiple techniques are used when we run this command from a meterpreter shell - we should be careful about running the default (all) because we can crash systems or be traced.

```bash
# view techniques
getsystem -h
```

The best to use is an in-memory named pipe - this does not drop any files onto the system

The last technique needs SeDebugPrivilege to run
