
# 🧠 Phishing Investigation — SOC Analyst Lab

## 📋 Project Overview
This repository documents a **phishing email investigation** performed in a SOC lab environment.  
The goal was to analyze a suspicious email, decode its payloads, extract Indicators of Compromise (IOCs), and correlate findings with threat intelligence platforms.

---
## 🛡️Investigation Workflow

Blue Team Labs Online Challenge: The Planet's Prestige https://blueteamlabs.online/home/challenge/the-planets-prestige-e5beb8e545

### Step 1: Initial Triage
- Preserved the suspicious `.eml` file for forensic integrity.
- Ensured safe handling by isolating the email in a lab environment.

### Step 2: Header Analysis
- Examined `From`, `Return‑Path`, and `Received` fields.
- Checked SPF/DKIM/DMARC results → SPF failed for IP `93.99.104.210`.
- Tools: **MXToolbox**, **AbuseIPDB**.

### Step 3: Body & Content Review
- Extracted and decoded obfuscated URLs (Base64, hex, Punycode).
- Identified ransom‑style note demanding “1 Billion CoCans🧃.”
- Saved suspicious attachments for controlled analysis.

### Step 4: Payload & File Signature Verification
- Detected ZIP archive signature (`UEsDB`).
- Tools: **Hexdump**, **CyberChef**, **VirusTotal**.
- Finding: Archive contained disguised files.

### Step 5: Archive Content Analysis
Unzipped archive revealed:
- Tools: **unzip**, **file**, **ExifTool**.
- Finding: Embedded metadata provided attacker clues.

### Step 6: Metadata Extraction
- `GoodJobMajor.pdf` authored by *Pestero Negeja*.
- `DaughtersCrown.jpg` sanitized (no GPS data).
- Tools: **ExifTool**, **strings**, **binwalk**.

### Step 7: Threat Intelligence Correlation
- IP `64.190.63.222` → **SEDO GmbH**, Germany (104 reports on AbuseIPDB).
- Domain `pashter.com` flagged malicious on VirusTotal (1/91 vendors).
- Tools: **AbuseIPDB**, **VirusTotal**, **WHOIS**.

### Step 8: Log Correlation (SOC Context)
- Queried SIEM for related activity:
  - Outbound traffic to flagged domains.
  - Multiple recipients of the same phishing email.
  - Endpoint traces of attachment execution.
- Tools: **Splunk SPL queries**, **ELK dashboards**.

### Step 9: Impact Assessment
- Determined if users clicked links or opened attachments.
- Checked endpoint logs for execution traces.
---

## 🧾 Indicators of Compromise (IOCs)
| Type       | Indicator        | Source              |
|------------|------------------|---------------------|
| IP Address | 93.99.104.210    | Email Header        |
| IP Address | 64.190.63.222    | AbuseIPDB           |
| Domain     | pashter.com      | VirusTotal          |
| File Hash  | SHA256 (zip)     | Local Analysis      |
| Author     | Pestero Negeja   | PDF Metadata        |

---

## 🧠 Lessons Learned
- SPF/DKIM validation is critical for early phishing detection.  
- Encoded payloads often hide multi‑stage lures.  
- Metadata correlation helps trace attacker infrastructure.  
- Combining **CyberChef**, **Splunk**, and **AbuseIPDB** builds a reproducible SOC workflow.

---

## 🧰 Tools & Environment
| Category   | Tools |
|------------|-------|
| OS         | Kali Linux (VirtualBox) |
| Analysis   | CyberChef, ExifTool, VirusTotal, AbuseIPDB |
| Decoding   | Base64, Hexdump |
| Documentation | Markdown, GitHub README |
| Threat Intel | WHOIS, MXToolbox,  |

---

 
  ![image alt](https://github.com/althafmohammed1818-crypto/Phishing-Investigation-/blob/37af1d52df69ce3a6f2029339f11f355e1cb5fbd/Screenshot%202026-05-09%20114021.png)
  ![image alt](https://github.com/althafmohammed1818-crypto/Phishing-Investigation-/blob/37af1d52df69ce3a6f2029339f11f355e1cb5fbd/Screenshot%202026-05-10%20110347.png)
  ![image alt](https://github.com/althafmohammed1818-crypto/Phishing-Investigation-/blob/37af1d52df69ce3a6f2029339f11f355e1cb5fbd/Screenshot%202026-05-10%20112339.png)
  ![image alt](https://github.com/althafmohammed1818-crypto/Phishing-Investigation-/blob/37af1d52df69ce3a6f2029339f11f355e1cb5fbd/Screenshot%202026-05-10%20112510.png)
  ![image alt](https://github.com/althafmohammed1818-crypto/Phishing-Investigation-/blob/37af1d52df69ce3a6f2029339f11f355e1cb5fbd/Screenshot%202026-05-10%20113331.png)
  ![image alt](https://github.com/althafmohammed1818-crypto/Phishing-Investigation-/blob/37af1d52df69ce3a6f2029339f11f355e1cb5fbd/Screenshot%202026-05-10%20114739.png)
  ![image alt](https://github.com/althafmohammed1818-crypto/Phishing-Investigation-/blob/37af1d52df69ce3a6f2029339f11f355e1cb5fbd/Screenshot%202026-05-10%20115021.png)
  ![image alt](https://github.com/althafmohammed1818-crypto/Phishing-Investigation-/blob/37af1d52df69ce3a6f2029339f11f355e1cb5fbd/Screenshot%202026-05-12%20004903.png)
  ![image alt](https://github.com/althafmohammed1818-crypto/Phishing-Investigation-/blob/37af1d52df69ce3a6f2029339f11f355e1cb5fbd/Screenshot%202026-05-12%20004941.png)
  ![image alt](htps://github.com/althafmohammed1818-crypto/Phishing-Investigation-/blob/37af1d52df69ce3a6f2029339f11f355e1cb5fbd/Screenshot%202026-05-12%20005104.png)
  ![image alt](ttps://github.com/althafmohammed1818-crypto/Phishing-Investigation-/blob/37af1d52df69ce3a6f2029339f11f355e1cb5fbd/Screenshot%202026-05-12%20005129.png)



