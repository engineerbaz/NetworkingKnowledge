
# IPv6 - Internet Protocol Version 6

## Introduction & Basics
- Huge Address
- Simple Packet space
- AutoConfiguratin and readdressing
- Hierarchical network structure
- End to end Security support
- QoS
- Mobility

## Address Format
- 128 bit Long
- seprated by colon (:)
- Eight group 
- Hexadecimal digits
- like 2031:0000:0000:130F:0000:09C0:876A:130B
- Can be in compressed Format
  - Any Zero at the beginning of a group can be omitted
    - 2031:0:130F:0:0:9C0:876A:130B
  - A double colon (::) can be using in IPv6 address when two or more consective group contain all Zeros
    - 2031:0:130F::9C0:876A:130B

## Address Structure
- Same like v4, It has 2 parts 
  - Network
  - interface ID : corresponds to host ID
- Interface ID can be configured 
  - Manually Configuration
  - automatically generated through System Software
  - generated in IEEE 64-bit Extended Unique Identifier (EUI-64) Format
    - MAC is 48 bit = 24 bit (Vendor ID) + 24 bit (Vendor Number)
    - In EUI64  = Spilt 48bit in half 
    - Add 16 bits 1111 1111 1111 1110 (FF FE)
    - Also chage 7th group as 1 in first part.
    - 

## IPv6 Address Classification
- Unicast
  - Identifies an interface. Packet sent to an IPv6 Unicast delivered
- Multicast
  - Identifies a group of interfaces. 
- Anycast
  - Identifies a group of interfaces. Packet sent to an anycast address are delivered to the nearest interface taht is Identified by the anycast depending on routing protocol
  - IPv6 anycast & Unicast address use same address space

### Global Unicast Address 
- Consist of Global routing prefix, subnet ID & Interface ID
- [001 Global Routing prefix] [Subnet ID][Interface ID]
- [Provider (M bit)] [Site (N bit)][Host (128-M-N bit)]
 

#### Link Local  
- For communication in same network
- starts FE80::/10
- Not global , no routing possible
- [FE80:: 0][Interface ID]
- [64 bit] [64 bits]


#### Unique local Address
- SImilar to IPv4 Private Address
- Has Unique local prefix DC00::/7
- No possiblity for this Address to implement the E2E feature of v6
- [Prefix | L ] [Global ID][Subnet ID] [Interface ID]
- [7 bit | 1 bit] [40 bit)][16 bit][16 bit]
 
#### Other Unicast Address
- Unspecified Address
  - 0:0:0:0:0:0:0:0/128 or ::/128
  - Indicates that an Interface or a node Doesnt have IP 
- Loopback Address
  - 0:0:0:0:0:0:0:1/128 or ::1/128
  - same as IPv4 127.0.0.1
  - Loopback cant be used as source or destination IP address of Packet to be forwarded

### Multicast address 
- Similar to IPv4 Multicast
- Consists of a prefix, flag, scope and Multicast group ID
- starts with FF00::/8
  - Node-local
    - For all nodes FF01:0:0:0:0:0:0:1
    - For all router FF01:0:0:0:0:0:0:2
  - Link-local
    - For all nodes FF02:0:0:0:0:0:0:0:1
    - For all router FF02:0:0:0:0:0:0:0:2
    - For Solicated-node : FF02:0:0:0:0:0:1:FFXX:XXXXX
    - For OSPF routers: FF02:0:0:0:0:0:0:0:5
    - For OSPF DRs: FF02:0:0:0:0:0:0:0:6
    - For all RIP router : FF02:0:0:0:0:0:0:9
    - For PIM router : FF02:0:0:0:0:0:0:D
- [8 bit][4 bit][4 bit][80 bit][32 bit]
- [FF00][Flag][Scope][Reserved must be Zero][Group ID]

### Anycast
- Like Same as Unicast but connect to nearest router
- Subnet-router Anycast address
  - Packet sent to a subnet-router Anycast address are delivered to nearest router on subnet Identified by Anycast address
    - [N bits][128- N bits]
    - [Subnet Prefix][0]

## IPv6 Packet Format - Basic Header 
- 3 part 
  - Basic 
    - 40 byte long and 8 fields
  - Extention
    - Variable Length
    - for additional features
    - Next Header is 8 byte .. 
    - it can be 1 0r 2 EH
      - Hop-by-Hop, Routing, auth, etc
  - PDU (Packet Data Unit) 

- Version (Version 6 = 0110)
- 
- 

### ICMPv6 
- Expect ping , it also do neighbour discovery (ID), duplicate address detection (DUD)
- Hexa 3a = ICMPv6
- Error on ICMPv6
  - destination unreachable (type 1)
    - Packet cant be transferred
  - Packet too bing (Type 2)
    - Size too big  & exceeed link MTU of outbound interface
  - Time exceeded (Type 3)
    - Value ot hop limit is 0
    - resonably time is longer than specified period 
  - Parameter Problem   (Type 4)
    - basic or Extention header r long
 
 - Classification of ICMPv6 inform message
   - Echo Request 
     - Sent to destination nodes. after recieving echo reguest, destination node respond with echo reply message
   - Echo reply
     - After recieving an Echo Request message, destination node respond with echo reply

