# Networking Start Pack

## OSI 7-Layer Model
The OSI (Open Systems Interconnection) model is a framework that describes the functions and interactions of computer systems in a network.

- Local Networking: Ethernet (start / end point of data moving across internet)
- Routing: Moving data across multiple networks
- Segmenting, Ports, and Sessions
- Applications

1. Physical
2. Data Link
3. Network
4. Transport
5. Session
6. Presentation
7. Application
^ These 7 layers are the "Networking Stack". 1-3 are Media Layers, 4-7 are Host Layers

### Layer 1 - Physical
Imagine you have two laptops at home and you want to LAN game between the two. You have a physical connection/medium between the two laptops (network interface card, network cable).

Physical Medium: can be Copper (electrical), fiber (light), of WiFi (RF). 

A Layer 3 device has the capabilities of all layers under it (3, 2, and 1). A Layer 1 device only has the capabilities of Layer 1, as no layers are below it.

There are no individual device addresses at Layer 1. Anything received on any port is transmitted out on every other port (including errors and collisions). If multiple devices transmit on the same level 1 physical medium, a collision occurs and corrupts data. The more layer 1 devices connected, the more likely a collision.

Layer 1 is "dumb". 1 broadcast and 1 collision domain, not very scalable. No access control. No uniquely identifiable devices. so no device-to-device communication.

### Layer 2 - Data Link (DL)
Data Link adds lots of intelligence to layer 1, allowing for more effective communication. DL all higher layers rely on Layer 2 as it supports the transfer of data.

Rather than physical wavelengths or voltages, but uses "frames". Devices at L2 have a unique hardware (MAC) address. Frames can be addressed to a destination or to a broadcast.

Frame is a container of sorts.
- First is PREAMBLE (let's device know this is start of the frame
- Destination and Source MAC addresses
- EtherType: which layer 3 protocol is putting its data in a frame
- Payload: The data the frame carries from source to destination
- Frame Check Sequence (FCS): Confirm it corruption has occurred

Mac Header = Source MAC address + Destination MAC address + EtherType

In order to have active Layer 2 network, you need Layer 1 active and working. Layer 2 checks for carriers, if no carriers, Frame is sent to Layer 1 for transmission. Carrier detected? Wait, as another device is transmitting.

CSMA: Carrier Sense Multiple Access. Detects data to avoid collision.

Encapsulation: When data is wrapped in by a Frame. As data is passed down OSI model, many different components encapsulate the data.

Collision Detection at layer 2. If both devices check for carrier which doesn't exist, then both L2's instruct transmission via layer 1, a collision can occur. If collision is detected, jam signal is sent and a random backoff occurs. Backoff = time + random. It increases if another collision occurs.

Hub = layer 1 device. Dumb, send data to all ports.
Switch = layer 2 device. Maintains MAC address table to learn what's connected to each port. Intelligent; store and forward Frames appropriately, based on MAC address table. Won't forward collisions. Each port becomes a separate collision domain.

- Identifiable devices
- Media Access Control (sharing)
- Collision Detection
- Unicast 1:1
- Broadcast 1:ALL
- Switches

### Layer 3 - Network
Requires 1 or more Layer 2 networks to function. Layer 3 gets data from one location to another. With streaming, data moved from server hosting video to local device.

#### Why is Layer 3 needed?
If we have two local area networks with geographic separation (east/west coast US separation). LAN1 and LAN2 are isolated Layer 2 local networks right now. You *could* use point to point physical links across the distance, but this is costly. Layer 2 protocols can be different so connecting to L2 networks can be challenging. We need something in common between the two L2's. To move data between two local networks... inter-networking ==> internet. IP addresses can be assigned as a way to connect separated L2 networks.

- Routers are the hardware that L3 uses to encapsulate data in an IP packet.

- IP allows you to connect to remote networks, allowing you to cross over intermediary networks in between.

Packet: Data unit used in IP. Similar to Frames (L2). Every packet has a Source IP and Destination IP address.

- Two versions of IP in use. Version 4 and Version 6.
-- Destination/Source IP addresses are larger in v6 to allow for more.

#### L3: IP Addressing (IPv4)
Structure of an IP address. This section focuses on v4.

IP Address
133 . 33 . 3 . 7
- Dotted decimal notation from 0 - 255
- All IP addresses formed of two different partsL 1) Network (133.33), 2) Hosts (3.7)
- You can see if two IP addresses are on same network if the first half matches (both being 133.33)
- 4 sets of 8 bits, 32 bits total for IP address. Each number in IP Address is an octet
- /16 prefix. First 16 bits are network, last 16 bits are host
- Static IP: assigned by humans. DHCP: Machine assigned IPs
- IP addresses need to be unique, esp on local network

