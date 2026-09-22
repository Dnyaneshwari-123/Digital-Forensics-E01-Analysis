# 🔍 Digital Forensic Analysis – Windows XP Disk Image

A digital forensic investigation of a **Windows XP Professional SP3 forensic disk image** using Autopsy, Registry Explorer, Windows Event Viewer, and FTK Imager.

The investigation focuses on reconstructing system activity, analyzing registry artifacts, reviewing event logs, recovering deleted files, examining browser activity, and building a timeline to investigate a possible data-theft or exfiltration scenario.

---

## 📌 Case Overview

| Field                   | Details                          |
| ----------------------- | -------------------------------- |
| **Case Reference**      | `jo-2009-11-12.E01`              |
| **Evidence Type**       | E01 forensic disk image          |
| **Operating System**    | Windows XP Professional SP3      |
| **Main Evidence**       | `jo-2009-11-12.E01`              |
| **Associated Evidence** | Two USB E01 images               |
| **Primary Tool**        | Autopsy 4.22.1                   |
| **Registry Tool**       | Registry Explorer v2026.5.0      |
| **Other Tools**         | FTK Imager, Windows Event Viewer |
| **Analysis Date**       | 20–21 July 2026                  |
| **Analyst**             | Dnyaneshwari Kale                |

The main image contains a Windows XP SP3 system, while two additional E01 images represent associated USB evidence.

---

# 💾 Evidence Images

The investigation contains three forensic evidence images:

```text
jo-2009-11-12.E01
jo-favorites-usb-2009-12-11.E01
jo-work-usb-2009-12-11.E01
```

### Main Workstation

```text
jo-2009-11-12.E01
```

This is the primary Windows XP workstation image.

### USB Evidence

```text
jo-favorites-usb-2009-12-11.E01
jo-work-usb-2009-12-11.E01
```

These two images are associated USB evidence and are important for determining whether files may have been copied from the workstation to removable media.

> ⚠️ The original E01 evidence images are **not included in this repository**. They are referenced for documentation and analysis purposes only.

---

# 🎯 Investigation Objectives

The main objectives were to:

* Verify the integrity of the forensic evidence.
* Identify the operating system and system configuration.
* Analyze Windows Registry hives.
* Identify local user accounts.
* Investigate USB device history.
* Examine recently accessed files and paths.
* Analyze Windows Event Logs.
* Recover deleted or carved files.
* Investigate browser history and downloads.
* Examine cookies and web artifacts.
* Build a forensic timeline.
* Investigate indicators related to possible data theft or exfiltration.

These objectives follow the six forensic exercises documented in the investigation report.

---

# 🛠️ Tools Used

### Autopsy 4.22.1

Used as the primary forensic examination platform for:

* E01 image analysis
* File-system examination
* Hash verification
* Data artifacts
* Deleted-file recovery
* Browser artifacts
* Timeline analysis
* File carving

### FTK Imager

Used for forensic image handling and evidence integrity verification.

### Registry Explorer

Used to examine Windows Registry hives such as:

```text
SYSTEM
SOFTWARE
SAM
NTUSER.DAT
```

### Windows Event Viewer

Used to examine:

```text
Security
System
Application
```

event logs.

---

# 1️⃣ Exercise 1 – Forensic Imaging & Integrity Verification

The main E01 image was loaded into Autopsy as a new data source.

The investigation used forensic integrity verification through hashes.

### Evidence Hashes

| Evidence                          | MD5                                | SHA-1                                      |
| --------------------------------- | ---------------------------------- | ------------------------------------------ |
| `jo-2009-11-12.E01`               | `d328bf1ddeb154b5e23d2f680bb03e45` | `e333fbaa0fe14733f96b88872f87225a71dc6eed` |
| `jo-favorites-usb-2009-12-11.E01` | `ad1d03cbdb8d81e918899479360f50dc` | `7da02a13f0effab5fdb02fe82d3596cc3a10aa2f` |
| `jo-work-usb-2009-12-11.E01`      | `8f23279deb398c3245829a98bc8fc1bd` | `9a2933b2391e5994745710ab317c702b82a9b141` |

The report records the issued hashes for all three evidence items.

---

# 2️⃣ Exercise 2 – Windows Registry Analysis

The following registry hives were examined:

```text
SYSTEM
SOFTWARE
SAM
NTUSER.DAT
```

The investigation identified the system as:

```text
Microsoft Windows XP
Service Pack 3
Build 2600
```

The system was registered to:

```text
MS7.biz
```

The report also examined the computer name and shutdown information stored within the Registry.

---

## 👤 User Accounts

The SAM hive identified four local accounts:

```text
Administrator
Guest
HelpAssistant
SUPPORT_388945a0
```

These were documented as standard built-in or vendor/support accounts, with no unexpected additional account identified during this part of the examination.

---

## 🔌 USB Analysis

USB-related Registry artifacts were examined, particularly:

```text
SYSTEM\ControlSet001\Enum\USB
SYSTEM\ControlSet001\Enum\USBSTOR
```

The general USB enumeration showed four root-hub entries and one genuine peripheral:

```text
Logitech Optical Wheel Mouse
VID_046D&PID_C016
```

The report identifies the USBSTOR records as the key evidence needed to determine whether the two supplied USB evidence images had previously been connected to the workstation.

---

# 3️⃣ Exercise 3 – Windows Event Log Analysis

The investigation examined:

```text
Security
System
Application
```

Important Windows event IDs considered included:

```text
4624  → Successful logon
4625  → Failed logon
4720  → Account creation
4726  → Account deletion
4732  → Privileged group membership change
6006  → Event Log service stopped
6009  → System startup information
```

For the XP-era logs, equivalent older event IDs were also considered.

---

## 🕐 System Shutdown

One important System log event was:

