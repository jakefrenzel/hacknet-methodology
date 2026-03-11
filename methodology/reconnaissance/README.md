# 🔎 Recon

> [!NOTE]
> This guide uses the easy difficulty subnet (192.168.147.0/24).

## Identify Live Hosts
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


## Extract Live Hosts
Extract the live IPs using grep
```bash
grep "Up" hosts.txt | awk '{print $2}' > live_hosts.txt
```

## Port Scan Live Hosts
Run a quick stealth (SYN) scan to find open ports.
```bash
sudo nmap -sS --top-ports 1000 -iL live_hosts.txt
```
