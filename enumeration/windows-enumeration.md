---
icon: windows
---

# Windows Enumeration

## Finding Executables

### Finding bash.exe

Bash.exe may be present on Windows systems through WSL (Windows Subsystem for Linux), Git Bash, MSYS2, or Cygwin installations.

#### Using `where` command (fastest):
```cmd
where /R C:\ bash.exe
```

#### Using PowerShell:
```powershell
Get-ChildItem -Path C:\ -Filter bash.exe -Recurse -ErrorAction SilentlyContinue
```

#### Using `dir` for recursive search:
```cmd
dir /s /b C:\bash.exe
```

#### Common bash.exe locations:
- `C:\Windows\System32\bash.exe` (WSL)
- `C:\Program Files\Git\bin\bash.exe` (Git Bash)
- `C:\Program Files\Git\usr\bin\bash.exe` (Git Bash)
- `C:\msys64\usr\bin\bash.exe` (MSYS2)
- `C:\cygwin\bin\bash.exe` (Cygwin)

#### Quick WSL check:
```cmd
wsl --list
wsl --status
```

### Finding any executable
```cmd
where /R C:\ [filename.exe]
```

```powershell
Get-ChildItem -Path C:\ -Filter [filename.exe] -Recurse -ErrorAction SilentlyContinue
```

## System Information

### Basic System Info
```cmd
systeminfo
```

### OS Information
```cmd
ver
wmic os get Caption,Version,BuildNumber,OSArchitecture
```

### Installed Software
```powershell
Get-ItemProperty HKLM:\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\* | Select-Object DisplayName, DisplayVersion, Publisher, InstallDate
```

```cmd
wmic product get name,version
```

## User Enumeration

### Current User
```cmd
whoami
whoami /priv
whoami /groups
```

### List all users
```cmd
net user
net localgroup administrators
```

### User details
```cmd
net user [username]
```

## Network Information

### Network configuration
```cmd
ipconfig /all
```

### Routing table
```cmd
route print
```

### ARP cache
```cmd
arp -a
```

### Active connections
```cmd
netstat -ano
```

### Firewall status
```cmd
netsh advfirewall show allprofiles
netsh firewall show state
netsh firewall show config
```

## Process and Service Enumeration

### Running processes
```cmd
tasklist /v
```

```powershell
Get-Process
```

### Services
```cmd
sc query
net start
```

```powershell
Get-Service
```

### Scheduled tasks
```cmd
schtasks /query /fo LIST /v
```

## File and Directory Enumeration

### Search for files
```cmd
dir /s /b C:\[filename]
```

```powershell
Get-ChildItem -Path C:\ -Include [pattern] -Recurse -ErrorAction SilentlyContinue
```

### Find files containing specific text
```cmd
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
```cmd
reg query HKLM /f [keyword] /t REG_SZ /s
reg query HKCU /f [keyword] /t REG_SZ /s
```

### AutoRun programs
```cmd
reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Run
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

## Credentials and Sensitive Data

### Check for saved credentials
```cmd
cmdkey /list
```

### Search for passwords in files
```cmd
findstr /si password C:\*.txt
findstr /si password C:\*.xml
findstr /si password C:\*.ini
findstr /si password C:\*.config
```

```powershell
Get-ChildItem -Path C:\ -Include *.txt,*.xml,*.config,*.ini -Recurse -ErrorAction SilentlyContinue | Select-String -Pattern "password"
```

### Unattended install files
```cmd
dir /s *sysprep.inf *sysprep.xml *unattended.xml *unattend.xml
```

## Installed Programs and Paths

### PATH environment variable
```cmd
echo %PATH%
```

### Program Files directories
```cmd
dir "C:\Program Files"
dir "C:\Program Files (x86)"
```

### Check for development tools
```cmd
where python
where python3
where perl
where ruby
where gcc
where git
```
