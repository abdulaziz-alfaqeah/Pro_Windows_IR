# 🛡️ Deep Windows IR Audit v5

<div align="center">

**A professional, read-only forensic triage tool for Windows — built for Incident Response analysts.**

[![PowerShell](https://img.shields.io/badge/PowerShell-5.1%2B-5391FE?style=for-the-badge&logo=powershell&logoColor=white)](https://docs.microsoft.com/en-us/powershell/)
[![Windows](https://img.shields.io/badge/Windows-11%20%7C%2010-0078D6?style=for-the-badge&logo=windows&logoColor=white)](https://www.microsoft.com/windows)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Read-Only](https://img.shields.io/badge/Mode-Read--Only-success?style=for-the-badge&logo=shield&logoColor=white)]()
[![IR](https://img.shields.io/badge/Use--Case-Incident%20Response-red?style=for-the-badge)]()

</div>

---

## 📌 Overview

**Deep Windows IR Audit v5** is a comprehensive PowerShell-based forensic triage script designed for **authorized incident responders and digital forensics analysts**. It performs a deep, non-destructive audit of a Windows system — collecting evidence from persistence mechanisms, running processes, network activity, and more — without modifying a single byte on disk or in the registry.

> **Key Philosophy:** The script deliberately separates **OBSERVATION** from **FINDING**. It does not flag "Auto + LocalSystem + unquoted path" as automatically malicious, avoiding the false-positive epidemic found in many other tools.

---

## ⚠️ Legal Disclaimer

> [!CAUTION]
> This tool is intended **exclusively** for authorized incident response, digital forensics, and security auditing on systems you **own or have explicit written permission** to investigate.
>
> **Unauthorized use against systems you do not own is illegal.** The author assumes no liability for misuse.

---

## ✨ Features

| Category | Details |
|---|---|
| 🔧 **Services & Processes** | Running services, processes, drivers — with Authenticode signatures |
| ⏰ **Scheduled Tasks** | Full scheduled task enumeration with action details |
| 🕸️ **WMI Persistence** | Permanent WMI event subscriptions (a common APT technique) |
| 🔑 **Registry Persistence** | Run/RunOnce, IFEO, Winlogon, AppInit, Startup folders |
| 🌐 **Network** | Active connections, firewall profiles/rules, DNS cache, proxy settings, hosts file |
| 👤 **Users & Groups** | Local accounts, group memberships, recently logged-in users |
| 📦 **Software Inventory** | Installed programs + AppX/MSIX packages |
| 🛡️ **AV State** | Windows Defender & Kaspersky configuration/status |
| 🔍 **Signatures & Hashes** | Authenticode validation + optional SHA-256 of all executables |
| 🔓 **Weak ACLs** | Detection of misconfigured permissions on critical paths |
| 📋 **Event Logs** | Optional export: Security / System / Defender Operational |
| 🎯 **Findings Engine** | Severity-rated findings: `INFO` → `LOW` → `MEDIUM` → `HIGH` → `CRITICAL` |

---

## 🚀 Quick Start

### Prerequisites

- Windows 10 / Windows 11
- PowerShell 5.1 or later
- **Administrator privileges** (required for full access)

### Basic Usage

```powershell
# 1. Open PowerShell as Administrator

# 2. Allow script execution for this session only
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force

# 3. Run the audit (basic)
.\Deep_Windows_IR_Audit_v5.ps1

# 4. Run with event log collection (last 30 days)
.\Deep_Windows_IR_Audit_v5.ps1 -CollectEventLogs -EventDays 30

# 5. Full deep audit (includes SHA-256 hashing of all executables — slower)
.\Deep_Windows_IR_Audit_v5.ps1 -CollectEventLogs -EventDays 30 -DeepHashAllExecutables -OutputRoot "C:\IR_Evidence"
```

### Parameters

| Parameter | Type | Default | Description |
|---|---|---|---|
| `-OutputRoot` | `String` | `C:\Forensic_IR` | Root directory where evidence is saved |
| `-CollectEventLogs` | `Switch` | `false` | Export Security, System & Defender event logs |
| `-EventDays` | `Int` | `14` | Number of past days of event logs to collect |
| `-DeepHashAllExecutables` | `Switch` | `false` | SHA-256 hash every resolvable executable (slower) |

---

## 📁 Output Structure

Each run creates a **timestamped evidence folder**:

```
C:\Forensic_IR\
└── DeepWindowsIR_v5_20260922_010000\
    ├── Audit.log                  ← Real-time execution log
    ├── Findings.csv               ← All flagged findings (severity-rated)
    ├── Errors.csv                 ← Non-fatal collection errors
    └── Raw\
        ├── Services.csv
        ├── Processes.csv
        ├── Drivers.csv
        ├── ScheduledTasks.csv
        ├── WMI_Persistence.csv
        ├── RegistryPersistence.csv
        ├── NetworkConnections.csv
        ├── FirewallRules.csv
        ├── DNS_Cache.csv
        ├── LocalUsers.csv
        ├── InstalledSoftware.csv
        ├── Signatures.csv
        ├── WeakACLs.csv
        ├── EventLogs\             ← (if -CollectEventLogs)
        └── ...
```

---

## 🔬 Findings Severity Scale

| Severity | Color | Meaning |
|---|---|---|
| `CRITICAL` | 🔴 | Definite indicators of compromise or active threat |
| `HIGH` | 🟠 | Strong anomalies requiring immediate investigation |
| `MEDIUM` | 🟡 | Suspicious findings that need analyst review |
| `LOW` | 🔵 | Minor anomalies or policy deviations |
| `INFO` | ⚪ | Neutral observations for baseline documentation |

---

## 🗂️ Repository Structure

```
Pro_Windows_IR/
├── Deep_Windows_IR_Audit_v5.ps1   ← Main forensic audit script
├── execution_command.txt           ← Example run commands
└── README.md                       ← This file
```

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/new-collection-module`
3. Commit your changes: `git commit -m 'feat: add new persistence check'`
4. Push to the branch: `git push origin feature/new-collection-module`
5. Open a Pull Request

---

## 👤 Author

**Abdulaziz Al-Faqeah**  
🔗 [GitHub: @abdulaziz-alfqeah](https://github.com/abdulaziz-alfqeah)

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

<div align="center">
<sub>Built with ❤️ for the Incident Response & DFIR community</sub>
</div>