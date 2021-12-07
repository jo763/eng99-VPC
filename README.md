# Definitions
- CIDR block: Classless inter-domain routing (CIDR) is a set of Internet protocol (IP) standards that is used to create unique identifiers for networks and individual devices. Two groups: The network address and the subnet. https://whatismyipaddress.com/cidr
-  IPv4 and IPv6 are CIDR classes. IPv4 is current standard, but as demand is exceeding amount, IPv6 will be implemented. IPv6 addresses may contain up to 128 bits instead of the 32-bit maximum of IPv4.
- Route table: A routing table is a set of rules, often viewed in table format, that is used to determine where data packets traveling over an Internet Protocol (IP) network will be directed. All IP-enabled devices, including routers and switches, use routing tables. A routing table contains the information necessary to forward a packet along the best path toward its destination. Each packet contains information about its origin and destination. When a packet is received, a network device examines the packet and matches it to the routing table entry providing the best match for its destination. The table then provides the device with instructions for sending the packet to the next hop on its route across the network. https://www.techtarget.com/searchnetworking/definition/routing-table
- Internet Gateway (IG): An internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between your VPC and the internet.
An internet gateway serves two purposes: to provide a target in your VPC route tables for internet-routable traffic, and to perform network address translation (NAT) for instances that have been assigned public IPv4 addresses.
- VPC & Subnet Range: A virtual private cloud (VPC) is a secure, isolated private cloud hosted within a public cloud. VPC customers can run code, store data, host websites, and do anything else they could do in an ordinary private cloud, but the private cloud is hosted remotely by a public cloud provider. (Not all private clouds are hosted in this fashion.) VPCs combine the scalability and convenience of public cloud computing with the data isolation of private cloud computing. https://www.cloudflare.com/en-gb/learning/cloud/what-is-a-virtual-private-cloud/. A subnet, or subnetwork, is a segmented piece of a larger network. More specifically, subnets are a logical partition of an IP network into multiple, smaller network segments.
- NACLs - Networking and Cryptography library - high-speed software library for network communication, encryption, decryption, signatures, etc
![VPC Diagram](https://github.com/jo763/eng99-VPC/blob/main/VPC_diagram.PNG)

# Creating a VPCs
- Go to VPC --> VPCs (on sidenav)
- Create VPC with IPv4 CIDR = 10.0.0.0/16
- Give a name, ensure "IPv4 CIDR manual input" is selected then create
- Create internet gateway (IG) on sidenav with sensible name then create
- Return to internet gate, select IG and then click actions and then attach to desired VPC
- Create subnet: go to subnets on sidenav, select VPC, choose availability zone then create.
- Create route table (rt): go to route table on sidenav, associate with vpc.
- Go to actions (for rt) --> edit route add enter 0.0.0.0/0 for destination and attach the internet gateway for the target
- Go to actions (for rt) --> edit subnet associations, attach relevant subnets
- Go to EC2 --> AMIs, select AMI and launch
- Select instance type
- Select VPC created, select subnet, enable auto assign public ip
- Add storage
- Add tags
- port 22 for my ip, port 3000 for specified app, port 80 for http and https for ssl - public facing app
- allow access for other app subnet and ip addresses
- for private portion, ensure it doesn't have internet access
- Note IP addresses to each other are now private and not public
- Change db_host environment vairable to reflect this
