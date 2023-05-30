 ## DEMO - Custom VPCs - Create VPC - Overview
 - VPCs are regionally isolated and regionally resilient service. Operates from all AZs in that region.
 - Nothing is allowed IN or OUT of a VPC without explicit permission; provides isolated blast radius; if you have a proble inside a VPC, the impact is limited to that VPC and/or anything connected
 - Custom VPCs allow for simple or multi-tier; flexible configuration
 - Custom VPCs also provide Hybrid Networking
 - When you create VPC, you can pick DEFAULT or DEDICATED tenancy. AKA shared or dedicated hardware
 -- If you pick DEFAULT tenancy, you can choose on a per resource basis later on when provisioning resources whether it's shared or dedicated hardware
 -- If you pick DEDICATED tenancy at VPC level, it's locked in. Any resources created inside the VPC have to be on dedicated hardware (cost premium compared to Default)
 - By default, VPC uses IPv4 private/public IPs. The private CIDR block is main method of IP communication for VPC, & Puclic IPs (when you want make resources public)
 - VPC allocated ONE mandatory Private IPv4 CIDR Block
 -- Primary Block has two main restrictions: min /28 (16 IPs), max /16 (65,536 IPs)
 -- Optional to add secondary IPv4
 - Optional: VPC can use IPv6 by assigning /56 IPv6 CIDR to VPC (start appliny IPv6 as default as this is what's being adopted now)
 -- IMPORTANT: You can't pick a block of IP ranges like IPv4. Your range is either allocated by AWS, or customer can use their OWN IPv6 range 
 -- IPv6 doesn't have Public/Private concept, the range is all Publicly routable by default

### DEMO - Custom VPCs - Create VPC - DNS
 VPCs also have DNS. provided by R53
 - DNS is 'Base IP + 2', so if VPC is 10.0.0.0, then DNS IP is 10.0.0.2
 EXAM: 
 - Two critical options for how DNS functions in a VPC
 -- 1. First is a setting called enableDnsHostnames - Gives instances public DNS names
 -- 2. enableDnsSupport setting. Enables DNS resolution in VPC. Indicates whether DNS is enabled or disabled in VPC. If enabled, instances in VPC can use the DNS IP address
 
 ## DEMO pt.1 - Custom VPCs - Create/Configure VPC
 Steps through the architecture and features of Custom VPCs including the main issues which are raised in the exam
 
 ### STEPS pt.1
 1. Create the VPC: VPC > Your VPCs > Create VPC > select VPC Only > name tag "a4l-vpc1" > IPv4 CIDR "10.16.0.0/16" > IPv6 CIDR block "Amazon-provided IPv6 CIDR block", default us-east-1 > Tenancy set to Default > Create VPC
 2. VPC Settings: In VPC > Actions dropdown, "Edit VPC Settings" > DNS Settings check both Enable DNS Resolution and Enable DNS Hostnames < Save (for any resources in this custom VPC, if they have puclic IP addresses, they'll also get public DNS names)
 
 ## DEMO pt.2 - Custom VPCs - VPC Subnets
 Subnets are what services run from inside VPCs, within a particular Availability Zone. They're how you add function, structure, and resilience to VPCs
 NOTE: With AWS diagrams, color Blue is private and Green is for Public (green = Go = Public)
 - Subnets in a VPC start off Private and take config to make Public
 - Subnets are AZ Resilient. Created within on AZ and can never be changed. If AZ fails, subnet (and any contained services) fails
 EXAM: Subnet can NEVER be in multiple AZs. 1 subnet is in 1 AZ. An AZ can have 0 or more subnets
 - Default IP for subnet is IPv4 and is allocated an IPv$ CIDR, this CIDR is a subset of the VPC CIDR Block (has to be within VPC allocated range)
 EXAM: CIDR that a subnet uses cannot overlap with any other subnets in the VPC
 - Subnet can optionally be allocated IPv6 CIDR (/64 subset of the /56 VPC, space for 256 /64 ranges that each subnet can use. Note: VPC must also be config'd for IPv6
 - By default, subnets in a VPC can communicate with other subnets in the same VPC

 ### DEMO pt.2 - Custom VPCs - VPC Subnets - Subnet IP addressing
 - 5 IPs inside every VPC subnet are RESERVED
 -- Example: Subnet is 10.16.16.0/20, range of 10.16.16.0 -> 10.16.31.255
 --- Unusable Addresses: Network Address (10.16.16.0) - NOTE: Not just AWS, NOTHING uses first address on any IP networks
 --- Unusable Addresses: 'Network+1' Address (10.16.16.1) - VPC Router; logical network device that moves data between subnets
 --- Unusable Addresses: 'Network+2' Address (10.16.16.2) - Reserved VPC address, but generally for DNS
 --- Unusable Addresses: 'Network+3' Address (10.16.16.3) - Reserved Future Use
 --- Unusable Addresses: Network Broadcast Address (10.16.31.255) - LAST IP in subnet
 EXAM: if a subnet has 16 usable IPs... it actually only has 11, because 5 are reserved (3 for AWS (+1, +2, +3, 1 network (1st IP in range), one broadcast (last IP in range))
 - Dynamic Host Configuration Protocol (DHCP). VPC has a configuration object applied to it called DHCP Option Set. It's how computing devices receive IP address  automatically. 1 DHCP option set applied to a VPC at a time and flows through to Subnets. You can create DHCP option sets, but you CANNOT edit them. To change  settings, create a new DHCP and change the VPC allocation to the new DHCP Option Set.
 - On every subnet, you can define two IP Allocation Options: 1. auto-assign public IPv4 address 2. auto-assign an IPv6 address

 ### STEPS pt.2 - Creating lots of subnets
 3. Create Multiple Subnets with VPC multi-tier structure: VPC > Subnets > Create subnet > Select VPC (a4l-vpc1) > subnet name "sn-reserved-A" > IPv4 CIDR block "10.16.0.0/20" > IPv6 CIDR block, choose the one option, fill in unique IPv6 value for the respective subnet (00 for first one) > Add New Subnet > Repeat for each subnet in the AZ (4 total) > Verify Details in each > Create Subnet. Repeat for AZB, AZC.
 4. Auto allocate IPv6 Addressing: select sn-app-A > Actions drop down, "Edit Subnet Settings" > Auto-assign IP settings, check "Enable auto-assign IPv6 address" > Save > Do this for all new subnets