Subnet Masks: ID's host and network parts of IP addresses. So it can know when to send data on same local network, or use a router to transport across different networks. Configured on L3 along with IP addresses. Allows an IP device to know if IP is on same network or not. If not on same network, data is sent to Default Gateway (router)
- e.g. 255.255.0.0 is a subnet mask, and is the same as the /16 prefix (when broken down into binary)

#### L3: Route Tables & Routes
How a router decides where to send data.

Every router has at least 1 route table. This is how a router knows where to send data. Two fields: 1) destination field 2) Next Hop/Target. The larger the prefix, the more specific the route (/0, /16, /32). Routers prefer more specific routes.  

/24 = first 24 bits for network, last 8 bits are for host.

Default Route: 0.0.0.0/0 = matches if nothing else does.

IMPORTANT: When ISP router is forwarding packet to AWS router, it's forwarding it at Level 2; wrapped in a Frame. How do we determine MAC address of AWS router? Address Resolution Protocol

#### L3: Address Resolution Protocol
Used when Layer 3 packet needs to be encapsulated in a Frame and sent to MAC address. You don't know the MAC address, but you need to get it. This is where ARP comes in. 
- ARP will give you MAC address with given IP address
- ARP broadcasts on Layer 2

#### L3: IP Routing
Lengthy example, not a very great visual. Recommend looking up another video on YouTube for IP Routing Explanation

### Layer 4 & 5 - Transport & Session
Layer 4 allows you to create Segments with a sequence number in order to maintain the order (L3 can't control order of packets)


NOTE: Course is no longer broken down by Layers


#### TCP - Transmission Control Protocol
- connection between client and server used to exchange data
- established between two devices using a 'random port' on a client and a 'known port' on the server
- connection is reliable provided via segments encapsulated in IP packets. Orders segments with their sequence numbers
- also has error checking and retransmission
- bidirectional connections
- creates a 'channel' to exchange data, but really it's just a collection of segments; no real channel
- Ephemeral Port: client source port (or High Ports). Needs separate rules compared to Well Known Port
- Well Known Port: server port. Needs separate rules compared to Ephemeral Port

##### Flags Field in TCP
Contains actual flags which can be set to influence the connection.
FIN - used to close
ACK - used for acknowledgments
SYN - sequence numbers
1) "Hey, let's talk": Send segment to server with SYN (initial sequence number is ISN, or 'cs'; sequence set)
2) "Sure, let's talk": SYN-ACK - server receives communication from client, receives cs, sets ACK to cs+1, sends cs+1 and ss
3) "Awesome, go!": Send segment with ACK, send to ss+1
4) Connection established, client can send data

##### Firewalls on Ephemeral Port side
- Stateless Firewall: Doesn't understand state of a connection. Two rules 1) OUT: allow outbound segments (initiating traffic) 2) IN: allow response (response traffic). In AWS, a Nework Access Control List (ACL) is a stateless firewall.
- Stateful Firewall: Sees OUT and IN as the same thing; if OUT allowed, IN is auto-alowed (and vice versa). In AWS, this is how a Security Group works

