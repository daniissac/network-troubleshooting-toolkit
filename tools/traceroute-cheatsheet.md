# Traceroute Command Cheatsheet

## Basic Syntax
- `traceroute <host>` - Basic traceroute
- `traceroute -n <host>` - No DNS resolution
- `traceroute -w <seconds> <host>` - Wait time
- `traceroute -q <queries> <host>` - Number of queries
- `traceroute -m <max_ttl> <host>` - Maximum hops

## Protocol Options
- `traceroute -I <host>` - Use ICMP
- `traceroute -T <host>` - Use TCP
- `traceroute -U <host>` - Use UDP
- `traceroute -p <port> <host>` - Specify port

## Advanced Features
- `traceroute -A <host>` - AS path lookup
- `traceroute -g <gateway> <host>` - Loose source route
- `traceroute -r <host>` - Bypass routing tables

## Common Issues and Solutions
- `traceroute -f <first_ttl> <host>` - Start from specific TTL (skip early hops)
- `traceroute -M <method> <host>` - Use specific probe method
- `traceroute -4 <host>` - Force IPv4
- `traceroute -6 <host>` - Force IPv6

## Troubleshooting Tips
- `traceroute -d <host>` - Enable socket level debugging
- `traceroute -i <interface> <host>` - Specify network interface
- `traceroute -s <source_ip> <host>` - Use specific source IP
- `traceroute -F <host>` - Don't fragment packets

## Output Interpretation
- `*` - No response (timeout)
- `!H` - Host unreachable
- `!N` - Network unreachable
- `!P` - Protocol unreachable
- `!X` - Communication administratively prohibited
- `!S` - Source route failed
- `!F` - Fragmentation needed

## Alternative Tools
- `mtr <host>` - Continuous traceroute
- `tracepath <host>` - Similar to traceroute but no root needed
- `paris-traceroute <host>` - More accurate for load-balanced paths
