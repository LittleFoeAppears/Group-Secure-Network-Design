### Subnets and VLANs

To comply with our clients requirements we need to establish different subnets and VLANs :
- Management - VLAN 10
- Production - VLAN 20
- Study - VLAN 30
- Support - VLAN 40
- DMZ - VLAN 50
- Network - VLAN 60

So we configure one switch per subnet and we connect the correct number of hosts to those switches. All the subnet switches except for the DMZ switch is plugged to the Internal Router and the DMZ switch is connected to the External Router. 

We created VLANs on each switch as shown earlier ( SHOW SCREENSHOT VLAN DATABASE ), attributed every host port to those VLANs (SHOW SCREENSHOT VLAN HOST PORT ) and for the port connected from the switch to the router we need to establish them as Trunks (SHOW TRUNK SCREENSHOT ). 

Commands : 

int range fa0/3-20
switchport access VLAN <VLAN number>

int gig0/1
switchport mode trunk
switchport trunk allowed vlan all 


### Initial Routers Config

This is how we configured the routers :

- Internal Router :
Responsible for the internal network, connecting each internal subnets.
- External Router :
Responsible for the external network, connecting to the internet and the DMZ subnet.
We made the DMZ outside of the internal network to make our networks safer from the outside since DMZ is made to host servers that would be available from the outside.

We need to create sub-interface to connect the vlans to the router. 
Example for the VLAN 10 :

fa0/1
no shutdown

fa0/1.10
encapsulation dot1Q 10
ip address 192.168.10.1
ip helper-address 192.168.0.11 ( Which will be our DHCP router that we'll explain in a bit )

### Network Subnet 

Now we can start configuring our network subnet and its servers.
We create our servers are assign them static ips as such : 

- DNS Server - 192.168.0.10
- DHCP Server - 192.168.0.11
- ISCI Server - 192.168.0.12
- RADIUS Server - 192.168.0.13
- ACTIVE DIRECTORY Server - 192.168.0.14

DNS Server : 

We can configure it by going to the service tab , put it on and add some DNS record by providing a name, an Ip and a record type as such : (SHOW DNS TAB SCREENSHOT)
Don't forget to copy the DNS server address and input it on all the static ip configured hosts on the network.

DHCP Server : 

We can configure it by going to the service tab, put it on and create a DHCP pool per subnet/VLAN as such :  ( SHOW DHCP POOL SCREENSHOT )

Example : 

Name: Management
Default Gateway : 192.168.10.1
DNS Server : 192.168.0.10
Start IP Address : 192.168.10.0
Subnet Mask : 255.255.255.0
Max User : 256

When it's done, any pc from the network should be able to do a DHCP request and get an IP.

ISCI Server : 

We can configure it by going to the service tab , put it on and configure the ISCI Server.
An iSCSI server is like a remote hard drive that you can connect to over your regular network cable, letting you store files on it from another computer.
Since it is not possible on Cisco Packet tracer we decided to emulate it by creating an FTP server : ( SHOW FTP SERVER SCREEN )

RADIUS Server : 

We can configure it by going to the aaa service tab, put it on and configure it as such : ( SHOW RADIUS CONFIGURATION SCREENSHOT )
We can then configure each routers from our network to use radius as such : (SHOW SCREENSHOT RADIUS CONFIG )

aaa new-model
radius-server host 192.168.0.11 auth-port 1812 key password
aaa authentication login default group radius local
aaa authorization exec default group radius local
aaa accounting exec default start-stop group radius
line vty 0 15
login authentication default
transport input all
end

Now, to enter to an host CLI you'd need to have credentials that gives access to the host.

ACTIVE DIRECTORY Server :

Active Directory is an electronic phonebook for your network, storing user accounts, devices, and permissions in one central location for easy management and secure access.
Since it's not possible to make one in cisco packet tracer we've decided to emulate one by making a server that would host the active directory on a web page.
(SHOW ACTIVE DIRECTORY SCREENSHOT)

### The Outside 

We then connected our external router to the internet. We emulated the internet by creating a cluster from where outsiders could host their servers ( In our example we created a google server ) ( SHOW GOOGLE SCREENSHOT ) and we made sure that we could access them from any hosts in our network. 

### Routing 

Our routers are connected via serial DTE cable and we configured the routes as such : ( SHOW ROUTES SCREENSHOT ) 

For example connecting our internal router to the dmz : 

ip route 192.168.50.0 255.255.255.0 192.168.60.2

### Access List Config