### Network Address Translation (NAT)
We will cover the basics of NAT, including how it works, its different types, and the benefits and drawbacks of using NAT.
- NAT is a process designed to address growing shortages of IPv4 addresses
- Translates Private IPv4 addresses to Public and back as they cannot communicate otherwise. This is what gets Private IPs on the internet
-- Publically routable addresses (must be unique)
-- Private addresses (don't need to be unique, can be used multiple places)
- Router is an example of a NAT device

#### Types of NATs (3)
1 - Static NAT: 1 private to 1 (fixed) public address (IGW, Internet Gateway). Gives private address access to internet in both directions
2 - Dynamic NAT: Pool of public IP addresses for private IP's to use. Generally used with large number of private IP addresses but have less Public Addresses than private. Private IPs must use the Public IP allocations at DIFFERENT times; they cannot overlap. External access may fail if there are no IPs in the public pool
3 - Port Address Translation (PAT): Many private to 1 public (AWS NATGW). This is what your home router does with multiple devices. Uses ports to ID devices
-- This is the method that NAT instances use in AWS NATGateway (NATGW)
-- Uses both IP addresses &  Ports to allow multiple devices to use same IP
-- MANY:1, PrivateIP:PublicIP Architecture

- NAT only makes sense for IPv4. IPv6 has enough addresses, as is (no need for NAT in IPv6)

### IP Address Space & Subnetting (IPv4)
Originally this was directly managed by IANA (Internet Assigned Numbers Authority)
- Parts now delegated to regional authorities
- There are about 4.3B IPv4 addresses

#### Address Space Classing
Class A Address Space: 0.0.0.0 -> 127.255.255.255 (for huge business/early internet)
Class B Address Space: 128.0.0.0 -> 191.255.255.255 (for larger businesses that didn't need Class A)
Class C Address Space: 192.0.0.0 -> 223.255.255.255 (for smaller businesses not large enough for B or A)
Class D & Class E: D for Multicast, E is Reserved

#### Private IP Adresses
Defined by a standard RFC1918

When possible, allocate non-overlapping ranges across your networks.

##### IPv4 Address Space
See Class A - E above. 4,294,967,296 total IPs in IPv4. Too few which is why IPv6 was created (340 trillion trillion trillion addresses)

##### IP Subnetting (IPv4)
Subnetting takes a large network and breaks into smaller networks.

CIDR (Classless Inter-Domain Routing) - Let's us take networks and break them down, determining size of network (ex. /16 prefix)
/8 is the same as a class A network
/16 is smaller network within Class A network
- The larger the prefix value, the smaller the network

If you have a large network, you can subnet them. /16 => 2 * /17, split network in 2. One /16 network is the same as 2 /17 networks.
-- Now we have two /17 networks. We can split one of these into 2 * /18. Now we have 3x: /17, /18. and /18 networks.
--- To get to 4 networks, split the remaining /17 network into another two /18 networks, for four total
-- /32 represents a single IP address
- While unusual, it is possible to have odd numbered split networks

Entire internet is a /0 network. This is why 0.0.0.0 matches the entire internet.

Eg. 10.16.0.0/16 = 10.16.0.0 => 10.16.255.255 -- Start to End of Network
- If you create /17 subnets from this...
-- 10.16.0.0/17 (1) = 10.16.0.0 => 10.16.127.255
-- 10.16.128.0/17 (2) = 10.16.128.255 => 10.16.255.255
- And so on. Think of it as splitting network ranges in half each time.

### DDOS Attacks - Distributed Denial of Service Attacks
A Distributed Denial of Service (DDoS) attack is a type of cyber attack where multiple compromised devices, often from different locations, are used to flood a targeted website or network with traffic, causing the website or network to become unavailable to its users

#### VLAN - Virtual Local Area Networking
Avoids forcing physical networking throughout an organization.

Frame Tagging (802.1Q & 802.1AD) - used for VLAN ID or VID
- 802.1Q allows multiple VLANs over the same L2 physical network
- If two 802.1Q VLANs over different connected networks have the same VLAN, 802.1AD adds new fields to VLAN to make same VLAN #'s unique
- One Switch can host multiple Broadcast Domains
- Trunk Port: Connection between 2 802.1Q capable devices
- Devices on different VLANs cannot communicate without a Layer 3 Device (router)

VLANs allow you to create separate L2 network segments to allow for Isolation
VLANs offer separate broadcast domains
802.1Q == VLANs
802.1AD (nested Q-in-Q VLANs)
Q-in-Q used in larger networks. .1Q for smaller networks.

### Decimal to Binary Conversion (IP Addressing)
In computer networking, IP (Internet Protocol) addresses are used to identify and communicate with devices on a network. IP addresses are typically represented in decimal notation, with four decimal numbers separated by periods (e.g. 192.168.1.1). However, computers process and transmit data in binary form, which is a sequence of 0s and 1s. To enable communication between devices, IP addresses must be converted from decimal to binary form, and vice versa. In this lesson, we will explore how to convert IP addresses from decimal to binary form and from binary to decimal form.
** for IPv4 Addressing

Eg. 133.33.33.7 -> Dotted decimal notation, which is what a human sees
- Computer sees 10000101.00100001.00100001.00000111

#### Decimal to Binary
Eg. 133.33.33.7 to binary. 
HINT: Use binary table https://www.networkacademy.io/ccna/ip-subnetting/converting-ip-addresses-into-binary
- 133, 33, 33, 7 are numbers each between 0 - 255. Tackle these sets of number individually. Each number in IP is 8 bits.
-- 133. If this number is less than Binary Position Value, write a 0. If equal or larger, minus binary position from your decimal number, add 1 in binary column (133 - 128 = 5. 
-- Position two is 5. 5 is less than 64, so write a 0. Position 3-5 are also less than 5. Put 0's
-- Position 6. Remaining value is 5, Binary Position Value is 4. 5 - 4 = 1. Put a 1 in position 6

BINARY VALUE of 133: [ 1 ][ 0 ][ 0 ][ 0 ][ 0 ][ 1 ][ 0 ][ 1 ]
BINARY VALUE of 33: [ 0 ][ 0 ][ 1 ][ 0 ][ 0 ][ 0 ][ 0 ][ 1 ]
BINARY VALUE of 33: [ 0 ][ 0 ][ 1 ][ 0 ][ 0 ][ 0 ][ 0 ][ 1 ]
BINARY VALUE of 7: [ 0 ][ 0 ][ 0 ][ 0 ][ 0 ][ 1 ][ 1 ][ 1 ]

#### Binary to Decimal
Eg. 10000101.00100001.00100001.00000111
- Break into 4 sections. Work left to right. Still using conversion table
1. 10000101. Match digit with corresponding position on table. [128][0][0][0][0][4][0][1] = 133
2. 00100001. [0][0][32][0][0][0][0][1] = 33
3. 00100001. [0][0][32][0][0][0][0][1] = 33
4. 00000111. [0][0][0][0][0][4][2][1] = 7

#### SSL & TLS
Secure Socket Layer (SSL) and Transport Layer Security (TLS) are two cryptographic protocols used to provide secure communication over the internet. SSL was developed by Netscape in the mid-1990s and TLS is its successor. These protocols are used to secure web traffic, email, instant messaging, and other types of internet traffic. SSL and TLS use a combination of symmetric and asymmetric encryption to encrypt data, ensuring that information transmitted over the internet is secure and cannot be intercepted by unauthorized parties.
- TLS is newer and more secure version of SSL

TLS ensures privacy; communications are encrypted. Asymmetric and then symmetric encryption. Aim for symmetric encryption. Part of TLS process is moving from asymmetric to symmetric encryption. Also verifies ID's of server or client/server. Also protects against alteration.
- Phases 1) Cipher Suites 2) Authentication 3) Key Exchange
1) Cypher Suites - Set of protocols upon TCP connection. Client/server need to agree on cipher suite to use
2) Authentication - Ensure server certificate is authentic. Certificate Authority issues these signed certificates
3) Key Exchange - Where we move from assymetric to symmetric encryption (becomes faster). Client generates pre-master key, encrypts it with servers public key and sends to server. The server decrypts the pre-master key using its private key.

