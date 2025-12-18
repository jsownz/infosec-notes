---
icon: windows
---

# Windows Enumeration

## Finding Executables

### Finding bash.exe

Bash.exe may be present on Windows systems through WSL (Windows Subsystem for Linux), Git Bash, MSYS2, or Cygwin installations.

#### Using `where` command (fastest):

```bash
where /R C:\ bash.exe
```

#### Using PowerShell:

```powershell
Get-ChildItem -Path C:\ -Filter bash.exe -Recurse -ErrorAction SilentlyContinue
```

#### Using `dir` for recursive search:

```bash
dir /s /b C:\bash.exe
```

#### Common bash.exe locations:

* `C:\Windows\System32\bash.exe` (WSL)
* `C:\Program Files\Git\bin\bash.exe` (Git Bash)
* `C:\Program Files\Git\usr\bin\bash.exe` (Git Bash)
* `C:\msys64\usr\bin\bash.exe` (MSYS2)
* `C:\cygwin\bin\bash.exe` (Cygwin)

#### Quick WSL check:

```bash
wsl --list
wsl --status
```

### Finding any executable

```bash
where /R C:\ [filename.exe]
```

```powershell
Get-ChildItem -Path C:\ -Filter [filename.exe] -Recurse -ErrorAction SilentlyContinue
```

## System Information

### Basic System Info

```bash
systeminfo
```

### OS Information

```bash
ver
wmic os get Caption,Version,BuildNumber,OSArchitecture
```

### Installed Software

```powershell
Get-ItemProperty HKLM:\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\* | Select-Object DisplayName, DisplayVersion, Publisher, InstallDate
```

```bash
wmic product get name,version
```

## User Enumeration

### Current User

```bash
whoami
whoami /priv
whoami /groups
```

### List all users

```bash
net user
net localgroup administrators
```

### User details

```bash
net user [username]
```

## Network Information

### Network configuration

```bash
ipconfig /all
```

### Routing table

```bash
route print
```

### ARP cache

```bash
arp -a
```

### Active connections

```bash
netstat -ano
```

### Firewall status

```bash
netsh advfirewall show allprofiles
netsh firewall show state
netsh firewall show config
```

## Process and Service Enumeration

### Running processes

```bash
tasklist /v
```

```powershell
Get-Process
```

### Services

```bash
sc query
net start
```

```powershell
Get-Service
```

### Scheduled tasks

```bash
schtasks /query /fo LIST /v
```

## File and Directory Enumeration

### Search for files

```bash
dir /s /b C:\[filename]
```

```powershell
Get-ChildItem -Path C:\ -Include [pattern] -Recurse -ErrorAction SilentlyContinue
```

### Find files containing specific text

```bash
findstr /si [text] C:\*.txt
```

### Recently modified files

```powershell
Get-ChildItem -Path C:\ -Recurse -ErrorAction SilentlyContinue | Where-Object {$_.LastWriteTime -gt (Get-Date).AddDays(-7)}
```

### World-writable folders

```powershell
Get-ChildItem 'C:\Program Files' -Recurse | Get-ACL | Where-Object {$_.AccessToString -match "Everyone\sAllow\s\sModify"}
```

## Registry Enumeration

### Search registry

```bash
reg query HKLM /f [keyword] /t REG_SZ /s
reg query HKCU /f [keyword] /t REG_SZ /s
```

### AutoRun programs

```bash
reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Run
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

## Credentials and Sensitive Data

### Check for saved credentials

```bash
cmdkey /list
```

### Search for passwords in files

```bash
findstr /si password C:\*.txt
findstr /si password C:\*.xml
findstr /si password C:\*.ini
findstr /si password C:\*.config
```

```powershell
Get-ChildItem -Path C:\ -Include *.txt,*.xml,*.config,*.ini -Recurse -ErrorAction SilentlyContinue | Select-String -Pattern "password"
```

### Unattended install files

```bash
dir /s *sysprep.inf *sysprep.xml *unattended.xml *unattend.xml
```

## Installed Programs and Paths

### PATH environment variable

```bash
echo %PATH%
```

### Program Files directories

```bash
dir "C:\Program Files"
dir "C:\Program Files (x86)"
```

### Check for development tools

```bash
where python
where python3
where perl
where ruby
where gcc
where git
```

### Locksmith

[https://github.com/jakehildreth/Locksmith](https://github.com/jakehildreth/Locksmith)
