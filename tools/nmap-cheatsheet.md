# Nmap Command Cheatsheet

## Basic Scans
- `nmap <target>` - Basic scan
- `nmap -sP <network>` - Ping scan
- `nmap -p <port> <target>` - Specific port
- `nmap -p- <target>` - All ports
- `nmap -F <target>` - Fast scan

## Scan Types
- `nmap -sS <target>` - SYN scan
- `nmap -sT <target>` - TCP connect scan
- `nmap -sU <target>` - UDP scan
- `nmap -sV <target>` - Version detection
- `nmap -O <target>` - OS detection

## Output Options
- `nmap -oN <file> <target>` - Normal output
- `nmap -oX <file> <target>` - XML output
- `nmap -oG <file> <target>` - Grepable output