#### BGP (Border Gateway Protocol)
Border Gateway Protocol (BGP) is a routing protocol used to exchange routing information between different networks on the internet. BGP is the protocol that enables the internet to function as a global network of interconnected networks. BGP is responsible for choosing the best path for network traffic to follow from one network to another, and for announcing that path to other routers on the internet
- BGP as a system is made up of self-managing networks known as Autonomous Systems (AS). AS's are black boxes that abstract away the detail of the network; BGP just needs to know network, as a whole, exists
- Each AS is allocated a number called ASN's. 16 bits in length. Allocated by IANA. Numbers 64,512 - 65,534 are private
- Operates over TCP port 179; it's reliable
- Not automatic, it's manually configured
- BGP is a path-vector protocol. It exchanges the BEST PATH between peers (aka shortest path), this path is called the ASPATH. This path is then 'trusted' and trust can be shared (AS's share trusted routes)
- iBGP and eBGP (internal BGP and external BGP). Either within an AS or between AS's
- AS Path Prepending can be used to artificially make one path look longer than another

In summary, an AS will advertise all the shortest paths it knows to all its peers, as the AS prepends its own AS number onto the path, this creates a source-to-destination path which BGP routers can learn and propogate.

#### Stateful VS Stateless Firewalls
Firewalls are an essential component of network security that help protect against unauthorized access and attacks. 
There are two primary types of firewalls: stateful and stateless
- Stateful: A stateful firewall is designed to monitor and track the state of network connections, keeping track of the status of individual network sessions to make more informed decisions about what network traffic to allow or deny
- Stateless: stateless firewall examines each individual network packet in isolation and makes decisions based on predetermined rules, without any awareness of the state of the network connection

Reminder: TCP (transmission control protocol) transfers IP packets using error correction and ports. REQUEST and RESPONSE: two components of a client-server connection.
- Request can be inbound or outbound. Response needs to be the inverse.

OUTBOUND VS INBOUND connections are based off perspective. Whether you're looking from eyes of client or server.
- Eg. User requesting cat photos from catigram.io... OB Request per User, IB Request per Server.

Stateless firewall doesn't understand the state of connections. A Stateless Firewall needs a separate rule for each inbound and outbound response (we see it as a single Connection, but Stateless doesn't see that; the Request and Response each need a separate rule). Inverse rule is required for the response in Stateless.

