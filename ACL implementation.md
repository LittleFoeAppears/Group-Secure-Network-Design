- only http and https access to Web Server form outside
- only established traffic can access the Internal Network

### ACL restrictions for DMZ
External Router:
>```bash
>en
>conf t
>```
>Restrict access to web server to http and https port
>`Web Server ip: 192.168.50.10`
>```bash
>access-list 101 permit tcp any host 192.168.50.10 eq 80  
>access-list 101 permit tcp any host 192.168.50.10 eq 443
>access-list 101 deny ip any 192.168.50.0 0.0.0.255
>access-list 101 permit ip any any
>```
>Apply the ACL to the internet inbound interface
>```bash
>interface Se2/0
>ip access-group 101 in
>```
>Save settings
>```bash
>end
>write memory
>```

### ACL restrictions for Internal network
Internal  Router:
>```bash
>en
>conf t
>```
>Restrict inbound traffic except responses to internal requests (established connections)
> ```bash
> access-list 102 permit tcp any any established 
> access-list 102 deny ip any any
> ```
> Apply the ACL to the inbound interface to Internal Network
> ```bash
> int Se2/0
> ip access-group 102 in
> ```
>Save settings
>```bash
>end
>write memory
>```