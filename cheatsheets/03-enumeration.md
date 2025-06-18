## 🔹 Phase 3 – Enumeration

Enumeration is the bridge between reconnaissance and exploitation. While recon tells you *what* exists, enumeration tells you *how it behaves*, *what it's running*, and *what you can target*. This phase involves active interaction with services, applications, and protocols to extract as much meaningful information as possible.

> 🧠 Think of it as the fingerprinting phase: you're identifying versions, endpoints, parameters, users, directories, and misconfigurations.

---

## 🔍 Service Enumeration

### 🔸 Web Directory and File Bruteforcing

Uncover hidden paths, admin panels, backups, and more.

#### `ffuf`

```bash
ffuf -u https://target.com/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -c -t 50
```

* `-u`: target URL with placeholder `FUZZ`
* `-w`: wordlist path
* `-c`: colorized output
* `-t`: threads

#### `gobuster`

```bash
gobuster dir -u https://target.com -w /usr/share/wordlists/dirb/common.txt -x php,txt,bak -t 40
```

* `-x`: extensions to brute-force (`.php`, `.txt`, `.bak`)

🧠 Use multiple wordlists, test with and without trailing slashes, try common file extensions.

### 🔸 Virtual Host Discovery

Sometimes targets use multiple vhosts on a single IP.

```bash
ffuf -u http://target.com -H "Host: FUZZ.target.com" -w /usr/share/wordlists/subdomains-top1million-110000.txt
```

---

## 🔐 User, Login, and Parameter Enumeration

### 🔸 Login Panels

Look for login forms, comment areas, search bars:

* Manual browsing + Burp Suite Proxy
* Use `whatweb` or `nmap` scripts to find panels

### 🔸 Brute-force and Enumeration

Use `hydra`, `ncrack`, or `medusa` to test known login forms.

#### `hydra` example (web form):

```bash
hydra -l admin -P rockyou.txt target.com http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect"
```

* Replace `/login` and failure message as needed

### 🔸 Parameter Discovery

Find hidden parameters that control logic or access.

* Tools: `Arjun`, `ParamSpider`

#### `arjun` example:

```bash
arjun -u https://target.com/page.php -m GET
```

* Outputs parameters discovered by fuzzing common names

---

## 🔄 Technology and Framework Enumeration

### 🔸 HTTP Headers Inspection

```bash
curl -I https://target.com
```

* Useful for detecting server, framework, security headers (or lack of)

### 🔸 CMS Detection

```bash
wpscan --url https://target.com
```

* Only for WordPress (also detects users, plugins, themes)

```bash
droopescan scan drupal -u https://target.com
```

* Drupal-focused detection

### 🔸 BuiltWith and Wappalyzer (OSINT)

* Use [https://builtwith.com](https://builtwith.com) and browser plugins
* Identify tech stacks: Apache/Nginx, React/Angular, Laravel, etc.

---

## 📌 Tips

* Enumerate **everything**: usernames, directories, params, headers.
* Use `Burp Suite` to capture requests and manually test injection points.
* If login exists, test weak creds first: `admin:admin`, `admin:password`, etc.
* Don’t assume `/robots.txt` is boring — it often hides sensitive paths.