Stateful firewall is intelligent enough to identify the REQUEST and RESPONSE components of a connection as being RELATED. In this way, only the Request has to be ALLOWED or NOT, then the Response is automatically ALLOWED or NOT. This reduces admin overhead and chance of mistakes.

#### JumboFrames & MTU
What is a JumboFrame? Max V2 Frame size is 1500 bytes. Anything bigger is a JumboFrame (but generally max size 9000 bytes).

Imagine 4 EC2 instances. A/B and C/D connected. A/B standard frames, C/D JumboFrames
- Frame Payload and Frame Overhead (1500 bytes normal, 9000 bytes jumbo)
- Data split between frames. There's always space between frames (times when nothing is transmitted; downtime). With normal frames, you have more overhead with increased frames, and more wasted time on medium between increased frames. With JumboFrames, less combined Overhead and less downtime.
- To avoid Fragmentation, JumboFrames need to be the same size. Every step must also support JumboFrames.

##### Areas of AWS that do and don't support JumboFrames
DOES NOT:
- Traffic outside single VPC
- Traffic over an inter-region VPC peering connection
- Traffic over VPN connections
- Traffic over an internet gateway

DOES
- Same region peering
- Direct Connect
- Transit Gateway (up to 8500 bytes)

#### Application Firewalls (Layer 7 Firewalls)
Layer 7 firewalls, also known as application-layer firewalls, are a type of firewall that provides advanced security features by inspecting and filtering data at the application layer of the OSI (Open Systems Interconnection) model. Traditional firewalls, such as packet filtering or stateful inspection firewalls, operate at the network and transport layers and are only capable of filtering traffic based on IP addresses, port numbers, and protocol types. In contrast, layer 7 firewalls have the ability to analyze the content of network traffic, including application protocols such as HTTP, FTP, and SMTP, and can make more granular decisions about which traffic should be allowed or blocked.
- Normal Firewalls (Layer 3/4/5): Sees two flows of info: Request and Response. As this is Layer 3/4, the request/response are seen as separate. If you add session capability, request/response now seen as one session. They can't see into the data, it's just an opaque layer as the data is Level 7 (HTTP).
- Layer 7 Firewalls can see the data above layer 3/4/5. It can identify abnormal requests. Keeps all Layer 3/4/5 elements, but can react to L7 elements

#### IP Sec VPN Fundamentals
IPSEC, or Internet Protocol Security, is a suite of protocols used to secure Internet Protocol (IP) communications by authenticating and encrypting each IP packet. IPSEC is widely used to secure Virtual Private Networks (VPNs), remote access connections, and other types of network traffic.

##### Fibre Optic Cables
- Alternative way to transmit data VS copper cables. Fiber optic cables transmits light over glass/plastic medium (VS electric over copper). Fiber also resistance to electromagnetic interference and less prone to water ingress. Fiber is more consistent; better for higher speeds, larger distances, etc.
- Physical construction is cable and connector. 
- Fiber diameter expressed as X/Y eg. 9/125. X is diameter of core, Y is diameter of cladding (both in microns). Light bounces off inside of core, which is why its diameter is important. Core/cladding are for the data transmission. The buffer is a boundary surrounding the core for protection
- Single Mode and Multi-Mode Fiber
-- Single Mode. Small core, 8-9 microns, yellow jacket usually. Little bounce, little distortion. Best for high speed over long distance. Laser optics
-- Multi-mode. Bigger core, orange or aqua color jacket. Bigger core means wider range of light to use, and more bouncing. Different colors of light can be sent simultaneously. Creates more distortion over distance. Best for speed/cost effectiveness. LED optics
- Fiber Optic transceivers. How to connect to fiber. These are what generates and sends the light to/from fiber. Data -> Light -> Data
-- Transceivers also Mult- or Single-mode. Optimised for a cable type, need same kind at both ends

