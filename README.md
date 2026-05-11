# Phishing-Investigation-
This repository documents a complete phishing email investigation performed in a controlled SOC lab environment. It showcases a reproducible workflow for analyzing suspicious emails, decoding payloads, extracting Indicators of Compromise (IOCs), and correlating findings with threat intelligence platforms.

# 🧠 Phishing Investigation — SOC Analyst Lab

## 📋 Project Overview
This repository documents a **phishing email investigation** performed in a SOC lab environment.  
The goal was to analyze a suspicious email, decode its payloads, extract Indicators of Compromise (IOCs), and correlate findings with threat intelligence platforms.

---

## 🧩 Investigation Workflow

### 1️⃣ Email Header Analysis
- **SPF Authentication:** Failed for IP `93.99.104.210` → spoofed sender detected.  
- **SPF Record Validation:** Domain published valid SPF syntax but failed authentication.  
- **Tools Used:** MXToolbox, Email Header Analyzer.  
- **Finding:** Sender domain impersonation confirmed.

### 2️⃣ Payload Decoding
- Extracted Base64‑encoded message using **CyberChef**.  
- Decoded output revealed ransom‑style demand: *“1 Billion CoCans🧃 in cash💰.”*  
- Message referenced an attached puzzle ZIP file.

### 3️⃣ File Signature Verification
- Hex signature `55 45 73 44 42` → ASCII `UEsDB` → ZIP archive.  
- **Tools Used:** Hexdump, VirusTotal, Wikipedia file signature reference.  
- **Finding:** Attachment contained compressed files disguised as legitimate documents.

### 4️⃣ Archive Content Analysis
Unzipped `attachment.zip` revealed:

- **Tools Used:** unzip, file, ExifTool.  
- **Finding:** Files contained embedded metadata and clues pointing to attacker identity.

### 5️⃣ Metadata Extraction
- `GoodJobMajor.pdf` authored by *Pestero Negeja*, produced with *Skia/PDF m90*.  
- `DaughtersCrown.jpg` contained no GPS data, confirming metadata sanitization.  
- **Tools Used:** ExifTool, strings, binwalk.  
- **Finding:** Metadata timestamps aligned with phishing campaign timeline.

### 6️⃣ Threat Intelligence Correlation
- IP `64.190.63.222` → **SEDO GmbH**, Germany — reported 104 times on AbuseIPDB.  
- Domain `pashter.com` flagged **malicious** on VirusTotal (1/91 vendors).  
- **Tools Used:** AbuseIPDB, VirusTotal, WHOIS lookup.  
- **Finding:** Infrastructure hosted on data‑center transit network; likely attacker C2 domain.

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
| Threat Intel | WHOIS, MXToolbox, Splunk |

---

## 📸 Evidence Screenshots
*(Add screenshots in `/evidence` folder)*  
- SPF failure report  
- CyberChef decoding output  
- ZIP file signature verification  
- ExifTool metadata extraction  
- VirusTotal and AbuseIPDB results  

---

## 📂 Repository Structure

