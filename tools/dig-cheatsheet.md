# Dig Command Cheatsheet

## Basic Queries
- `dig <domain>` - Standard query
- `dig +short <domain>` - Brief output
- `dig +noall +answer <domain>` - Show only answer
- `dig @<nameserver> <domain>` - Query specific nameserver

## Record Types
- `dig <domain> A` - IPv4 records
- `dig <domain> AAAA` - IPv6 records
- `dig <domain> MX` - Mail records
- `dig <domain> NS` - Nameserver records
- `dig <domain> SOA` - Start of Authority
- `dig <domain> TXT` - Text records
- `dig <domain> ANY` - All records
- `dig <domain> CNAME` - Canonical name records
- `dig <domain> PTR` - Pointer records
- `dig <domain> SRV` - Service records

## Advanced Options
- `dig +trace <domain>` - Trace DNS path
- `dig -x <IP>` - Reverse lookup
- `dig +dnssec <domain>` - DNSSEC info
- `dig +norecurse <domain>` - Disable recursive query
- `dig +tcp <domain>` - Force TCP instead of UDP

## Troubleshooting Options
- `dig +stats <domain>` - Show query statistics
- `dig +tries=N <domain>` - Set number of query attempts
- `dig +time=N <domain>` - Set query timeout
- `dig +multiline <domain>` - Verbose multi-line output
- `dig +nocmd +noall +answer <domain>` - Clean output for scripting

## Response Section Control
- `dig +noauthority <domain>` - Hide authority section
- `dig +noadditional <domain>` - Hide additional section
- `dig +noquestion <domain>` - Hide question section
- `dig +nostats <domain>` - Hide statistics section

## Common Troubleshooting Commands
- `dig +trace +noadditional <domain>` - Clean trace of DNS path
- `dig +short @8.8.8.8 <domain>` - Quick check using Google DNS
- `dig +noall +answer +tries=2 +time=2 <domain>` - Fast fail query
- `dig +dnssec +cd <domain>` - Check DNSSEC validation
- `dig +short mx <domain>` - Quick mail server check
