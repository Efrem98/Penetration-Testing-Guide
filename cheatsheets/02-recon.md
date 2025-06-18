## 🔹 Phase 2 – Reconnaissance (Recon)

Reconnaissance is the first technical step in any penetration test. It's the phase where you act like a digital detective: gathering intel, understanding your target’s infrastructure, and mapping the potential attack surface. A well-executed recon phase sets the foundation for the rest of the test. Inexperienced attackers rush it — seasoned professionals spend most of their time here.

Recon is divided into:

1. **Passive Recon**: Gathering information without touching the target system directly.
2. **Active Recon**: Controlled interaction with the target to expand knowledge.

---

## 🔍 Passive Reconnaissance

Passive recon relies on publicly available data, third-party services, and OSINT. It's stealthy, legal (in most contexts), and often incredibly revealing.

### 🔸 WHOIS Lookups

WHOIS allows you to retrieve domain registration information.

```bash
whois target.com
```

* Use it to identify the registrant (organization/email), domain age, registrar.
* May reveal internal emails or naming conventions useful for phishing.

### 🔸 DNS Records Enumeration

Query DNS servers for public records:

```bash
dig target.com any
```

This command requests all available records (A, MX, TXT, NS).

Attempt a **Zone Transfer** (often blocked but gold when successful):

```bash
dig AXFR @ns1.target.com target.com
```

* If successful, it dumps every DNS entry (internal and external) for the domain.

### 🔸 Subdomain Enumeration

Subdomains often expose internal tools, staging environments, or forgotten apps.

```bash
subfinder -d target.com
```

```bash
amass enum -passive -d target.com
```

```bash
assetfinder --subs-only target.com
```

* Run all tools and merge results.
* Prioritize subdomains like `dev.`, `staging.`, `admin.`, `beta.`

### 🔸 Certificate Transparency Logs

Certificates expose domains and subdomains.

* Search via browser: [https://crt.sh](https://crt.sh/?q=target.com)
* Or with `crtsh.py` or tools like `certspotter`

### 🔸 Google Dorking

Craft specific queries to discover publicly exposed data:

```text
site:target.com intitle:"index of"
site:target.com ext:sql | ext:log | ext:bkf | ext:env
inurl:/admin/ | inurl:/login/ | inurl:/dashboard/
```

* Use this to identify exposed directories, login panels, backups, Git repos, or leaked credentials.

### 🔸 Shodan and Censys

These services index metadata of internet-facing devices.

* Visit: [https://shodan.io](https://shodan.io) or [https://censys.io](https://censys.io)
* Search for:

```text
ssl:"target.com"
hostname:"target.com"
```

* Identify open ports, banners, service versions, geographic location, IoT/SCADA systems.

---

## 🚀 Active Reconnaissance

Active recon means interacting directly with the target — scanning ports, identifying services, probing technologies. It’s noisier, but it gives actionable data.

### 🔸 Port Scanning with Nmap

Full TCP port scan:

```bash
nmap -sS -T4 -p- target.com
```

* `-sS`: TCP SYN scan (stealthy)
* `-T4`: Aggressive timing for speed
* `-p-`: Scan all 65535 ports

Service detection and script scan:

```bash
nmap -sV -sC target.com -oN nmap-basic.txt
```

* `-sV`: Detect service versions
* `-sC`: Run default scripts (e.g., for SSL certs, HTTP titles)
* `-oN`: Output in normal text format

### 🔸 Fast Scanning with Masscan

When speed is more important than stealth:

```bash
masscan -p1-65535 --rate=10000 target.com
```

* Masscan can scan entire IP ranges quickly
* Tune `--rate` to avoid firewall blocks

### 🔸 Web Technology Detection

```bash
whatweb https://target.com
```

* Identifies server, CMS, analytics, frameworks

Alternative:

```bash
httpx -title -tech-detect -status-code -web-server -ip -cname -url target.com
```

* `httpx` provides a cleaner, more scriptable output

### 🔸 WAF Detection

Check for Web Application Firewalls (helps avoid false positives or bans):

```bash
wafw00f https://target.com
```

* Detects vendors like Cloudflare, AWS WAF, F5, etc.

---

## 📌 Pro Tips

* Document everything — recon is not linear. Keep notes of dead-ends and successful leads.
* Merge results from different tools.
* Avoid overwhelming the target. Keep scans low-intensity unless explicitly allowed.
* Use VPNs or VPS for active scanning. Don’t leak your IP.
