# MCP-Kali-Orchestration

An MCP (Model Context Protocol) server that orchestrates Kali Linux instances on-demand and exposes 50+ security tools to Claude Code or other MCP clients.

## Features

- **On-demand Kali instances** - Spin up/down Docker containers or Proxmox VMs
- **50+ security tools** - Reconnaissance, web testing, exploitation, password attacks, post-exploitation, network tools
- **User-controlled lifecycle** - Explicit `kali_start`/`kali_stop` commands
- **Flexible backend** - Docker (default) or Proxmox VMs

## Quick Start

### 1. Build the Kali Docker image

```bash
npm run build:image
```

This creates the `mcp-kali:latest` Docker image with all security tools pre-installed.

### 2. Install dependencies and build

```bash
npm install
npm run build
```

### 3. Configure (optional)

Copy `.env.example` to `.env` and adjust settings:

```bash
cp .env.example .env
```

### 4. Add to Claude Code

Add to your Claude Code MCP configuration:

```json
{
  "mcpServers": {
    "mcp-kali-orchestration": {
      "command": "node",
      "args": ["/path/to/mcp-kali-orchestration/dist/index.js"]
    }
  }
}
```

## Available Tools

### Lifecycle Management

| Tool | Description |
|------|-------------|
| `kali_start` | Spin up a new Kali instance |
| `kali_stop` | Stop and remove an instance |
| `kali_list` | List all running instances |
| `kali_exec` | Execute arbitrary command |
| `kali_upload` | Upload file to instance |
| `kali_download` | Download file from instance |

### Reconnaissance

| Tool | Description |
|------|-------------|
| `nmap_scan` | Port scanning |
| `nmap_vuln_scan` | Vulnerability scanning |
| `masscan_scan` | High-speed port scanner |
| `whois_lookup` | Domain WHOIS |
| `dig_lookup` | DNS queries |
| `dnsrecon_scan` | DNS enumeration |
| `theharvester_search` | Email/subdomain harvesting |
| `amass_enum` | Subdomain enumeration |
| `sublist3r_scan` | Subdomain enumeration |

### Web Application Testing

| Tool | Description |
|------|-------------|
| `nikto_scan` | Web server scanner |
| `dirb_scan` | Directory brute-forcing |
| `gobuster_dir` | Directory enumeration |
| `gobuster_dns` | DNS brute-forcing |
| `ffuf_fuzz` | Fast web fuzzer |
| `sqlmap_scan` | SQL injection |
| `wpscan_scan` | WordPress scanner |
| `whatweb_scan` | Technology fingerprinting |
| `wafw00f_detect` | WAF detection |
| `nuclei_scan` | Template-based scanner |
| `xsser_scan` | XSS scanner |
| `commix_scan` | Command injection |

### Exploitation

| Tool | Description |
|------|-------------|
| `metasploit_search` | Search for exploits |
| `metasploit_run` | Run Metasploit module |
| `searchsploit_search` | Search Exploit-DB |
| `msfvenom_generate` | Generate payloads |

### Password Attacks

| Tool | Description |
|------|-------------|
| `hydra_attack` | Online password cracking |
| `medusa_attack` | Parallel password cracker |
| `john_crack` | Offline hash cracking |
| `hashcat_crack` | GPU hash cracking |
| `hash_identifier` | Identify hash type |
| `cewl_generate` | Custom wordlist from website |
| `crunch_generate` | Pattern-based wordlist |

### Post-Exploitation

| Tool | Description |
|------|-------------|
| `impacket_secretsdump` | Dump Windows secrets |
| `impacket_psexec` | Remote execution via SMB |
| `impacket_smbexec` | SMB-based execution |
| `impacket_wmiexec` | WMI-based execution |
| `evil_winrm` | WinRM shell |
| `crackmapexec_run` | Network protocol attacks |
| `bloodhound_collect` | AD enumeration |

### Network

| Tool | Description |
|------|-------------|
| `netcat_connect` | Network utility |
| `tcpdump_capture` | Packet capture |
| `wireshark_cli` | tshark analysis |
| `responder_run` | LLMNR/NBT-NS poisoner |
| `bettercap_run` | Network attacks |
| `socat_relay` | Network relay |
| `aircrack_crack` | WPA/WPA2 cracking |

## Usage Example

```
Human: Start a Kali instance and scan example.com

Claude: I'll start a Kali instance and run a scan.

[Uses kali_start]
Instance started: kali-1704825600, IP: 172.17.0.2

[Uses nmap_scan with target=example.com]
Starting Nmap scan...
PORT     STATE  SERVICE
80/tcp   open   http
443/tcp  open   https
...
```

## Configuration

Environment variables (in `.env` or environment):

```bash
# Backend: "docker" or "proxmox"
KALI_BACKEND=docker

# Docker settings
DOCKER_SOCKET=/var/run/docker.sock
KALI_IMAGE=mcp-kali:latest

# Proxmox settings (when using proxmox backend)
PROXMOX_HOST=192.168.1.100
PROXMOX_PORT=8006
PROXMOX_API_TOKEN_ID=root@pam!mcp-kali
PROXMOX_API_TOKEN_SECRET=xxxx
PROXMOX_SSH_USER=root
PROXMOX_SSH_KEY_PATH=~/.ssh/id_rsa
PROXMOX_KALI_TEMPLATE=local:vztmpl/kali-template
PROXMOX_TARGET_NODE=pve

# Execution timeouts
DEFAULT_TIMEOUT_MS=120000
LONG_RUNNING_TIMEOUT_MS=1800000
```

## Security Notice

This tool is intended for:
- Authorized penetration testing engagements
- CTF competitions
- Security research in lab environments
- Educational purposes

**Always ensure you have proper authorization before using these tools against any target.**

## License

MIT