##### Encryption 101
Encryption is the process of converting data into a form that is unreadable to unauthorized users
- Encryption Approaches: 2
-- 1. Encryption at Rest. One party. Eg. Local laptop encrypting/decrypting data as it's written / read from disc. Used in cloud environments.
-- 2. Encryption In Transit. Protecting data as transferred between two places. Multiple individuals/systems involved Eg. Laptop to bank and back (applying encryption wrapper). 

- Concepts
-- Plain text (document, image, app), algorithm (plain text + encryption key = encrypted data), key (a 'password'), ciphertext created from all the previous stuff. Decrypt: ciphertext + key = plain text. 

- Symmetric
Same key used for both encryption and decryption processes. Transferring this key is the problem here.

- Asymmetric
Keys used in asymmetric encryption are also asymmetric
-- Asym keys are formed of twp parts: Public and Private keys. Only private key can decrypt data. No issue with public key being stolen as it is made to be accessible. Asym used with two parties involves where the two parties have never physically met before. Computationally more difficult than symmetric.

- Signing
Uses asymmetric keys to verify identity. Encryption doesn't prove identity, which is why Signing exists. Message gets signed with private key for verification.

- Steganography
It's obvious when data is encrypted; you can't hide it. Steganography is a process which addresses this -- hiding something in something else. Eg. cat data hidden in puppy image

#### Envelope Encryption
Envelope encryption is a technique used to secure data by encrypting it with multiple layers of keys

KMS (Key Management Services) - Used to encrypt data less than 4kb in size (other keys). Key Encryption Key (KEK). DEKs (Data Encryption Key) are created by KMS but not managed by KMS. KEK Asym or Sym. DEK always symmetric.
- Asym flexible but slow. Sym fast but difficult to move securely.

#### Hardware Security Modules (HSM)
Hardware Security Modules (HSMs) are physical devices designed to provide a high level of security and cryptographic processing to protect sensitive data and keys
- HSM isolated from main infrastructure. For cryptographic operations, you send the operations to the isolated HSM system. Keys created/stored/authenticatednever leave HSM. 
- Tamper proof and hardened against physical or logical attacks
- Role Separation (admins w/o full access)

#### Hash Functions & Hashing
Hash functions are mathematical algorithms that transform input data into a fixed-length string of characters, called a hash or message digest. Hashing is the process of applying a hash function to data to produce a unique and irreversible representation of the original data. Hash functions are widely used in computer security and cryptography for data integrity and authentication, digital signatures, password storage, and more. 

The main characteristics of a hash function are its one-way property, where it is easy to compute the hash value of the input data but computationally infeasible to reconstruct the original data from the hash value, and its collision resistance, where it is highly unlikely for two different inputs to produce the same hash value

#### How it works
- Data + Hashing Function = Hash
- Starts with hash function (MD5, SHA2-256)
- Data1 in -> Hash Function -> Hash1 out. Change 1 pixel in data and re-run, this creates Hash2
- Hashing is one way. Once you hash an image, you can't unhash it
- Same data in, same hash value out. But again, a single different byte or pixel creates a new hash
- MD5 hashing algo is too weak to be used in real-world systems
- Downloaded data can be verified using hash (to verify data is unaltered)
- Has the hash itself been altered? Digital Signing addresses this

##### Hashing Weakness
- Collision. If we hash image of a plane, then take another image and hash both... Should have different hash values. However, if both hash's match... Collision.
- Don't use MD5

#### Digital Signatures
Digital signatures are electronic signatures that are used to authenticate the integrity and authenticity of digital messages or documents
- Can sign using a Private Key for verification
- Two benefits when used with Hashing: verifies INTEGRITY of data and AUTHENTICITY of data (verify WHAT and WHO)

#### DNS - What does DNS do?
The Domain Name System (DNS) is a core part of most applications and IT systems

##### DNS 101: Functionality
If you visit netflix.com, the computers communicating don't use the namespace "netflix.com". Instead, this name is linked to an IP. DNS is what connects names to IPs. Basically, DNS is a huge DB that converts names to IP addresses

