# 🔎 Recon

## Nmap

Nmap (Network Mapper) is commonly used in the reconnaissance phase to understand the attack surface of a target.

# Scan Types
| Flag | Name | How it works |
|------|------|--------------|
| -sn | Ping Scan | Checks if hosts are alive (no port scanning) |
| -sT | TCP Connect Scan | Completes the full 3-way handshake |
| -sS | TCP SYN Scan | Sends SYN, gets SYN-ACK, then sends RST (never completes handshake) |

### Example Usage

Ping Scan: `nmap -sn 192.168.0.1`

TCP SYN Scan: `nmap -sS 192.168.0.1`

TCP Connect Scan: `nmap -sT 192.168.0.1`

UDP Scan: `nmap -sU 192.168.0.1`
