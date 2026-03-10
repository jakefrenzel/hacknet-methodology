# Nmap

Nmap (Network Mapper) is commonly used in the reconnaissance phase to understand the attack surface of a target.

## ⚡ Port Scan Types
| Flag | Name | How it works |
|------|------|--------------|
| -sn | Ping Scan | Checks if hosts are alive (no port scanning) |
| -sT | TCP Connect Scan | Completes the full 3-way handshake |
| -sS | TCP SYN Scan | Sends SYN, gets SYN-ACK, then sends RST (never completes handshake) |
| -sU | UDP Scan | Sends UDP packets to ports |

## 🔧 Service and Version Detection Modifiers
| Flag | Name | How it works |
|------|------|--------------|
| -sV | Version Detection | Probes open ports to detect software and version |
| -sC | Default Scripts | Runs Nmap's default NSE scripts for extra info |
| -O | OS Detection | Tries to fingerprint the operating system |
| -A | Agressive Scan | Enables `-sV` `-sC` `-O` and traceroute all at once |

### Example Usage

Ping Scan: `nmap -sn 192.168.0.1`

TCP SYN Scan: `nmap -sS 192.168.0.1`

TCP Connect Scan: `nmap -sT 192.168.0.1`

UDP Scan: `nmap -sU 192.168.0.1`
