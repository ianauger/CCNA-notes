# Chapter 1 - Internetworking


### Concepts



*   Broadcast domain -- set of all devices able to receive a broadcast
*   Collision domain -- set of all devices where a collision can occur due to multiple send/receive transactions
*   Internetwork -- network composed of other, smaller networks
*   Models:
    *   OSI (Open Systems Interconnection) Model
    *   DOD (TCP/IP) model
    *   Both of above hierarchical/layered models


### Device Types



*   Hub -- repeated, rebroadcasts all packets.  All devices connected to it are in the same broadcast and collision domain.
*   Switch -- "intelligently" switches packets to only devices supposed to be receiving the packet.  One broadcast domain for entire device, one collision domain _per interface_.
*   Router -- Switches packets between logically distinct subnets.  1 broadcast domain and collision domain per interface.  Also selects paths for routing packets and filters packets.


## OSI Reference Model



*   OSI Seven Layer Dip -- 7 layers, 9 if you're sarcastic
*   Most devices only operate on a certain subset of the model


### Layer 7 -- Application



*   Layer closest to the user -- provides applications methods for traversing the full stack.
*   Confirms partner availability and required resources for communication


### Layer 6 -- Presentation



*   Translates data -- encodes to a generic format for sending
*   Includes protocols for standardized data transmission (compression, decompression, encryption, decryption, &c)


### Layer 5 -- Session



*   Sets up, manages, dismantles sessions (sound familiar?)
*   Manages keeping user data separate between sessions
*   Sets duplexing for higher layers


### Layer 4 -- Transport



*   _Segments _and reassembles datastreams
*   Handles end-to-end data transit, establishes _logical_ connections
*   Protocols on this layer: TCP and UDP


#### Connection-Oriented Communications



*   Three-way handshake to establish
    *   → SYN -- request for synchronization
    *   ← ACK -- acknowledgment and establishment of session parameters
    *   → SYN/ACK -- the terms are accepted and connection established
*   Sets flow control for data streams to ensure transmission over potentially congested networks
    *   Delivered segments are acknowledged by recipient and undelivered segments are resent
    *   Segments resequenced on arrival using sequence numbers
    *   Endpoint can send not ready/stop and ready/go signals to manage traffic flow
*   Connection oriented services _must_:
    *   Establish a virtual circuit over intervening topology
    *   Use sequencing, acknowledgement, and flow control
*   Windowing
    *   Session parameters establish how much sent data between acknowledgements
    *   TCP/IP uses # of bytes sent
*   Acknowledgement
    *   Receiver informs sender of lost data by transmitting next piece it expects
        *   E.g.: "I got 1-5, send 6 now"
        *   Or: "I got 1-4 and 6, send 5"
*   Session multiplexing
    *   Layer keeps different sessions separate so you don't get your Redtube in your VoIP


### Layer 3 -- Network



*   Manages _logical _addressing
*   Determines best route to move data in and out of a network
*   Routers live mostly on this layer
*   Unit of data is the _packet_
    *   Data packets
    *   Route update packets
*   Routing tables store, on a basic level:
    *   Network address of reachable network
    *   Which interface that network is attached to
    *   The "distance" to that network
*   Routers also…
    *   Don't forward broadcast/multiplex traffic by default
    *   Use the _logical_ address to determine destination, not physical
    *   Can implement ACLs
    *   Can bridge/route through the same interface
    *   Can route VLANs
    *   Provide QOS


### Layer 2 -- Data Link



*   Provides physical data transmission
*   Handles…
    *   Error notification
    *   Physical topology
    *   Flow control over local network
*   Encapsulates packets in _frames_ with physical address in header
*   Standards:
    *   Media Access Control: 801.11, 802.3
    *   Logical Link Control: 802.2
*   Sublayers
    *   Media Access Control
        *   Controls _access_ to _media _-- how packets are placed on the physical network (duh, mcfly!)
        *   Bandwidth first come first served
        *   Defines physical addressing and logical topology (signal path through physical topology)
        *   Sets line discipline, error notification (not correction), ordered delivery, and flow control
    *   Logical Link Control
        *   Identifies relevant layer 3 protocol and encapsulates appropriately
        *   Header with logical address tells recipient what to do with frame
        *   Provides flow control/control bit sequencing
*   Switches/bridges live here
*   Switches segregate traffic by looking at logical address and matching to entry on ARP table, then forwarding the frame out the appropriate interface
*   If entry not found on ARP table, switch forwards frame out _all_ interfaces and seeing if anyone acknowledges it -- ARP table then populated with new entry
*   Otherwise, only broadcasts forwarded by default


### Layer 1 -- Physical



*   Provides for sending and receiving bits
*   Layer 1 protocols specify electrical, mechanical, procedural, and functional requirements for the above
*   Interface between DTE/DCE identified at this layer
    *   DTE -- Data Terminal Equipment (usually at prem)
    *   DCE -- Data Communication Equipment (usually at service provider end)
    *   Network connected to DTE/DCE via CSU/DSU (Channel Service Unit/Data Service Unit -- fancy word for "the modem")
*   Physical layer connections defined by OSI standards -- only one concerned in CCNA is IEEE Ethernet.
*   Hubs operate at this layer


#### Physical Topologies



*   Bus
*   Ring
*   Star
*   Mesh

<!-- GD2md-html version 1.0β11 -->
