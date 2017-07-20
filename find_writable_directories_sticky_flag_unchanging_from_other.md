# Find writable directories, which is not accessible from others
```
find / -type d \( -perm -g+w -o -perm -o+w \) -exec ls -ld {} \;
```

