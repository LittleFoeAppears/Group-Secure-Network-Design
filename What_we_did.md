
What do we need in terms of subnets ? 

- Network
- Management
- Production
- Study
- Support
- DMZ

So we planned on implementing a VLAN per subnet : 

Network VLAN 60 192.168.0.1 255.255.255.0
Management VLAN 10 192.168.10.1 255.255.255.0
Production VLAN 20 192.168.20.1 255.255.255.0
Study VLAN 30 192.168.30.1 255.255.255.0
Support VLAN 40 192.168.40.1 255.255.255.0
DMZ VLAN 50 192.168.50.1 255.255.255.0

Each subnet will have a switch that is connected to an internal router, except to the DMZ subnet which is connected to the external router. 

On each subnet switch I configure them as such : 

First I create the VLANs on each switch :

vlan <vlan number>
name <vlan name>

-- put screenshot

The port that goes from the switch to the router will be a trunk that will allow all vlans:
In my configuration : 

switchport mode trunk

-- put screenshot

And for all the ports that goes from the switch to each host on the subnet :

switchport mode access
switchport access vlan <vlan number>

-- put screenshot

Then you need to configure the router on the ports that connects the vlans :

open port : (example f1/0 goes from the internal router to the management switch )

int fa1/0
no shutdown
exit

create the vlan10 sub-interface : 

int fa1/0.10
encapsulation dot1Q 10
ip address 192.168.10.1
ip helper-address 192.168.0.11 ( will be our DHCP server )

-- put screenshot

Do that for all the VLANS. 

Now it's time to create our DHCP server and plug it to the Network switch :

iPv4 address:  192.168.0.11
Subnet Mask: 255.255.255.0
Default Gateway : 192.168.0.1
DNS Server : 192.168.0.10 ( we'll create it laster )

Now go to services and activate the DHCP service on this server : 

We need to create a DHCP pool per VLAN : 
Example VLAN 10 : management

Pool Name : ManagementPool
Default Gateway : 192.168.10.1
DNS Server : 192.168.0.10
Start Ip Address : 192.168.10.0
Subnet Mask: 255.255.255.0
Maximum Number of Users: 256

Now you should be able to start a DHCP request from any subnet ( Except DMZ because we still need to connect the internal router to the external router )

We can make our required servers on the Network subnet and we'll configure them later :

DNS Server 192.168.0.10
ISCI Server 192.168.0.12
RADIUS Server 192.168.0.13
ACTIVE DIRECTORY Server 192.168.0.14

Now we need to connect our 2 routers with a Serial cable. 

On the internal router Se2/0 port : 

int Se2/0 
ip address 192.168.60.1 255.255.255.0
no shutdown

On the external router Se3/0 port :

int Se3/0
ip address 192.168.60.2 255.255.255.0
no shutdown

And then adjust the routing tables :

Internal Router : 

192.168.60.0/24 via 192.168.60.2
192.168.50.0/24 via 192.168.60.2

External Router : 

192.168.0.0/24 via 192.168.60.1
192.168.10.0/24 via 192.168.60.1
192.168.20.0/24 via 192.168.60.1
192.168.30.0/24 via 192.168.60.1
192.168.40.0/24 via 192.168.60.1
192.168.60.0/24 via 192.168.60.1

We added a web server in the DMZ subnet





