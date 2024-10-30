# Wireshark Cheatsheet

## Display Filters
### Basic Filters
- `ip.addr == 192.168.1.1` - Traffic to/from IP
- `ip.src == 192.168.1.1` - Traffic from IP
- `ip.dst == 192.168.1.1` - Traffic to IP
- `tcp.port == 80` - TCP port traffic
- `http` - HTTP traffic only
- `dns` - DNS traffic only
- `!arp` - Exclude ARP traffic

### Protocol Filters
- `tcp` - TCP traffic
- `udp` - UDP traffic
- `icmp` - ICMP traffic
- `ssl` or `tls` - SSL/TLS traffic
- `ftp` - FTP traffic
- `ssh` - SSH traffic
- `telnet` - Telnet traffic

### Logical Operators
- `and` or `&&` - Both conditions
- `or` or `||` - Either condition
- `not` or `!` - Negate condition
- `contains` - Contains string
- `matches` - Regex match

## Capture Filters
- `host 192.168.1.1` - Capture specific host
- `net 192.168.0.0/24` - Capture subnet
- `port 80` - Capture port
- `src host 192.168.1.1` - From specific host
- `dst host 192.168.1.1` - To specific host
- `tcp port 80` - TCP specific port

## Analysis Tools
### Statistics
- Statistics → Protocol Hierarchy
  - Shows breakdown of protocols by packets/bytes
  - Useful for identifying dominant protocols
- Statistics → Conversations
  - Shows traffic between pairs of addresses
  - Can sort by bytes, packets, or duration
- Statistics → Endpoints
  - Lists all active network endpoints
  - Shows bytes sent/received per host
- Statistics → I/O Graph
  - Visualizes traffic patterns over time
  - Customizable with multiple graphs and filters
- Statistics → Flow Graph
  - Displays packet flow between endpoints
  - Shows request/response sequences

### Expert Info
- Analyze → Expert Information
  - Automatically detects network issues
  - Provides detailed analysis of problems
- Colors indicate severity:
  - Red: Error
    - TCP reset, malformed packets
    - Application errors
  - Yellow: Warning
    - Retransmissions
    - Window size problems
    - Slow response times
  - Cyan: Note
    - TCP window updates
    - Zero window conditions
    - Protocol sequences
  - Green: Chat
    - Connection establishments
    - Normal protocol behavior
    - Standard operations


## Keyboard Shortcuts

### Navigation
- `Ctrl + .` - Go to next packet
- `Ctrl + ,` - Go to previous packet
- `Ctrl + G` - Go to packet number
- `Ctrl + B` - Back in history
- `Ctrl + F` - Forward in history

### Display
- `Ctrl + +` - Zoom in
- `Ctrl + -` - Zoom out
- `Ctrl + 0` - Reset zoom
- `Spacebar` - Page down
- `Shift + Spacebar` - Page up

### Analysis
- `Ctrl + T` - Time reference
- `Ctrl + E` - Prepare filter
- `Ctrl + R` - Start capture
- `Ctrl + K` - Start capture
- `Ctrl + S` - Save capture

## Follow Streams
- Right-click → Follow → TCP Stream
- Right-click → Follow → UDP Stream
- Right-click → Follow → SSL Stream
- Right-click → Follow → HTTP Stream

## Time Display Formats
- Seconds since epoch
- UTC date/time
- Local date/time
- Delta time
- Delta time displayed
- Relative time

## Useful Tips
### Finding Problems
1. Check for TCP Retransmissions:
   `tcp.analysis.retransmission`
2. Look for TCP Reset flags:
   `tcp.flags.reset == 1`
3. Find HTTP errors:
   `http.response.code >= 400`
4. Detect duplicate ACKs:
   `tcp.analysis.duplicate_ack`

### Performance Analysis
1. Round Trip Time:
   `tcp.analysis.ack_rtt`
2. Window Size:
   `tcp.window_size`
3. TCP Zero Window:
   `tcp.analysis.zero_window`

### Security Analysis
1. Find SSL/TLS errors:
   `ssl.alert`
2. Detect port scans:
   `tcp.flags.syn==1 && tcp.flags.ack==0`
3. Find malformed packets:
   `_ws.malformed`
