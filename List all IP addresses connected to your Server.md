# List all IP addresses which are connected to your Server
![A](https://github.com/nu11secur1ty/List-all-IP-addresses-which-are-connected-to-your-Server/blob/master/photo/24382-06--internet-network.jpg)


Below is an Unix command to list all the IP addresses connected to your server on port 80.

```
netstat -tn 2>/dev/null | grep :80 | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -nr | head
netstat -tn 2>/dev/null | grep 80
netstat -tn 2>/dev/null | grep 22
netstat -tn 2>/dev/null | grep 23
netstat -tn 2>/dev/null | grep 53
```

Output example – Total connections by IP, from highest to lowest.

```
97 114.198.236.100
56 67.166.157.194
44 170.248.43.76
38 141.0.9.20
37 49.248.0.2
37 153.100.131.12
31 223.62.169.73
30 65.248.100.253
29 203.112.82.128
29 182.19.66.187
```


# Note
This command is useful to detect if your server is under attack, and null route those IPs. Read this null route attacker IP story.


Let break above lengthy command into pieces :
# 1. netstat -tn 2>/dev/null

Uses netstat to list all network connections, ins and outs.

   1. -n – Display numeric only, don’t resolve into name.
   2. -t – Display only TCP connections.

Output:


```
# Examples - 7 connections
tcp        0      0 64.91.*.*:80            114.198.236.100:12763       TIME_WAIT
tcp        0      0 64.91.*.*:80            175.136.226.244:51950       TIME_WAIT
tcp        0      0 64.91.*.*:80            175.136.226.244:51951       TIME_WAIT
tcp        0      0 64.91.*.*:23            202.127.210.2:14517         TIME_WAIT
tcp        0      0 64.91.*.*:80            149.238.193.121:65268       TIME_WAIT
tcp        0      0 64.91.*.*:80            114.198.236.100:44088       ESTABLISHED
tcp        0      0 64.91.*.*:80            175.136.226.244:51952       TIME_WAIT
```

```
# 2>/dev/null
Redirect all unwanted output to /dev/null, a special place to absorb all output and clear it.
```

# 2. grep :80

Only display the IP address that connected to server on port 80. 
example:

```
tcp        0      0 64.91.*.*:80            114.198.236.100:12763       TIME_WAIT
tcp        0      0 64.91.*.*:80            175.136.226.244:51950       TIME_WAIT
tcp        0      0 64.91.*.*:80            175.136.226.244:51951       TIME_WAIT
tcp        0      0 64.91.*.*:80            149.238.193.121:65268       TIME_WAIT
tcp        0      0 64.91.*.*:80            114.198.236.100:44088       ESTABLISHED
tcp        0      0 64.91.*.*:80            175.136.226.244:51952       TIME_WAIT
```
# 3. awk ‘{print $5}’

Uses awk to display the 5th field only.

```
114.198.236.100:12763
175.136.226.244:51950
175.136.226.244:51951
149.238.193.121:65268
114.198.236.100:44088
175.136.226.244:51952
```


# 4. cut -d: -f1

Uses cut to extract the content.

   1. -d – Character immediately following the -d option is use as delimiter, default is tab.
   2. -f – Specifies a field list, separated by a delimiter.

```
114.198.236.100
175.136.226.244
175.136.226.244
149.238.193.121
114.198.236.100
175.136.226.244
```

# 5. sort | uniq -c | sort -nr

Sort the list, group it and sort it again in reverse order.

sort

```
114.198.236.100
114.198.236.100
149.238.193.121
175.136.226.244
175.136.226.244
175.136.226.244
```

uniq -c – Group it.

```
2 114.198.236.100
1 149.238.193.121
3 175.136.226.244
```

sort -nr – sort by numeric, and reverse order (highest display first)


```
3 175.136.226.244
2 114.198.236.100
1 149.238.193.121
```

Done.

# 6. head

This is optional, to display the first 10 result.
References

   1. /dev/null
   2. Netstat
   3. AWK
   4. Cut
   5. Uniq
   6. Sort
   7. Optional: 
     Listening ports and...
```
netstat -tulpn
```

# Have fun with nu11secur1ty =)








