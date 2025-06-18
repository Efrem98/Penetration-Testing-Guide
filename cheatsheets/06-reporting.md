## 🔹 Phase 6 – Reporting

Reporting is where all your technical work becomes **business-relevant insight**. A good report doesn't just say *"we found a vulnerability"* — it explains what it means, how it impacts the organization, and how to fix it. Your report is often the **only part the client reads**, so make it clear, professional, and actionable.

> 🧠 A pentester without a solid report is just a noisy hacker. Reporting is where your work becomes value.

---

## 🧾 Report Structure

### 1. **Executive Summary**

* Non-technical overview
* Focus on business impact
* Top 3–5 critical findings, explained simply

### 2. **Scope and Methodology**

* What was tested, when, and how
* Type of test (black/grey/white box)
* Tools and techniques used

### 3. **Findings**

Each vulnerability should include:

* **Title**: clear and short (e.g., *Unauthenticated SQL Injection on /api/products*)
* **Description**: explain the issue and root cause
* **Risk Rating**: use CVSSv3, OWASP Risk Rating, or custom scale
* **Impact**: business consequences of exploitation
* **Evidence**: screenshots, request/response samples, payloads
* **Remediation**: what to fix, how to fix it, and references

### 4. **Appendices**

* List of tools, versions, wordlists
* IP ranges, tested endpoints, credentials used
* Raw output (optional)

---

## 📊 Risk Rating

Use a consistent model to assess severity.

### 🔸 CVSSv3 (Common Vulnerability Scoring System)

* Base Score from 0.0 to 10.0
* Online calculator: [https://www.first.org/cvss/calculator/3.1](https://www.first.org/cvss/calculator/3.1)

### 🔸 OWASP Risk Rating

Considers:

* Likelihood (easy to exploit? public?)
* Impact (technical & business)

---

## 📋 Reporting Tools & Templates

### Markdown → PDF (with Pandoc)

Keep your report versionable:

```bash
pandoc report.md -o final-report.pdf --toc --pdf-engine=xelatex
```

### GUI Tools

* **Dradis**: collaborative reporting and plugin support
* **Serpico**: markdown-based GUI report builder
* **CherryTree / Obsidian**: structured internal reporting

---

## 🧠 Best Practices

* Prioritize clarity over technical jargon
* Support each finding with solid, repeatable evidence
* Include visuals: screenshots, diagrams, timeline of attack
* Avoid blaming or emotional tone — keep it professional
* Include recommendations that are **realistic** for the client
* Ask for a debrief meeting to walk through the report

---

Your report is your legacy. A well-written report helps the client improve, protects users, and showcases your expertise.
