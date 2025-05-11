---
title: Ethical Design of Forensic Scripts for System Activity Data Collection
author: Fatima Iqbal and Team
layout: default
---

# 🛡️ Ethical Design of Forensic Scripts for System Activity Data Collection

**📍 By Fatima Iqbal, Brian Palencia Sanchez, Simran Kaur, Bryan Fayad Pirbaksh, Saiyad Mohamed Hussain**  
*CYB 625 | Principles of Secure Scripting and Cryptography – St. John's University*

---

## 🔍 Introduction

Forensic scripts are essential tools in cybersecurity, helping organizations track and investigate system activities during audits, incidents, or legal investigations. However, many scripts ignore ethical issues like user consent, data overreach, and insecure storage. 

This blog explores how **transcript-based logging**, **NIST SP 800-53 controls**, and **secure script design** can align forensic scripting with both policy and ethics.

---

## 🎯 Research Goals

- ✅ Design PowerShell & Python scripts with built-in **user consent**, **data minimization**, and **secure log storage**
- 🧪 Evaluate script security using **PSScriptAnalyzer** and **Bandit**
- 🔐 Ensure alignment with **NIST SP 800-53 controls** for audit and accountability
- 📄 Simulate **structured transcript logs** for audit readiness

---

## 🧰 Methodology

### 📝 Script Design (PowerShell + Python)

- PowerShell used `Start-Transcript` to log system commands.
- Python used `logging` and `subprocess.run(['tasklist'])`.
- Logs were stored in a restricted folder: `C:\Logs`.
- Scripts displayed **user consent notices** at startup.

### 📸 Screenshot Example

```powershell
Write-Output "This script collects system activity data for audit purposes."
Start-Transcript -Path C:\Logs\transcript.log
Get-Process | Select-Object -First 5
Stop-Transcript
```

```python
import logging, subprocess
logging.basicConfig(filename="C:/Logs/transcript_python.log", level=logging.INFO)
logging.info("This script collects system activity data for audit purposes.")
logging.info(subprocess.run(["tasklist"], capture_output=True).stdout.decode())
```

---

## 🧪 Static Analysis

- **PowerShell**:
  - `PSScriptAnalyzer` flagged `Write-Host` and unused variables.
- **Python**:
  - `Bandit` flagged use of `subprocess` with partial paths and no input validation.

### 🔍 Vulnerabilities Addressed

- ✅ Switched to `Write-Output`
- ✅ Ensured proper paths in Python
- ✅ Validated script structure before use

---

## 📋 Ethical & Policy Compliance

| Consideration     | Implementation                                          | NIST Control |
|------------------|---------------------------------------------------------|--------------|
| User Consent      | Notification at script start                            | AU-3         |
| Data Minimization | Logged only first 5 processes                           | AU-2         |
| Secure Storage    | Logs saved in `C:\Logs` with restricted permissions    | AU-9         |
| Traceability      | Timestamped logs                                        | AU-12        |

---

## 📂 Simulated Transcript Logs

### 📁 PowerShell Example

```
********** Transcript started **********
This script collects system activity data for audit purposes.
Get-Process | Select-Object -First 5
Timestamp: 2025-05-05 10:00:00
********** Transcript ended **********
```

### 📁 Python Example

```
2025-05-05 10:00:00,123 - INFO - Logging started.
2025-05-05 10:00:00,456 - INFO - Collecting running processes...
2025-05-05 10:00:01,789 - INFO - Output: [‘process1’, ‘process2’, ...]
```

---

## 🌟 Key Takeaways

- 📌 Transcript logging boosts **transparency**, **compliance**, and **accountability**.
- 🧠 Ethical script design reduces legal and privacy risks.
- ⚙️ Static analysis ensures scripts are **secure and reliable**.
- ✅ NIST alignment prepares scripts for **real-world audit scenarios**.

---

## 🚧 Limitations

- Only 2 script types tested (PowerShell & Python)
- No real-world system execution (simulated logs only)
- Focused on NIST SP 800-53; other frameworks (e.g., GDPR) not covered

---

## 🔭 Future Work

- Expand to network, authentication, and file-access logs
- Integrate enterprise logging tools (e.g., Splunk, ELK Stack)
- Perform live testing in real-time environments
- Compare compliance across GDPR, HIPAA, and NIST

---

## ✅ Conclusion

Ethical design in forensic scripting is not optional — it’s essential. By combining **secure practices**, **transparent logging**, and **industry standards**, our project builds a foundation for responsible cybersecurity investigations. This approach supports audit readiness, protects user rights, and ensures legal defensibility.

---

## 📚 References

1. [NIST SP 800-53 (Rev. 4)](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r4.pdf)  
2. [PowerShell Script Analyzer](https://devblogs.microsoft.com/powershell/powershellscript-analyzer-static-code-analysis-for-windows-powershell-scripts-modules/)  
3. [Bandit Python Analyzer](https://bandit.readthedocs.io/en/latest/)  
4. [Digital Guardian Audit Logging Guide](https://digitalguardian.com/blog/audit-logs-best-practices)  
5. [The IIA AI Framework 2024](https://www.theiia.org/en/content/articles/2024/artificial-intelligence-auditing-framework/)  
6. [Snare Solutions Logging Compliance](https://www.snaresolutions.com/)

---

**🖼️ Stay tuned! Screenshots and log visuals will be added soon.**

