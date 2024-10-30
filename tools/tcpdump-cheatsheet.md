# TCPdump Command Cheatsheet

## Basic Capture
- `tcpdump -i <interface>` - Capture interface
- `tcpdump -n` - Don't resolve names
- `tcpdump -nn` - Don't resolve names or ports
- `tcpdump -v` - Verbose output
- `tcpdump -vv` - More verbose
- `tcpdump -D` - List available interfaces
- `tcpdump -i any` - Capture on all interfaces

## Capture Filters
- `tcpdump host <host>` - Traffic to/from host
- `tcpdump src <host>` - Traffic from host
- `tcpdump dst <host>` - Traffic to host
- `tcpdump port <port>` - Traffic on port
- `tcpdump net <network>` - Network traffic
- `tcpdump tcp` - Only TCP traffic
- `tcpdump udp` - Only UDP traffic
- `tcpdump port 80 or port 443` - HTTP/HTTPS traffic
- `tcpdump not port 22` - Exclude SSH traffic
- `tcpdump 'tcp[tcpflags] & (tcp-syn) != 0'` - Capture SYN packets
- `tcpdump 'tcp[tcpflags] & (tcp-rst) != 0'` - Capture RST packets

## Output Options
- `tcpdump -w <file>` - Write to file
- `tcpdump -r <file>` - Read from file
- `tcpdump -c <count>` - Capture count packets
- `tcpdump -A` - ASCII output
- `tcpdump -X` - Hex and ASCII output
- `tcpdump -q` - Quick/brief output
- `tcpdump -t` - Don't print timestamp
- `tcpdump -tttt` - Print human-readable timestamp

## Common Troubleshooting Examples
- `tcpdump -i any -nn port 53` - DNS traffic
- `tcpdump -i any -nn 'tcp[tcpflags] == tcp-syn'` - TCP connection attempts
- `tcpdump -i any -nn dst port 80 or dst port 443` - Outbound web traffic
- `tcpdump -i any -nn 'icmp or icmp6'` - ICMP (ping) traffic
- `tcpdump -i any -nn '(tcp[tcpflags] & (tcp-syn|tcp-fin)) != 0'` - TCP connections start/end
- `tcpdump -i any -nn 'tcp[tcpflags] & (tcp-rst) != 0'` - Failed TCP connections
- `tcpdump -i any -nn greater 1000` - Packets larger than 1000 bytes
- `tcpdump -i any -nn src net 192.168.1.0/24` - Traffic from specific subnet

## Advanced Filters
- `tcpdump -i any -nn 'tcp[((tcp[12:1] & 0xf0) >> 2):4] = 0x47455420'` - HTTP GET requests
- `tcpdump -i any -nn 'tcp[((tcp[12:1] & 0xf0) >> 2):4] = 0x504F5354'` - HTTP POST requests
- `tcpdump -i any -nn 'ether host <MAC>'` - Traffic by MAC address
- `tcpdump -i any -nn 'ip[6] & 0x40 = 0x40'` - IPv4 fragmented packets
