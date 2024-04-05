This is a group project done with : @Etta99 @LittleFoeAppears @Tuuxy

![NETWORK ARCHITECTURE](Assets/network.png)

# Subnets and VLANs

To comply with our clients requirements we need to establish different subnets and VLANs :
- Management - VLAN 10
- Production - VLAN 20
- Study - VLAN 30
- Support - VLAN 40
- DMZ - VLAN 50
- Network - VLAN 60

We configure one switch per subnet and we connect the correct number of hosts to those switches. All the subnet switches except for the DMZ switch is plugged to the Internal Router and the DMZ switch is connected to the External Router. 

![VLAN DATABASE](Assets/VLAN_DATABASE.png)

![VLAN HOST](Assets/VLAN_HOST_PORT.png)

![TRUNK](Assets/VLAN_TRUNK.png)

We created VLANs on each switch as shown earlier , attributed every host port to those VLANs and for the port connected from the switch to the router we need to establish them as Trunks . 

Commands : 

```bash
en
conf t

int range fa0/3-20
switchport access VLAN <VLAN number>

int gig0/1
switchport mode trunk
switchport trunk allowed vlan all 
```

---
# Initial Routers Config

This is how we configured the routers :

- Internal Router :
Responsible for the internal network, connecting each internal subnets.
- External Router :
Responsible for the external network, connecting to the internet and the DMZ subnet.
We made the DMZ outside of the internal network to make our networks safer from the outside since DMZ is made to host servers that would be available from the outside.

We need to create sub-interface to connect the vlans to the router. 
Example for the VLAN 10 :

```bash
fa0/1
no shutdown

fa0/1.10
encapsulation dot1Q 10
ip address 192.168.10.1
ip helper-address 192.168.0.11 
# Which will be our DHCP router that we'll explain in a bit 
```

---
# Network Subnet 

Now we can start configuring our network subnet and its servers.
We create our servers are assign them static ips as such : 

> - DNS Server - 192.168.0.10
> - DHCP Server - 192.168.0.11
> - ISCI Server - 192.168.0.12
> - RADIUS Server - 192.168.0.13
> - ACTIVE DIRECTORY Server - 192.168.0.14

#### DNS Server : 

We can configure it by going to the service tab , put it on and add some DNS record by providing a name, an Ip and a record type as such : 

![DNS](Assets/DNS_TAB.png)

Don't forget to copy the DNS server address and input it on all the static ip configured hosts on the network.

#### DHCP Server : 

We can configure it by going to the service tab, put it on and create a DHCP pool per subnet/VLAN as such :  

![DHCP Pools](Assets/DHCP_POOL.png)

Example : 
> 
> Name: Management
> Default Gateway : 192.168.10.1
> DNS Server : 192.168.0.10
> Start IP Address : 192.168.10.0
> Subnet Mask : 255.255.255.0
> Max User : 256

When it's done, any pc from the network should be able to do a DHCP request and get an IP.

#### ISCI Server : 

We can configure it by going to the service tab , put it on and configure the ISCI Server.
An iSCSI server is like a remote hard drive that you can connect to over your regular network cable, letting you store files on it from another computer.
Since it is not possible on Cisco Packet tracer we decided to emulate it by creating an FTP server : 

![FTP Config](Assets/FTP.png)

![FTP Logged](Assets/FTP_ACCESS.png)

#### RADIUS Server : 

We can configure it by going to the aaa service tab, put it on and configure it as such : 

![Radius Config](Assets/RADIUS_CONFIG.png)

We can then configure each routers from our network to use radius as such : 


```bash
en
conf t
aaa new-model
radius-server host 192.168.0.11 auth-port 1812 key password
aaa authentication login default group radius local
aaa authorization exec default group radius local
aaa accounting exec default start-stop group radius
line vty 0 15
login authentication default
transport input all
end
```

![Radius Login](Assets/RADIUS_ROUTER.png)

Now, to enter to an host CLI you'd need to have credentials that gives access to the host.

![Radius Access](Assets/RADIUS_ACCESS.png)

#### ACTIVE DIRECTORY Server :

Active Directory is an electronic phonebook for your network, storing user accounts, devices, and permissions in one central location for easy management and secure access.
Since it's not possible to make one in cisco packet tracer we've decided to emulate one by making a server that would host the active directory on a web page.

![Active Directory](Assets/ACTIVE_DIRECTORY.png)

---
# The Outside 

We then connected our external router to the internet. 
We emulated the internet by creating a cluster from where outsiders could host their servers ( In our example we created a google server )  and we made sure that we could access them from any hosts in our network. 

![Google](Assets/GOOGLE.png)

---

# Routing 

Our routers are connected via serial DTE cable and we configured the routes as such : 

![Routes Internal](Assets/ROUTER_1.png)

![Routes External](Assets/ROUTER_2.png)

For example connecting our internal router to the dmz : 

```bash
ip route 192.168.50.0 255.255.255.0 192.168.60.2
```

---

# Access List Config

#### External Server:
We set the first Access list (101).
Here we denied access to the DMZ except for http and https requests.
So only normal utilization of the web server is allowed.
>```bash
>access-list 101 permit tcp any host 192.168.50.10 eq 80  
>access-list 101 permit tcp any host 192.168.50.10 eq 443
>access-list 101 deny ip any 192.168.50.0 0.0.0.255
>access-list 101 permit ip any any
>```

#### Internal Server:
We set the second Access list (102).
Here we denied access to every inbound traffic except for responses to internal request (established connections).
> ```bash
> access-list 102 permit tcp any any established 
> access-list 102 deny ip any any
> ```


So in conclusion we blocked anything to access the Internal Network, and only normal http or https can enter the DMZ from outside.
This coupled with the radius system protecting the routers insures a descent security setup.

### Costs

We estimate the cost of the installation to be about 70k dollars, here is the breakdown : 

2 * 150 (routers) = 300
6 * 1500 (switches) = 9000
7 * 2000 (servers) = 14000
39 * 1000 (PCs) = 39000
4 * 1500 (Printers) = 6000
= 68 300

Plus the cabling. 






