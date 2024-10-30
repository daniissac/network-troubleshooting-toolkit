# CURL Command Cheatsheet

## Basic Syntax
- `curl <url>` - Basic GET request
- `curl -o <file> <url>` - Save output to file
- `curl -O <url>` - Save with remote filename
- `curl -I <url>` - Headers only
- `curl -i <url>` - Include headers in output
- `curl -L <url>` - Follow redirects
- `curl -C - <url>` - Resume download
- `curl --compressed <url>` - Request compressed response

## HTTP Methods
- `curl -X GET <url>` - GET request
- `curl -X POST <url>` - POST request
- `curl -X PUT <url>` - PUT request
- `curl -X DELETE <url>` - DELETE request
- `curl -X PATCH <url>` - PATCH request
- `curl -X OPTIONS <url>` - OPTIONS request
- `curl -X HEAD <url>` - HEAD request
- `curl -X TRACE <url>` - TRACE request

## Request Headers
- `curl -H "Header: Value" <url>` - Add header
- `curl -A "User-Agent" <url>` - Set user agent
- `curl -e <referer> <url>` - Set referer
- `curl -b "cookie=value" <url>` - Send cookie
- `curl -c cookies.txt <url>` - Store cookies
- `curl -H "Accept: application/json" <url>` - Set Accept header
- `curl -H "Cache-Control: no-cache" <url>` - Cache control
- `curl -H "If-None-Match: \"etag-value\"" <url>` - ETag handling

## Data Transmission
### POST Data
- `curl -d "param=value" <url>` - POST data
- `curl -d @file.json <url>` - POST from file
- `curl -d '{"key":"value"}' -H "Content-Type: application/json" <url>` - POST JSON
- `curl --data-urlencode "param=value with spaces" <url>` - URL-encoded POST
- `curl --data-binary @file.bin <url>` - POST binary data
- `curl --data-raw "raw-data" <url>` - POST raw data

### Form Data
- `curl -F "file=@photo.png" <url>` - Upload file
- `curl -F "field=value" <url>` - Form field
- `curl -F "file=@photo.png;type=image/png" <url>` - Upload with content type
- `curl -F "file=@photo.png;filename=custom.png" <url>` - Custom filename
- `curl -F "files[]=@file1.txt" -F "files[]=@file2.txt" <url>` - Multiple files

## Authentication
- `curl -u username:password <url>` - Basic auth
- `curl -u username <url>` - Prompt for password
- `curl --oauth2-bearer <token> <url>` - OAuth2
- `curl --ntlm -u username:password <url>` - NTLM auth
- `curl --negotiate -u : <url>` - Negotiate auth
- `curl --aws-sigv4 "aws:amz:region:service" <url>` - AWS Signature V4
- `curl --digest -u username:password <url>` - Digest auth

## SSL/Security
- `curl -k <url>` - Allow insecure SSL
- `curl --cacert cert.pem <url>` - Custom CA cert
- `curl --cert client.pem <url>` - Client certificate
- `curl --key key.pem <url>` - Private key
- `curl --ciphers ECDHE-RSA-AES256-GCM-SHA384 <url>` - Specific cipher
- `curl --tls-max 1.2 <url>` - Maximum TLS version
- `curl --ssl-no-revoke <url>` - Skip cert revocation checks
- `curl --ssl-reqd <url>` - Require SSL/TLS
- `curl --pinnedpubkey key.pub <url>` - Public key pinning

## Output Control
- `curl -s <url>` - Silent mode
- `curl -S <url>` - Show errors
- `curl -v <url>` - Verbose output
- `curl --trace dump.txt <url>` - Full trace
- `curl -w "Time: %{time_total}\n" <url>` - Format output
- `curl --trace-ascii debug.txt <url>` - ASCII trace
- `curl --trace-time <url>` - Add timestamps to trace
- `curl -w "@format.txt" <url>` - Format from file
- `curl --write-out "%{json}" <url>` - JSON output format

