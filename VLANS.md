On switch :

```
int range fa0/3-20
switchport access <vlan vlan-number>

int fa0/1 (switch to router cable)
switchport mode trunk
switchport trunk allowed vlan all
```

On router : 

```
int fa0/1
no shutdown

int fa0/1.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
ip helper-address 192.168.0.11
end
write memory
```


