# Network Log Analysis Cheatsheet

## System Logs Location
### Linux
- `/var/log/syslog` - General system logs
- `/var/log/auth.log` - Authentication logs
- `/var/log/secure` - Security logs
- `/var/log/messages` - Global system messages
- `/var/log/dmesg` - Device/driver messages
- `/var/log/kern.log` - Kernel logs
- `/var/log/boot.log` - System boot logs
- `/var/log/maillog` - Mail server logs
- `/var/log/cron` - Cron job logs
- `/var/log/audit/audit.log` - Audit daemon logs

### Network Service Logs
- `/var/log/apache2/` - Apache logs
- `/var/log/nginx/` - Nginx logs
- `/var/log/haproxy.log` - HAProxy logs
- `/var/log/openvpn/` - OpenVPN logs
- `/var/log/iptables.log` - Firewall logs
- `/var/log/fail2ban.log` - Fail2ban logs
- `/var/log/squid/` - Squid proxy logs
- `/var/log/mysql/` - MySQL database logs
- `/var/log/postgresql/` - PostgreSQL database logs
- `/var/log/docker/` - Docker container logs

## Log Analysis Commands
### Basic Commands

# Follow log file in real-time
tail -f /var/log/syslog

# Search for errors
grep "error" /var/log/syslog

# Follow log with less
less +F /var/log/auth.log

# View systemd journal logs
journalctl -f

# View last 100 lines
tail -n 100 /var/log/syslog

# View first 100 lines
head -n 100 /var/log/syslog


### Advanced Filtering

# Extract failed password attempts with timestamp and IP
awk '/Failed password/ {print $1,$2,$3,$11}' /var/log/auth.log

# View logs between specific times
sed -n '/Jan 12 10:00/,/Jan 12 11:00/p' /var/log/syslog

# Recursive search for connection refused
grep -r "Connection refused" /var/log/

# Count occurrences of pattern
grep -c "error" /var/log/syslog

# Case-insensitive search
grep -i "warning" /var/log/syslog


### Real-time Monitoring

# Monitor failed password attempts
watch 'grep -c "Failed password" /var/log/auth.log'

# Monitor nginx access log
watch 'tail -n 20 /var/log/nginx/access.log'

# Monitor system load
watch 'cat /proc/loadavg'

# Monitor disk I/O
watch 'iostat'


### Log Rotation and Management

# Check logrotate configuration
logrotate -d /etc/logrotate.conf

# Force log rotation
logrotate -f /etc/logrotate.conf

# View logrotate status
cat /var/lib/logrotate/status


### Network-Specific Logs

# View connection tracking
cat /proc/net/nf_conntrack

# Check network interface logs
dmesg | grep eth0

# View DNS server logs
journalctl -u named

# Monitor VPN logs
tail -f /var/log/openvpn/openvpn.log

# View firewall logs
tail -f /var/log/iptables.log


### Performance Analysis

# Network interface statistics
sar -n DEV 1

# TCP retransmission statistics
netstat -s | grep -i retransmitted

# Network interface errors
ifconfig | grep -i error

# Check network connections
ss -s


### Security Event Monitoring

# Monitor authentication failures
grep "authentication failure" /var/log/auth.log

# Check UFW firewall blocks
grep "UFW BLOCK" /var/log/syslog

# Monitor sudo usage
grep "sudo" /var/log/auth.log

# Check SSH login attempts
grep "sshd" /var/log/auth.log


### Log Analysis Tools
- `logwatch` - Automated log analysis and reporting
- `fail2ban-client` - Intrusion prevention system
- `goaccess` - Real-time web log analyzer
- `lnav` - Advanced log file navigator
- `splunk` - Enterprise log management
- `elastic stack` - Log collection, analysis, and visualization
- `prometheus` - Metrics collection and alerting
- `grafana` - Metrics visualization

### Useful One-Liners

# Top IP addresses in access log
awk '{print $1}' access.log | sort | uniq -c | sort -nr | head -n 10

# HTTP status code distribution
awk '{print $9}' access.log | sort | uniq -c | sort -rn

# Failed SSH attempts by IP
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -nr

# Large file transfers
awk '$10 > 1000000' access.log | awk '{print $7,$10}'

# 404 errors in last hour
awk -v date=$(date -d "1 hour ago" +[%d/%b/%Y:%H:%M:%S) '$4 > date && $9 == "404"' access.log


## Best Practices
1. Regular Log Rotation
   - Configure appropriate rotation intervals
   - Set up compression for archived logs
   - Maintain adequate retention periods

2. Timestamp Synchronization
   - Use NTP for accurate timestamps
   - Configure correct timezone settings
   - Regular time sync verification

3. Centralized Logging
   - Set up log aggregation servers
   - Implement secure log transmission
   - Configure redundant storage

4. Security Measures
   - Implement log file permissions
   - Enable log file integrity monitoring
   - Set up log backup encryption

5. Monitoring and Alerting
   - Configure threshold-based alerts
   - Set up real-time monitoring
   - Implement escalation procedures

## Log Format Examples
### Syslog Format

Jan 12 10:00:00 hostname service[PID]: message


### Apache/Nginx Access Log

IP - - [timestamp] "REQUEST" STATUS_CODE BYTES "REFERRER" "USER_AGENT"


### SSH Authentication

Jan 12 10:00:00 hostname sshd[PID]: Accepted publickey for user from IP port PORT


### MySQL Error Log

YYYY-MM-DD HH:MM:SS [ERROR] [Server] Error message


### Docker Container Log

YYYY-MM-DD HH:MM:SS.SSSSSS Container_ID: Message