```text
Event ID: 6006
Date: 13 November 2009
Time: 08:38:26 AM
```

This represented an orderly Event Log service stop/shutdown.

The report also notes that the System log did not show unusual service installations during the reviewed period.

---

# 4️⃣ Exercise 4 – Deleted File Recovery

Deleted and recoverable files were investigated using file-carving techniques.

Autopsy's PhotoRec Carver module was enabled during ingestion.

The investigation focused on:

* Deleted files
* Unallocated-space artifacts
* Recovered documents
* Images
* Archives
* File metadata
* MD5/SHA-256 hashes

One recovered artifact was:

```text
A0000671.ini
```

from a System Restore point.

The report notes that this particular artifact appeared to be an empty placeholder rather than meaningful user document content.

---

# 5️⃣ Exercise 5 – Browser & Web Artifacts

Both Firefox and Internet Explorer artifacts were identified.

### Firefox

The Firefox profile included:

```text
profiles.ini
```

### Internet Explorer

The investigation identified:

```text
Temporary Internet Files\Content.IE5
```

---

## 🌐 Browser Findings

The investigation recovered:

* Web history
* Cookies
* Downloads
* Search artifacts
* Browser cache

The report recorded approximately:

```text
6,852 Web History entries
72 Web Search entries
```

Two downloads were identified:

```text
python-2.6.4.msi
Firefox Setup 3.5.5.exe
```

Both were identified as legitimate publicly distributed software packages.

---

## 📧 Email & Webmail Investigation

Two recovered email messages were identified:

```text
msg_25.txt
msg_43.txt
```

They were described as system-generated bounce/mailer-daemon messages rather than personal correspondence.

The reviewed web artifacts did not show cloud-storage, webmail, or file-sharing domains.

---

# 6️⃣ Exercise 6 – Timeline Reconstruction

Autopsy's Timeline module was used to combine timestamped evidence from multiple sources.

The timeline included artifacts from:

* File-system activity
* Registry
* Event Logs
* Browser history
* Recovered files
* Metadata

The timeline showed increasing activity from approximately 2004 onward, with significant activity during 2008–2009.

---

# 🧩 Investigation Timeline

A working chronology was constructed from the available evidence:

```text
12 Nov 2009
    │
    ├── Main workstation image acquired
    │
    ▼
13 Nov 2009
08:38:26 AM
    │
    ├── Event ID 6006
    ├── Event Log service stopped
    └── Orderly shutdown
    │
    ▼
11 Dec 2009
    │
    ├── USB evidence images acquired
    ├── jo-favorites-usb
    └── jo-work-usb
```

The report identifies the relationship between the workstation image and the two USB images as an important area for further correlation.

---

# 🔎 Key Findings

The investigation identified:

### System

```text
Windows XP Professional SP3
Build 2600
Registered Organization: MS7.biz
```

### Local Accounts

```text
Administrator
Guest
HelpAssistant
SUPPORT_388945a0
```

### USB Hardware Observed

```text
Logitech Optical Wheel Mouse
```

along with root-hub entries.

### Browser Activity

```text
6,852 Web History entries
72 Web Search entries
```

### Downloads

```text
python-2.6.4.msi
Firefox Setup 3.5.5.exe
```

### Event Log

```text
Event ID 6006
13 November 2009
08:38:26 AM
```

### USB Evidence

```text
jo-favorites-usb-2009-12-11.E01
jo-work-usb-2009-12-11.E01
```

These USB images are important for determining whether files were transferred from the workstation to removable media.

---

# ⚠️ Investigation Status

The examination **does not by itself establish that data was exfiltrated from the workstation**.

The report identifies three important correlations that still need to be completed:

1. **Security log analysis**

   * Logon activity
   * Account changes
   * Relevant timestamps

2. **USBSTOR correlation**

   * Determine whether either USB device was connected to the workstation.
   * Compare device serial numbers.

3. **Recovered-file comparison**

   * Hash recovered files.
   * Compare them with files on the two USB evidence images.

The report states that these correlations are required before reaching a definitive conclusion regarding the theft/exfiltration hypothesis.

---

# 📂 Recommended GitHub Structure

```text
Digital-Forensics-Windows-XP/
│
├── README.md
│
├── Dnyaneshwari_Forensic_Analysis_Report.pdf
│
└── screenshots/
    ├── autopsy-ingest.png
    ├── registry-analysis.png
    ├── event-log-analysis.png
    ├── deleted-file-recovery.png
    ├── browser-artifacts.png
    └── timeline.png
```

### Do NOT upload the original evidence images

```text
❌ jo-2009-11-12.E01
❌ jo-favorites-usb-2009-12-11.E01
❌ jo-work-usb-2009-12-11.E01
```

Keep the actual forensic evidence files out of your GitHub repository unless you have explicit permission to redistribute them.

---

# 📚 Skills Demonstrated

This project demonstrates practical experience with:

* Digital Forensics
* Disk Image Analysis
* E01 Evidence Handling
* Evidence Integrity Verification
* Hash Analysis
* Windows Registry Forensics
* USB Forensics
* Event Log Analysis
* Deleted File Recovery
* File Carving
* Browser Forensics
* Web Artifact Analysis
* Timeline Analysis
* Autopsy
* FTK Imager
* Registry Explorer

---

# 👩‍💻 Author

**Dnyaneshwari Kale**

Cybersecurity / Digital Forensics Student

**Focus Areas:**

`Digital Forensics` • `DFIR` • `SOC` • `Incident Response` • `Memory Forensics`

---

## 📄 Detailed Report

The complete forensic examination is documented in:

```text
Dnyaneshwari_Forensic_Analysis_Report.pdf
```

The report contains the detailed exercises, evidence analysis, screenshots, findings, and forensic procedures used during the investigation.
