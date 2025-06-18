## 🔹 Resources and References

This section contains the essential wordlists, tools, learning platforms, blogs, and public repositories that every penetration tester should know. It’s not just a collection of links — it’s your **arsenal**. These are curated and categorized for clarity.

---

## 📚 Wordlists

Wordlists are essential for fuzzing, brute-force, and enumeration. Always start with a solid base and customize over time.

### 🔸 SecLists (Ultimate Collection)

* GitHub: [https://github.com/danielmiessler/SecLists](https://github.com/danielmiessler/SecLists)
* Includes:

  * Directory and file names
  * Usernames and passwords
  * API routes
  * Payloads for XSS, LFI, SQLi, etc.

### 🔸 RockYou.txt (Password Bruteforce)

* Path: `/usr/share/wordlists/rockyou.txt`
* Use with: `hydra`, `john`, `hashcat`

### 🔸 Fuzzing lists

* `raft-small-words.txt`, `common.txt`, `big.txt`, `quickhits.txt`
* Located in `SecLists/Discovery/Web-Content/`

---

## 🛠️ Core Tools (CLI & GUI)

These are foundational tools used in real-world penetration testing.

### 🔸 Recon & Enumeration

| Tool        | Purpose                             |
| ----------- | ----------------------------------- |
| `nmap`      | Port scanning and service detection |
| `amass`     | Subdomain enumeration               |
| `subfinder` | Passive subdomain recon             |
| `whatweb`   | Technology fingerprinting           |
| `ffuf`      | Directory fuzzing                   |
| `gobuster`  | Directory & DNS brute-force         |
| `httpx`     | Mass web probe and status scan      |

### 🔸 Vulnerability Scanners & Exploitation

| Tool         | Purpose                               |
| ------------ | ------------------------------------- |
| `sqlmap`     | SQL Injection testing                 |
| `xsstrike`   | Advanced XSS fuzzing                  |
| `nuclei`     | Vulnerability templates (CVE scanner) |
| `Metasploit` | Exploitation framework                |
| `Burp Suite` | Web application proxy and scanner     |
| `wafw00f`    | WAF detection                         |

### 🔸 Post-Exploitation & Privilege Escalation

| Tool          | Platform | Purpose                  |
| ------------- | -------- | ------------------------ |
| `linpeas`     | Linux    | Privilege escalation     |
| `winpeas`     | Windows  | Privilege escalation     |
| `proxychains` | Linux    | Tunnel traffic via SOCKS |
| `chisel`      | Cross    | Port forwarding/pivoting |

---
