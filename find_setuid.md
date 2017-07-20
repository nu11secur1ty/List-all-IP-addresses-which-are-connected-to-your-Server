# Example—Finding Files With setuid Permissions in /root/

```
find / -user root -perm -4000 -exec ls -ldb {} \; 
```
# Find Files With setuid Permissions on directory

```
find _directory_ -user root -perm -4000 -exec ls -ldb {} \; >/tmp/_filename_
```


