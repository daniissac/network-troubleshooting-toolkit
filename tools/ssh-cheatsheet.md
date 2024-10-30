# SSH Command and Configuration Cheatsheet

## Basic Connection Commands
- `ssh user@hostname` - Basic connection
- `ssh -p 2222 user@hostname` - Connect to specific port
- `ssh -v user@hostname` - Verbose output
- `ssh -vv user@hostname` - More verbose
- `ssh -vvv user@hostname` - Maximum verbosity

## Key Management
- `ssh-keygen -t rsa -b 4096` - Generate RSA key pair
- `ssh-keygen -t ed25519` - Generate Ed25519 key (modern)
- `ssh-copy-id user@hostname` - Copy public key to server
- `ssh-add ~/.ssh/id_rsa` - Add key to SSH agent
- `ssh-add -l` - List loaded keys

## Port Forwarding

### Local Port Forwarding
- `ssh -L 8080:localhost:80 user@hostname` - Forward local port to remote
- `ssh -L 3306:remote_db:3306 user@hostname` - Database port forwarding
- `ssh -L *:8080:localhost:80 user@hostname` - Allow external connections

### Remote Port Forwarding
- `ssh -R 8080:localhost:80 user@hostname` - Forward remote port to local
- `ssh -R 52698:localhost:52698 user@hostname` - Remote pair programming

### Dynamic Port Forwarding (SOCKS Proxy)
- `ssh -D 9090 user@hostname` - Create SOCKS proxy
- `ssh -D 0.0.0.0:9090 user@hostname` - SOCKS proxy (all interfaces)

## SSH Config File
Example configuration in `~/.ssh/config`:

# Default settings for all hosts
Host *
    ServerAliveInterval 60
    ServerAliveCountMax 3
    HashKnownHosts yes
    AddKeysToAgent yes

# Specific host configuration
Host dev
    HostName dev.example.com
    User developer
    Port 2222
    IdentityFile ~/.ssh/dev_rsa

# Jump host configuration
Host prod
    HostName prod.internal
    User admin
    ProxyJump jumphost.example.com

# Shortcut for tunneling
Host tunnel
    HostName remote.example.com
    LocalForward 3306 db.internal:3306
    LocalForward 6379 redis.internal:6379


## Security Options
- `ssh -o PubkeyAuthentication=no user@hostname` - Disable public key authentication
- `ssh -o PreferredAuthentications=password user@hostname` - Force password authentication
- `ssh -o StrictHostKeyChecking=no user@hostname` - Disable host key checking
- `ssh -o UserKnownHostsFile=/dev/null user@hostname` - Don't save host key

## SCP Commands (Secure Copy)
- `scp file.txt user@hostname:/path` - Upload file
- `scp user@hostname:/path/file.txt .` - Download file
- `scp -r directory user@hostname:/path` - Upload directory
- `scp -P 2222 file.txt user@hostname:/path` - Specific port

## SFTP Commands
- `sftp user@hostname` - Start SFTP session
- `get file.txt` - Download file
- `put file.txt` - Upload file
- `ls` - List files
- `pwd` - Print working directory
- `cd directory` - Change directory

## Advanced Usage

### Jump Hosts
- `ssh -J jump.host user@destination` - Using jump host
- `ssh -J user1@jump1,user2@jump2 user@destination` - Multiple jumps

### X11 Forwarding
- `ssh -X user@hostname` - Enable X11 forwarding
- `ssh -Y user@hostname` - Trusted X11 forwarding

### Multiplexing
Add to SSH config file:

Host *
    ControlMaster auto
    ControlPath ~/.ssh/control:%h:%p:%r
    ControlPersist 1h


## Debugging Tips

### Connection Issues
- `ssh -v user@hostname` - Verbose connection debugging

### Check SSH Service
- `systemctl status sshd` - Check SSH daemon status