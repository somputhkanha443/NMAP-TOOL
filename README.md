
# NMAP Basic Lesson (Network Mapper Guide)

> **⚠️ Legal Notice:** Please use NMAP only on networks or hosts for which you have explicit permission! Unauthorized scanning is illegal in many countries [cite: 10]. *For Educational Purposes Only [cite: 10].*

---

1. What is NMAP?
NMAP (Network Mapper) is a famous open-source tool used for network discovery, security auditing, and finding hosts, ports, services, operating systems, and other information on a network[cite: 10].

Official Website / Tool Link: Nmap:[Nmap](https://nmap.org/)).

### Main Use Cases:
* Discover active hosts on a network [cite: 10].
* Find open/closed ports [cite: 10].
* Identify services and software versions [cite: 10].
* Detect Operating Systems [cite: 10].
* Perform penetration testing and security auditing [cite: 10].

---


## 2. Basic Commands

| Command | Usage | Explanation |
| :--- | :--- | :--- |
| `nmap 192.168.1.1` | Scan host | Scan a specific IP address or domain name [cite: 10] |
| `nmap 192.168.1.0/24` | Scan subnet | Scan all hosts in a /24 subnet [cite: 10] |
| `nmap 192.168.1.1-50` | Scan IP range | Scan IP range from .1 to .50 [cite: 10] |
| `nmap -iL hosts.txt` | Scan from file | Scan IPs listed in a text file [cite: 10] |

---

## 3. Scan Types

* **SYN Scan (Stealth Scan) (`-sS`):** 
  * The best and most popular scan type [cite: 10]. Sends a SYN packet and resets the connection immediately without completing the 3-way handshake [cite: 10].
  * Fast and efficient [cite: 10]; requires root/admin privilege [cite: 10]; leaves fewer logs than standard TCP scans [cite: 10].
* **TCP Connect Scan (`-sT`):** 
  * Performs a full 3-way TCP handshake [cite: 10]. Does not require root privilege [cite: 10], but is easier to detect [cite: 10].
* **UDP Scan (`-sU`):** 
  * Scans UDP ports like DNS (53), DHCP (67/68), and SNMP (161) [cite: 10]. Very slow because UDP lacks an acknowledgment mechanism [cite: 10]. *(Tip: Use `--top-ports 100` to speed it up [cite: 10]).*
* **Ping Scan / Host Discovery (`-sn`):** 
  * Checks which hosts are online without scanning ports [cite: 10]. Great for initial network mapping [cite: 10].

---

## 4. Port Selection

| Command | Usage | Explanation |
| :--- | :--- | :--- |
| `nmap -p 80,443,22 target` | Specific ports | Scan specific ports [cite: 10] |
| `nmap -p 1-1000 target` | Port range | Scan ports 1 to 1000 [cite: 10] |
| `nmap -p- target` | All ports | Scan all 65,535 ports [cite: 10] |
| `nmap --top-ports 100 target` | Top ports | Scan top 100 common ports [cite: 10] |
| `nmap --top-ports 1000 target` | Top 1000 | Scan top 1000 common ports [cite: 10] |

---

## 5. Service & OS Detection

* **Version Detection (`-sV`):** Identifies service versions (e.g., OpenSSH 8.9, nginx 1.18, MySQL 8.0) to spot vulnerable versions [cite: 10].
* **Default Script Scan (`-sC`):** Runs default NSE scripts to gather extra info like SSH host keys, HTTP titles, and SSL certificates [cite: 10].
* **OS Detection (`-O`):** Detects operating systems (Linux, Windows, BSD) via TCP/IP fingerprinting (requires root/admin) [cite: 10].
* **Aggressive Scan (`-A`):** Combines `-sV`, `-sC`, `-O`, and `--traceroute` [cite: 10]. *Note: Very noisy and easily detected by IDS/IPS [cite: 10].*

---

## 6. Timing Templates

Nmap provides 6 timing templates (`-T0` to `-T5`) to balance speed and stealth [cite: 10]:

| Command | Usage | Explanation |
| :--- | :--- | :--- |
| `-T0` (Paranoid) | Slowest | 5 min delay between probes; highest stealth [cite: 10] |
| `-T1` (Sneaky) | Very slow | 15 sec delay; good for evading IDS [cite: 10] |
| `-T2` (Polite) | Slow | 0.4 sec delay; uses less bandwidth [cite: 10] |
| `-T3` (Normal) | Default | Balanced default speed [cite: 10] |
| `-T4` (Aggressive) | Fast | Recommended for fast networks [cite: 10] |
| `-T5` (Insane) | Fastest | Extremely fast; may drop packets [cite: 10] |

---

## 7. Output Formats

| Command | Usage | Explanation |
| :--- | :--- | :--- |
| `nmap -oN result.txt target` | Normal text | Save human-readable text format [cite: 10] |
| `nmap -oX result.xml target` | XML | Great for other tools like Metasploit [cite: 10] |
| `nmap -oG result.gnmap target` | Grepable | Good for grep commands [cite: 10] |
| `nmap -oA results target` | All formats | Save in all 3 primary formats at once [cite: 10] |
| `nmap -v target` / `-vv` | Verbose | Show detailed output [cite: 10] |

---

## 8. Common Command Combos

* **Quick Recon:** `nmap -sV --top-ports 1000 -T4 target` (Fast initial enumeration) [cite: 10]
* **Full Detail Scan:** `sudo nmap -sS -sV -sC -O -T4 -oA full_scan target` (Comprehensive combo scan) [cite: 10]
* **Network Discovery:** `nmap -sn 192.168.1.0/24 -oN hosts.txt` (Find all online hosts in subnet) [cite: 10]
* **Stealth Scan:** `sudo nmap -sS -T1 --top-ports 1000 target` (Quiet SYN scan with slow timing) [cite: 10]
* **UDP + TCP Combo:** `sudo nmap -sS -sU -p T:22,80,443,U:53,161 target` [cite: 10]

---

## 9. Basic NSE Scripts

* `--script=banner`: Grab service banner [cite: 10]
* `--script=http-title`: Find webpage title [cite: 10]
* `--script=ssl-cert`: View SSL certificate information [cite: 10]
* `--script=vuln`: Scan for known vulnerabilities [cite: 10]
* `--script=smb-vuln-*`: Check for SMB vulnerabilities [cite: 10]

---

## 10. Quick Cheat Sheet

| Command | Usage | Explanation |
| :--- | :--- | :--- |
| `nmap target` | Basic scan | Scan 1000 common ports [cite: 10] |
| `nmap -sS target` | Stealth SYN | Stealth scan (requires root) [cite: 10] |
| `nmap -sV target` | Version | Detect service versions [cite: 10] |
| `nmap -sC target` | Scripts | Run default scripts [cite: 10] |
| `nmap -O target` | OS detect | Detect operating system [cite: 10] |
| `nmap -A target` | Aggressive | Full combo scan [cite: 10] |
| `nmap -p- target` | All ports | Scan all 65535 ports [cite: 10] |
| `nmap -T4 target` | Fast | Aggressive timing template [cite: 10] |
| `nmap -sn target` | Ping scan | Host discovery only [cite: 10] |
| `nmap -oA target` | Save all | Save 3 output formats [cite: 10] |
