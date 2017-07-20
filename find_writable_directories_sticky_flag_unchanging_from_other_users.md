# Find writable directories, which is not accessible from other users
```
find / -type d \( -perm -g+w -o -perm -o+w \) -exec ls -ld {} \;
```