TIP: You MUST understand DNS to work in networking / AWS

##### DNS 101: Why do we need lots of DNS servers?
Problems with 1 (or a few) DNS servers: 
- Obvious risk problems. Bad actors could attack infrastructure
- Scaling problem (almost everyone uses DNS globally)
-- This demands a hierarchical structure

##### DNS 101: DNS Terms
DNS Zone. A database containing records (URLs etc)
ZoneFile. The "file" storing the zone on disk
Name Server (NS). DNS server which hosts 1 or more zones and stores 1 or more ZoneFiles
Authoritative. Contains real/genuine records (the boss)
Non-authoritative / Cached. Copies of records/zones stored elsewhere to speed things up

##### DNS 101: Hierarchical Design of DNS
- Starts with DNS Root (the boss)
- Root Zone - Contains high level info on top level domains (TLD), but no details. Root Zone points at name servers hosting TLD zones (which are run by registries like verisign). TLD stores high level info only on domains in that TLD. TLD points at NameServers. These NameServers are authoritative of the domains contained. Authoritative name servers point to the domain zones and zonefiles, which are subsequently authoritative. The zone prior knows a bit about the zone nested in it.

##### DNS 101: How DNS works
Core functionality of DNS: You have a person/device/service and you need to get the IP address of a domain. DNS's job allows you to locate the specific zone that can provide an authoritative response for your request (like visiting netflix.com)

How a query works:
1 - Querying for netflix.com
2 - First DNS local cache and host file of local machine is checked
3 - If local is unaware of query, we move to DNS Queries Resolver (type of DNS server within router or internet provider). This also has a local cache to check on. Results from here are non-authoritative
4 - Next is that the Queries Resolver queries Root Zone for netflix.com. Root Zone looks at NameServer Records and gets details from there
5 - Resolver can now query one of the .com TLD Name Servers. Details of DNS record from Netflix NS is returned to Resolver
6 - Now, Resolver queries netflix.com DNS Name Server. This can return an authoritative result. Result caches this result and returns result through to client
- End to end, this process is called 'walking the tree'

#### DNS 101: Registering a new domain
Process requires a few key entities: person registering, domain registrar, DNS hosting provider, TLD registry (Verisign), .com TLD Zone (managed by Verisign)
1 - pay for domain via domain registrar
2 - If registrar and hosting provider are same company, create a zone and get an NS
3 - If registrar and hosting provider are different, you'll be asked for NS zone info (which is configured separately)
4 - Register domain, supply Name Server info to TLD registry (Verisign)
5 - Verisign adds Name Server to the .com TLD zone, making domain live

Registrar VS Hosting Provider:
- Registrar has one purpose: let you purchase domains
- Hosting Provider operate DNS name servers which can host DNS zones. Allows you to manage content of those zones.
-- Some companies are either Registrars or HP's, some are both

#### DNS 101: DNSSEC
DNSSEC strengthens authentication in DNS using digital signatures based on public key cryptography. With DNSSEC, it's not DNS queries and responses themselves that are cryptographically signed, but rather DNS data itself is signed by the owner of the data
- Two improvements over DNS: 1) origin authentication (is the data from the correct entity), 2) data integrity protection (has the data been modified)
-- by creating cryptographically verifiable DNS Chain of Trust
-- DNSSEC is additive to DNS, not replacing DNS. DNS-only device won't receive DNSSEC results

##### How DNSSEC Works within a Zone
How it allows a DNSSEC to validate a resource within a zone (data integrity)

TERM: Resource Records Set (RRSE). icann.org zone has the following:  Resource Records (cname, A record, AAAA record, 4 MX records, mail exchange) -- 4 total resource record sets: cname, A, AAAA, MX. RRSETs are used within DNSSEC. DNSSEC looks at record sets, not individual records.
- RRSIG stores a digital signature for RRSET: Zone Signing Key (ZSK). This public/private key set is separate from the zone. ZSK is record #256. RRSIG validates RRSETS.
-- Uses digital signing and hashing

