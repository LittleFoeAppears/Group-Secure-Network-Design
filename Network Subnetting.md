Four network sectors:

- Management/Secretariat (5 workstations)
- Study (8 workstations)
- Production (10 workstations)
- Support (2 sectors, 10 workstations each)

Server networks:
- DHCP
- DMZ
- DNS
- iSCSI storage server

Need to use VLANs and ACLs

Choice of mask :  192.168.1.0/27

We could make up to 8 subnets with up to 30 hosts ( for scalabilty )

| Subnet Number | Network Address (Decimal) | Broadcast Address (Decimal) | Usable Hosts (Decimal) |
| ------------- | ------------------------- | --------------------------- | ---------------------- |
| 1 Net Devices | 192.168.1.0               | 192.168.1.31                | 30                     |
| 2 DMZ         | 192.168.1.32              | 192.168.1.63                | 30                     |
| 3 MGMT        | 192.168.1.64              | 192.168.1.95                | 30                     |
| 4 STUDY       | 192.168.1.96              | 192.168.1.127               | 30                     |
| 5 PROD        | 192.168.1.128             | 192.168.1.159               | 30                     |
| 6 SUPPORT 1   | 192.168.1.160             | 192.168.1.191               | 30                     |
| 7 SUPPORT 2   | 192.168.1.192             | 192.168.1.223               | 30                     |
| 8 FIREWALL    | 192.168.1.224             | 192.168.1.255               | 30                     |