## Network Options
- `curl --interface eth0 <url>` - Specific interface
- `curl --proxy proxy:port <url>` - Use proxy
- `curl --socks5 proxy:port <url>` - SOCKS5 proxy
- `curl --resolve host:port:ip <url>` - Custom resolution
- `curl --dns-servers 8.8.8.8 <url>` - DNS servers
- `curl --dns-ipv4-addr <ip> <url>` - Force IPv4 DNS
- `curl --dns-ipv6-addr <ip> <url>` - Force IPv6 DNS
- `curl --tcp-fastopen <url>` - Use TCP Fast Open
- `curl --tcp-nodelay <url>` - Disable Nagle's algorithm
- `curl --path-as-is <url>` - Don't squash .. sequences

## Advanced Features
### Ranges
- `curl -r 0-99 <url>` - First 100 bytes
- `curl -r -500 <url>` - Last 500 bytes
- `curl -r 500-999 <url>` - Specific range
- `curl -r 0-99,200-299 <url>` - Multiple ranges

### Multiple URLs
- `curl url1 url2` - Multiple downloads
- `curl url{1..5}.example.com` - URL sequences
- `curl -Z url1 url2` - Parallel downloads
- `curl --parallel url1 url2` - Parallel with options
- `curl --parallel-max 10 url1 url2` - Limit parallel connections

### Rate Limiting
- `curl --limit-rate 1000B <url>` - Limit speed
- `curl --max-time 10 <url>` - Timeout
- `curl --retry 3 <url>` - Retry attempts
- `curl --retry-delay 5 <url>` - Delay between retries
- `curl --retry-max-time 60 <url>` - Maximum retry time
- `curl --connect-timeout 10 <url>` - Connection timeout

## Common Use Cases
### API Testing

#### GET request with auth and JSON response
```
curl -H "Authorization: Bearer token123" \
     -H "Accept: application/json" \
     https://api.example.com/data
```

#### POST JSON data
```
curl -X POST \
     -H "Content-Type: application/json" \
     -d '{"name":"John","age":30}' \
     https://api.example.com/users
```

#### File upload with form data
```
curl -F "file=@document.pdf" \
     -F "description=My File" \
     https://api.example.com/upload
```

#### GraphQL query
```
curl -X POST \
     -H "Content-Type: application/json" \
     -d '{"query": "{ users { id name } }"}' \
     https://api.example.com/graphql
```

#### OAuth2 token request
```
curl -X POST \
     -d "grant_type=client_credentials" \
     -d "client_id=id123" \
     -d "client_secret=secret123" \
     https://auth.example.com/token
```

## Website Testing

### Test response time
curl -w "\nTime: %{time_total}s\n" -o /dev/null -s https://example.com


### Check HTTP/2 support
curl -I --http2 https://example.com


### Test different IP versions
curl -4 https://example.com  # IPv4 only
curl -6 https://example.com  # IPv6 only


### Load testing
```
curl -w "@format.txt" \
     -o /dev/null -s \
     -H "Connection: keep-alive" \
     --keepalive-time 60 \
     https://example.com
```

### Cookie handling
```
curl -b cookies.txt \
     -c cookies.txt \
     -L \
     https://example.com/login
```

## Debugging


### Full verbose output with timing
curl -v -w "\nTime: %{time_total}s\n" https://example.com


### Check redirect chain
curl -L -I https://example.com


### Test specific SSL version
curl --tlsv1.2 https://example.com


### Certificate information
curl -vI --cert-status https://example.com

## DNS debugging
```
curl --dns-servers 8.8.8.8 \
     --dns-ipv4-addr 1.2.3.4 \
     --trace dns.txt \
     https://example.com
```

## Performance Testing


### Download speed test
```
curl -o /dev/null \
     -w "Speed: %{speed_download} bytes/sec\n" \
     https://example.com/largefile
```


### Connection timing details
```
curl -w "\
    namelookup: %{time_namelookup}s\n \
    connect: %{time_connect}s\n \
    appconnect: %{time_appconnect}s\n \
    pretransfer: %{time_pretransfer}s\n \
    starttransfer: %{time_starttransfer}s\n \
    total: %{time_total}s\n" \
    -o /dev/null -s https://example.com
```

### HTTP/2 multiplexing test
```
curl --http2 \
     --parallel \
     --parallel-max 10 \
     -w "HTTP Version: %{http_version}\n" \
     https://example.com/resource{1..10}
```
