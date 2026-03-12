# 🕵️ Recon

> [!NOTE]
> This guide uses the easy difficulty subnet (192.168.147.0/24).

## 📋 Prerequisites
Before starting, it is recommended to review the following:
- [Nmap Guide](nmap.md) — covers scan types, modifiers, and output formats

---

## ⚙️ Setup
Create a folder structure to keep results organized across all subnets.
```bash
mkdir -p nmap/{easy,medium,hard,advanced}
```

This will create the following structure:
<pre><code>nmap/
├── easy/
│   ├── hosts.txt
│   ├── live_hosts.txt
│   └── port_scan.nmap / .xml / .gnmap
├── medium/
├── hard/
└── advanced/
</code></pre>

<details>
  <summary>View a detailed breakdown of the command</summary>
  <br>
  <ul><code>mkdir -p</code> create directories and any missing parent folders</ul>
  <ul><code>results/</code> root folder for all scan output</ul>
  <ul><code>{easy,medium,hard,advanced}</code> creates all four subnet folders at once</ul>
</details>

---

## 🔍 Identify Live Hosts
Before scanning ports, figure out which hosts are alive on the network.
```bash
nmap -sn 192.168.147.0/24 -oG hosts.txt
```
<details>
  <summary>View a detailed breakdown of the scan</summary>
  <br>
  
  <ul><code>-sn</code> ping scan for host discovery</ul>
  <ul><code>192.168.147.0/24</code> scan the entire subnet</ul>
  <ul><code>-oG</code> results save in grepable format</ul>
  <ul><code>hosts.txt</code> save results here</ul>
</details>

---

## 🗂️ Extract Live Hosts
Extract the live IPs using grep
```bash
grep "Up" hosts.txt | awk '{print $2}' > live_hosts.txt
```
<details>
  <summary>View a detailed breakdown of the command</summary>
  <br>

  <ul><code>grep "Up"</code> filter only hosts marked as up</ul>
  <ul><code>hosts.txt</code> the file to search through</ul>
  <ul><code>awk '{print $2}'</code> extract just the IP address column</ul>
  <ul><code>live_hosts.txt</code> save the IP list here</ul>
</details>

---

## ⚡ Port Scan Live Hosts
Run a quick stealth (SYN) scan to find open ports.
```bash
sudo nmap -sS --top-ports 1000 -iL live_hosts.txt -oA port_scan
```
<details>
  <summary>View a detailed breakdown of the scan</summary>
  <br>

  <ul><code>-sS</code> stealth SYN scan</ul>
  <ul><code>--top-ports 1000</code> scan the 1000 most common ports</ul>
  <ul><code>-iL</code> read targets from a file</ul>
  <ul><code>live_hosts.txt</code> the file containing live hosts</ul>
  <ul><code>-oA</code> save results in all formats</ul>
  <ul><code>port_scan</code> name for output files</ul>
</details>

---
