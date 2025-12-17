---
description: After we have a shell, we need to enumerate the system
icon: magnifying-glass
---

# Enumeration

## Current User Info

```bash
whoami
whoami /privs
whoami /groups
```

## System Info

```bash
systeminfo
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
```

Here, we can get the OS Name, OS Version, and Architecture in a one-liner

## Patching

```bash
wmic qfe
```

## Drives

```bash
wmic logicaldisk get caption,description,providername 
```

## Users

```bash
net user
net user [username]
```

## Groups

```bash
net localgroup
net localgroup [group]
```

## Searching

```bash
where /R [starting dir] [application]
```
