# Chapter 3 - Introduction to TCP/IP

## DOD Model
- Separate model developed by Department of Defense/DARPA
- Layers roughly correlate with OSI model
- Process/Application Layer -- layer 5-7
- Transport/Host-to-Host Layer -- layer 4
- Internet Layer - layer 3
- Network Access/Link Layer - Layer 1-2

## Protocols
### Process/Application Protocols
- Telnet
- SSH
- FTP/TFTP
- SNMP
- HTTP/S
- NTP
- DHCP/BootP
  - DHCP process:
  - DHCP Discover -- client makes a layer 2/3 broadcast to ff:ff:ff:ff:ff:ff and 255.255.255.255
  - DHCP Offer -- server unicasts a response with offered IP
  - DHCP Request -- client broadcasts reply asking for that or other specified IP
  - DHCP Ack -- server unicasts an acknowledgement with DHCP options
  - DHCP conflicts -- server tries to ping address it's going to assign, host uses gratuitous ARP to confirm availability
- APIPA

### Transport/Host-to-Host layer Protocols
#### TCP -- Transmission Control Protocol
- Takes blocks of data and breaks into segments
- Initial TCP handshake establishes virtual circuit, agrees on window between ACKs
- Full-duplex communication, connection-oriented
- High overhead
- Format: 5+ 32-bit words
  - 16 bit source/destination ports
  - 32-bit sequence number
  - 32-bit acknowledgement number -- value expected next
  - 4-bit header length -- number of 32-bit words in header, sets where data begins
  - 1 reserved bit -- always set 0
  - 3 flag bits -- controls used to set up and terminate session
  - 16-bit window -- size of window sender accepts
  - 16-bit checksum -- CRC
  - 16-bit urgent pointer -- if set, indicates where non-urgent data begins
  - Options
  - Data
  
#### UDP -- User Datagram Protocol
- "thin" protocol -- relatively little overhead
- Used when overhead/speed is important or reliability is handled on an upper layer
- Doesn't establish virtual circuit, just sends data
- Format -- 2 32-bit words
  - 16-bit source port
  - 16-bit destination port
  - 16-bit length
  - 16-bit checksum
  - Data

#### Ports
- Below 1024 are "well-known" ports -- assigned in RFC 3232
- 1024 and above used to establish individual layer 4 sessions

### Internet Layer Protocols
- IP and other helper protocols (ARP, ICMP)

#### Internet Protocol (IP)
- Receives data from layer 4, fragments if necessary, sends
- Format -- 5+ 32-bit words
- 4-bit version
- 4-bit header length
- 8-bit priority/ToS
- 16-bit total length
- 16-bit header ID in case packet contains fragmented data
- 3 bits of flags -- identifies fragmentation
- 13-bit fragment offset -- provides fragmentation and reassembly
- 8-bit TTL -- determines lifespan of packet
- 8-bit protocol identifier -- port of layer 4 protocol
- 16-bit header checksum -- CRC for header only
- 32-bit source IP
- 32-bit destination IP
- 0 or 32-bit options list
- Data

#### ICMP
- Internet Control Message Protocol -- sends status/provides diagnostic functions
- Messages:
  - Destination Unreachable
  - Buffer Full/Source Quench
  - Hops/TTL Exceeded
  - ping
  - traceroute
  
#### ARP
- Address Resolution Protocol
- ties layer 3 logical addresses to layer 2 physical addressed
- functions via broadcast messages sent asking for which MAC is linked to which logical address

#### IP Addressing
- 32-bit numbers divided into 8-bit octets
- Divided into classes
  - Class A: First octet reserved for network bits, first bit must be 0 -- space between 0-127
  - Class B: First two octets reserved, first two bits must be 10 -- space between 128-191
  - Class C: First three octets reserved, first two bits must be 110 -- space between 192-223
  - Class D: Multicast addresses, 224-239
  - Class E: Research/experimental 240-255
- RFC 1918 sets private addressing space

#### Packet Types
- Layer 2 broadcasts -- sent via Ethernet broadcast, read by all hosts on network but /never/ forwarded
- Layer 3 broadcasts -- sent with IP broadcast address, read by all hosts, not forwarded /by default/
- Unicast -- packet intended for single hosts
- Multicast -- packet sent to multicast group address and only listened to by specific hosts -- others drop the traffic
