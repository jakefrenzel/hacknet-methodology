# 🗺️ Nmap

Nmap (Network Mapper) is commonly used in the reconnaissance phase to understand the attack surface of a target.

---

> [!WARNING]
> Only scan systems you own or have explicit written permission to test. Unauthorized scanning is illegal in most jurisdictions.

## 🔍 Host Discovery
| Flag | Name | How it works |
|------|------|--------------|
| `-sn` | Ping Scan | Checks if hosts are alive (no port scanning) |
| `-Pn` | Skip Ping | Assumes host is up (useful when hosts block ICMP) |
| `-PU` | UDP Ping | Uses UDP packets for host discovery |

```bash
sudo nmap -sn 192.168.1.10
```

## ⚡ Port Scan Types
| Flag | Name | How it works |
|------|------|--------------|
| `-sT` | TCP Connect Scan | Completes the full 3-way handshake |
| `-sS` | TCP SYN Scan | Sends SYN, gets SYN-ACK, then sends RST (never completes handshake) |
| `-sU` | UDP Scan | Sends UDP packets to ports |

```bash
sudo nmap -sS 192.168.1.10
```

## 🔧 Service and Version Detection Modifiers
| Flag | Name | How it works |
|------|------|--------------|
| `-sV` | Version Detection | Probes open ports to detect software and version |
| `-sC` | Default Scripts | Runs Nmap's default NSE scripts for extra info |
| `-O` | OS Detection | Tries to fingerprint the operating system |
| `-A` | Aggressive Scan | Enables `-sV` `-sC` `-O` and traceroute all at once |

```bash
sudo nmap -sS -sV 192.168.1.10
```

## 🎯 Port and Target Modifiers 
| Flag | Example | How it works |
|------|---------|--------------|
| `-p` | `-p 22,80,443` | Scan specific ports |
| `-p-` | `-p-` | Scan all 65,535 ports |
| `--top-ports` | `--top-ports 100` | Scan top `N` most common ports |

```bash
sudo nmap -A -p- 192.168.1.10
```

## ⏱️ Timing and Speed Modifiers
| Flag | Level | Description |
|------|-------|-------------|
| `-T0` | Paranoid | Extremely slow (IDS evasion) |
| `-T1` | Sneaky | Slow (IDS evasion) |
| `-T2` | Polite | Slows down to use less bandwidth |
| `-T3` | Normal | Default |
| `-T4` | Aggressive | Faster (good for reliable networks) |
| `-T5` | Insane | Very fast (may miss results) |

```bash
sudo nmap -sS -T4 192.168.1.10
```

## 📤 Output Format Modifiers
| Flag | Description |
|------|-------------|
| `-oN file.txt` | Normal human-readable output |
| `-oX file.txt` | XML output |
| `-oG file.txt` | Grepable output |
| `-oA results` | Save in all formats |
| `-v` | Increase verbosity (prints in real-time) |

```bash
sudo nmap -sT -oN tcp_scan.txt 192.168.1.10
```

## 🧪 Common Combos

Quick host discovery on a subnet:
```bash
nmap -sn 192.168.1.0/24
```

Stealthy SYN scan with version detection on top 1000 ports
```bash
nmap -sS -sV 192.168.1.10
```

Full aggressive scan with OS detection
```bash
nmap -A 192.168.1.10
```

Scan all ports quietly
```bash
nmap -sS -p- -T4 192.168.1.10
```

Save results to all formats
```nmap
nmap -A 192.168.1.10 -oA results
```
