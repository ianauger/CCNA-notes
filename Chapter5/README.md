# VLSM, Summarization, and Troubleshooting TCP/IP

## Variable Length Subnet Masks (VLSMs)
- Older routing protocols do not have ability to exchange subnet information
- Assumed that all routable networks use the same mask
- "classful" routing
- Variable-length subnets supported in more recent protocols -- allow for mixing and matching of subnet lengths
- Helps conserve IP space -- you can use a small subnet for a small network, and a large subnet for a large network
- Helpful to fill out a VLSM table -- subdivide a larger block into smaller chunks you can then reserve for subnets to prevent overlap

## Summarization
- Advertisement of many nets as one, providing a summarized route -- cuts down on routing table size
- Usually best to tailor to smallest possible block of summarized routes -- all subnets in the block will use the same route

## Troubleshooting
- Tackle in steps -- follow until you find where things stop working.
- Cisco steps:
  - Ping loopback address -- ensures TCP/IP stack is up
  - Ping local IP and check local config -- tests local NIC functionality
  - Ping default gateway -- ensures local network functionality
  - Ping remote IP -- tests layer 1-3 end to end
