# Ping Command Cheatsheet

## Basic Syntax
- `ping <host>` - Standard ping
- `ping -c <count> <host>` - Specific number of pings
- `ping -i <interval> <host>` - Set interval between pings
- `ping -s <size> <host>` - Set packet size
- `ping -t <ttl> <host>` - Set Time To Live
- `ping -q <host>` - Quiet output
- `ping -f <host>` - Flood ping
- `ping -w <deadline> <host>` - Set timeout

## Advanced Options
- `ping -R <host>` - Record route
- `ping -v <host>` - Verbose output
- `ping -b <broadcast>` - Ping broadcast address
- `ping -I <interface> <host>` - Use specific interface

## Troubleshooting Scenarios
- `ping localhost` - Test local TCP/IP stack
- `ping 127.0.0.1` - Test loopback interface
- `ping -c 1 <host>` - Quick check if host is alive
- `ping -n <host>` - Numeric output only, no DNS resolution
- `ping -4 <host>` - Force IPv4
- `ping -6 <host>` - Force IPv6
- `ping -D <host>` - Print timestamp before each line
- `ping -O <host>` - Report outstanding replies

## Network Performance Testing
- `ping -f <host>` - Flood ping (requires root)
- `ping -A <host>` - Adaptive ping
- `ping -Q <tos> <host>` - Set Quality of Service
- `ping -l <preload> <host>` - Send packets as fast as possible

## Common Issues and Solutions
1. 100% packet loss:
   - Check physical connectivity
   - Verify firewall settings
   - Confirm correct IP address
   
2. High latency:
   `ping -c 10 <host>` - Check for consistent high times
   
3. Intermittent connectivity:
   `ping -c 100 -i 0.2 <host>` - Rapid pings to detect drops

## Examples
1. Ping with 1500 byte packets:
   `ping -s 1500 8.8.8.8`
2. Send 5 pings with 2-second intervals:
   `ping -c 5 -i 2 google.com`
3. Debug routing issues:
   `ping -R -v <host>`
4. Test MTU issues:
   `ping -M do -s 1472 <host>`
5. Long-term monitoring:
   `ping -D -O -i 60 <host>`