TERM: Key Signing Key (KSK, record #257). Ensures that a Zone Signing Key is trusted. The Private KSK creates an RRSIG from DNSKey (ZSK)

#### DNS 101: DNSSEC Chain of Trust
How the chain of TRUST is created between PARENT and CHILD zones within DNS

TERM: Delegated Signer (DS): Contains a HASH of the child domain's public KSK. Links the parent trust to the child.
- Root Zone Private Key / Signing Keys are explicitly trusted
- DNS Resolver can walk through the zones until establishing trust (from Root through to bottom)

#### DNS 101: DNSSEC Root Signing Ceremony
Controlling the keys of the internet. In case of Root Zone, there is no parent zone to provide trust -- we need a way to create this TRUST ANCHOR
- Key to internet: Private "." DNS Root Key Signing Key
-- This key is explicitly trusted by everything
- Ultimately, you're trying to get Root Zone RRSIG DNS Key

### CONTAINERS & VISUALIZATION

#### Kubernetes (K8)
Kubernetes, also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications

##### K8: Recovery Point Objective (RPO)
RPO is the max amount of data over time that can be loss before the loss exceeds what org can tolerate. Expressed in minutes or hours.
- Successful backups are known as Recovery Points
- Backups should occur as often or more than an RPO. Eg. If RPO is 6 hours, backups should occur at least once every 6 hours
- The lower the RPO, the more costly (more backups required)

##### K8: Recovery Time Objective (RTO)
RTO is the maximum tolerable length of time that a system can be down after a failure or disaster occurs

End to End Recovery: Recovery time of a system begins at the moment of failure and is only FIXED when handed back to business in a fully tested state

### DATA FORMATS & CONFIG FORMATS

#### YAML 101
YAML (short for "YAML Ain't Markup Language") is a lightweight, human-readable data serialization format that is often used for configuration files and data exchange between applications.
- Unordered collection of key:value pairs
- Indentations/spaces matter in YAML

YAML supports complex data structures, including lists, dictionaries, and nested structures, and it can be used with a wide range of programming languages and tools

Dictionary: Unordered data structure; key:value pair collection. Think key:value pairs with nested ones inside

#### JSON 101
JSON (short for "JavaScript Object Notation") is a lightweight data interchange format that is commonly used for data exchange between applications

In JSON, a dictionary is called an Object. A list is called an Array.

### CLOUD COMPUTING 101

#### What is cloud computing?
Cloud computing is a model for enabling ubiquitous, convenient, on-demand network access to a shared pool of configurable computing resources (e.g., networks, servers, storage, applications, and services) that can be rapidly provisioned and released with minimal management effort or service provider interaction. - National Institute of Standards and Technology (NIST) definition

To be cloud computing, meet these 5 characteristics / criteria:
1 - On-demand Self-service. Provision capabilities as needed without requiring human interaction
2 - Broad Network Access. Capabilities available over the network and accessed through the standard mechanisms
3 - Resource Pooling. There is a sense of location independence, no control / knowledge over exact location of resources. Resources pooled to serve multiple consumers using a multi-tenant model
4 - Rapid Elasticity. Capabilities can be elastically provisioned and released to scale rapidly outward / inward with demand. To the consumer, the resources avilable for provisioning appear to be unlimited
5 - Measured Service. Resource usage can be monitored, controlled, reported, and billed

#### Public vs Private vs Multi vs Hybrid Cloud
Public, private, hybrid, and multi-cloud are all viable options
- Public. Cloud available to the public.
- Private. Run from business on-premise *real* cloud.
- Hybrid. Private and public cloud cooperating together in a single environment (from same vendor usually). Not to be confused with 'hyrid environments / networking' (which is public cloud with legacy on-premise stuff)
- Multi-cloud. Using multiple public cloud environments (eg. AWS + Azure). Stay away from 'single management window/single pane of glass'; abstracts features abstracting down to common feature sets

#### Cloud Service Models Cloud Service Models (IAAS, PAAS, SAAS)
Terms & Concepts:
- Infrastructure Stack: Facilities, infrastructure, servers, virtualization, O/S, Container, runtime, Data, Application
- Unit of Consumption: What you use/pay for. This is what makes each service model below, different. Eg Virtual machine
- Infrastructure as a Service (IaaS): Provider manages facilities, infrastructure, servers, virtualization. You manage the rest. Unit of consumption is O/S or Virtual Machine
-- AWS EC2 uses IaaS
- Platform as a Service (PaaS): Provider manages facilities, infrastructure, servers, virtualization, O/S, Container, runtime. You consume the runtime environment.
- Software as a Service (SaaS): Provider manages facilities, infrastructure, servers, virtualization, O/S, Container, runtime, Data. You consume the application.
