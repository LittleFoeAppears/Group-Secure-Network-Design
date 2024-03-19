1. **DMZ Subnet:**
    
    - Subnet: 192.168.10.0/24
    - IP Range: 192.168.10.1 - 192.168.10.254
    - Default Gateway: 192.168.10.1
    - DHCP Scope: 192.168.10.50 - 192.168.10.100 (for servers in the DMZ)
2. **Management Subnet:**
    
    - Subnet: 192.168.20.0/24
    - IP Range: 192.168.20.1 - 192.168.20.254
    - Default Gateway: 192.168.20.1
    - DHCP Scope: 192.168.20.100 - 192.168.20.150
3. **Production Subnet:**
    
    - Subnet: 192.168.30.0/24
    - IP Range: 192.168.30.1 - 192.168.30.254
    - Default Gateway: 192.168.30.1
    - DHCP Scope: 192.168.30.100 - 192.168.30.200
4. **Support 1 Subnet:**
    
    - Subnet: 192.168.40.0/24
    - IP Range: 192.168.40.1 - 192.168.40.254
    - Default Gateway: 192.168.40.1
    - DHCP Scope: 192.168.40.100 - 192.168.40.150
5. **Support 2 Subnet:**
    
    - Subnet: 192.168.50.0/24
    - IP Range: 192.168.50.1 - 192.168.50.254
    - Default Gateway: 192.168.50.1
    - DHCP Scope: 192.168.50.100 - 192.168.50.150
6. **Study Subnet:**
    
    - Subnet: 192.168.60.0/24
    - IP Range: 192.168.60.1 - 192.168.60.254
    - Default Gateway: 192.168.60.1
    - DHCP Scope: 192.168.60.100 - 192.168.60.200
7. **Network Devices Subnet (for routers, switches, etc.):**
    
    - Subnet: 192.168.70.0/24
    - IP Range: 192.168.70.1 - 192.168.70.254
    - Default Gateway: 192.168.70.1
    - DHCP Scope: Not necessary (configure static IP addresses for network devices)