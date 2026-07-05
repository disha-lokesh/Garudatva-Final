# Garudatva: A Legally Compliant Dual-Node Forensic Pipeline

![Garudatva Banner](https://img.shields.io/badge/Garudatva-Forensic%20Pipeline-blue?style=for-the-badge)
![License](https://img.shields.io/badge/license-GPL--3.0-green.svg)
![Status](https://img.shields.io/badge/status-Production%20Ready-brightgreen.svg)

**Garudatva** is a groundbreaking dual-node forensic analysis platform that bridges the critical gap between **Code** and **Court**. It combines advanced malware analysis, threat intelligence, and forensic investigation with rigorous legal compliance to meet Indian judicial standards.

> *"Garudatva is not just a malware scanner; it is a legally compliant, dual-node forensic pipeline that bridges the gap between Code and Court."*

---

## 🎯 Core Vision

Garudatva addresses a fundamental problem: **Indian law enforcement lacks a unified, court-admissible platform for analyzing sophisticated malware while maintaining forensic integrity and legal compliance.** 

Our solution transforms raw forensic analysis into legally defensible evidence through:
- **Dual-Node Architecture**: Air-gapped sandbox for analysis + internet-connected threat intel node
- **Deep Code Analysis**: Dynamic + static analysis with ML-powered threat classification
- **Threat Fingerprinting**: JA4+ client fingerprinting and JARM server profiling for C2 attribution
- **Anti-Forensics Detection**: Timestomping and data wiper detection via MFT/USN analysis
- **Legal Compliance**: Automated evidence chain generation compliant with BNSS, BSA, IT Act, and UAPA

---

## 🏗️ Architecture Overview

### **Workstation A: Air-Gapped Sandbox (Forensic Isolation)**
- Completely offline malware detonation environment
- QEMU/KVM hypervisor + Android Virtual Device (AVD) for APK execution
- MonkeyRunner automation for systematic payload triggering
- Frida hooking for deep runtime introspection
- Custom QR-bridge encoder for secure C2 extraction

### **Workstation B: Threat Intelligence Node (Connected)**
- Internet-connected threat reconnaissance platform
- JARM fingerprinting server profiling
- Cloud infrastructure sweeps (AWS, GCP, Azure, Cloudflare)
- Masscan-based IP range hunting
- External network probing and attribution

### **Secure Bridge: QR-Encoded Data Transfer**
- Custom Python/JavaScript QR codec
- Bridges air-gapped and connected nodes without compromise
- Encodes extracted C2 IP addresses into dense QR codes
- Webcam-based scanning for automated threat data handoff

---

## 🔍 Key Features

### **1. Dynamic & Static Analysis Engine**
- **MonkeyRunner Integration**: Automated pseudo-random UI interaction to trigger malware payloads
- **System Call Profiling**: `strace` integration for comprehensive PID-level syscall frequency logging
- **Deep Frida Hooking**:
  - `okhttp3.internal.http.RealInterceptorChain.proceed()` for network interception
  - `javax.crypto.Cipher.init` & `doFinal` for cryptographic key capture
  - Hashcode-based payload-to-key correlation
- **ML-Powered Classification**: Random Forest classifier (100 trees, Information Gain) filtering Android permissions to 87 critical features

### **2. Threat Reconnaissance & Fingerprinting**
- **JA4+ Client Fingerprinting**: Passive TLS Client Hello analysis within air-gapped sandbox
- **JARM Server Profiling**: Crafted TLS handshake probes for C2 server identification
- **CSP IP Sweeps**: Asynchronous scanning of public cloud provider ranges for JARM matches

### **3. Anti-Forensics Detection Module**
- **Timestomping Detection**: MFTECmd-based MFT parsing with `$STANDARD_INFORMATION` vs `$FILE_NAME` comparison
- **Data Wiper Detection**: USN Journal and Prefetch artifact monitoring for secure deletion attempts

### **4. Legal & Evidentiary Compliance Framework**

#### **Case Initialization (Om Prakash Verma Compliance)**
- Mandatory device IMEI, brand, and manufacturing details logging
- Physical device-to-digital evidence chain establishment

#### **BNSS Section 176(3) Compliance**
- Crime scene videography ingestion with geolocation metadata
- Structured evidence preservation workflows

#### **Zero-Dependency Hash Chains (Web Crypto API)**
- Canonical JSON serialization (alphabetical key sorting)
- UUIDv7-based chronological audit logs
- Tamper-detection via pure SHA-256 verification

#### **BSA Section 63 Compliance**
- Automated PDF certificate generation for computer functioning verification
- Self-executing audit trails

#### **UAPA Section 46 Tagging**
- Automatic disclaimer markup: *"Admissible under Section 46 of the UAPA Act"*
- C2 traffic preemptive privacy classification

#### **IT Act Section 79A Workflow**
- Dual-officer signature enforcement (Reporting Officer + Reviewing Officer)
- Examiner of Electronic Evidence certification

---

## 🚀 Quick Start

### Prerequisites
```bash
# System Requirements
- Workstation A: Offline Linux machine with QEMU/KVM, 16GB+ RAM
- Workstation B: Online Linux machine with Masscan, Nmap, network probes
- AVD Android emulator installed and configured
- Frida and Frida-server binaries
```

### Installation (Workstation A - Sandbox)
```bash
git clone https://github.com/disha-lokesh/Garudatva-Final.git
cd Garudatva-Final

# Install Python dependencies
pip install -r requirements-sandbox.txt

# Initialize AVD
python setup_avd.py

# Test air-gap QR bridge
python qr_bridge_encoder.py --test
```

### Installation (Workstation B - Threat Intel)
```bash
# Install scanning tools
apt-get install masscan nmap jq

# Install Python dependencies
pip install -r requirements-threatintel.txt

# Initialize threat intel modules
python setup_threatintel.py
```

### Basic Analysis Workflow
```bash
# Step 1: Load APK on Workstation A
python load_apk.py --apk suspicious_app.apk

# Step 2: Execute MonkeyRunner with Frida hooks
python execute_analysis.py --hooks cryptography,network --duration 300

# Step 3: Extract logs and encode C2 data via QR
python extract_and_encode.py --output-qr threat_data.qr

# Step 4: Scan QR on Workstation B and launch threat intel
python scan_qr_and_hunt.py --qr-image threat_data.qr

# Step 5: Generate legally compliant report
python generate_legal_report.py --case-id "2026-CIDECODE-001" --output report.pdf
```

---

## 📋 Project Structure

```
Garudatva-Final/
├── sandbox/
│   ├── avd_setup/               # Android Virtual Device configuration
│   ├── frida_hooks/             # Deep Frida instrumentation scripts
│   │   ├── cryptography.js
│   │   ├── network_intercept.js
│   │   └── syscall_profiler.js
│   ├── monkeyrunner/            # Automated APK interaction
│   ├── qr_bridge/               # QR encoder/decoder for air-gap data transfer
│   └── analysis_engine/         # Core analysis orchestration
├── threatintel/
│   ├── jarm_profiler/           # Server fingerprinting
│   ├── masscan_sweeper/         # Cloud IP range hunting
│   ├── ja4_classifier/          # Client fingerprinting
│   └── csp_modules/             # AWS/GCP/Azure/Cloudflare scanners
├── forensics/
│   ├── anti_forensics/
│   │   ├── mft_parser/          # Timestomping detection
│   │   └── usn_analyzer/        # Data wiper detection
│   └── ml_classifier/           # Permission-based threat classification
├── legal/
│   ├── compliance_engine/
│   │   ├── case_wizard/         # BNSS Section 176(3)
│   │   ├── audit_chain/         # Hash chain generation
│   │   └── certificates/        # BSA Section 63 PDF generation
│   └── report_generator/        # Dual-officer signature workflow
├── config/
│   ├── legal_compliance.yaml    # Jurisdiction-specific rules
│   └── ml_models/               # Trained Random Forest classifier
└── tests/                       # Integration & unit tests
```

---

## 📊 Analysis Output

### **Dynamic Analysis Report**
```json
{
  "malware_name": "TrojanSpy.APK",
  "c2_servers": [
    {
      "ip": "192.168.1.100",
      "port": 8443,
      "protocol": "TLS 1.2",
      "jarm_fingerprint": "27d3ed7ed0e...",
      "cloud_provider": "AWS (us-east-1)"
    }
  ],
  "cryptographic_keys": [
    {
      "key_hash": "aes256_key_0x7f...",
      "algorithm": "AES-256-GCM",
      "payload_count": 47,
      "intercepted_packets": 156
    }
  ],
  "network_interceptions": [
    {
      "timestamp": "2026-07-05T14:23:45Z",
      "source": "192.168.1.50:54321",
      "destination": "192.168.1.100:8443",
      "data_size": 2048,
      "encryption_status": "encrypted"
    }
  ]
}
```

### **Legal Report (Court-Ready)**
```
DIGITAL EVIDENCE ANALYSIS REPORT
Case ID: 2026-CIDECODE-001
Investigation Officer: [BNSS §176(3) Verified IMEI: ...]

═══════════════════════════════════════
CHAIN OF CUSTODY (SHA-256 Hash Chain)
═══════════════════════════════════════
Event 1: Device Acquisition
  Timestamp: 2026-07-05T10:00:00Z
  Hash: 3a7f2b1c9e4d...
  Status: ✓ Verified

Event 2: Malware Extraction
  Timestamp: 2026-07-05T10:15:22Z
  Hash: 8f2e1a4c7b9d...
  Status: ✓ Verified

Event 3: Analysis Completed
  Timestamp: 2026-07-05T14:30:00Z
  Hash: c1d5f3a9e2b4...
  Status: ✓ Verified

═══════════════════════════════════════
ADMISSIBILITY CERTIFICATION
═══════════════════════════════════════
✓ Bharatiya Sakshya Adhiniyam (BSA) §63
✓ Bharatiya Nyaya Sanhita (BNSS) §176(3)
✓ Information Technology Act §79A
✓ Unlawful Activities (Prevention) Act §46

Reporting Officer: _________________
Reviewing Officer: __________________
Date: 2026-07-05
```

---

## 🎓 Use Cases

1. **Law Enforcement**: Investigate sophisticated mobile malware with court-ready evidence
2. **Cybersecurity Researchers**: Analyze APK malware families with rigorous forensic methods
3. **Digital Forensics Experts**: Detect anti-forensics attempts and preserve evidence integrity
4. **Legal Compliance**: Generate admissible evidence for criminal prosecution under Indian law

---

## 🛡️ Security & Forensic Integrity

- **Air-Gap Architecture**: Complete isolation between analysis and threat intel phases
- **Forensic Isolation**: No internet connectivity during malware execution
- **Cryptographic Verification**: SHA-256 hash chains prevent evidence tampering
- **Anti-Forensics Detection**: Built-in mechanisms to catch malware evasion attempts
- **Legal Chain of Custody**: Every step documented and verified for court admissibility

---

## 📚 Legal Compliance

Garudatva is designed to comply with:
- **Bharatiya Nyaya Sanhita (BNSS)** – Criminal Procedure Code
- **Bharatiya Sakshya Adhiniyam (BSA)** – Evidence Act
- **Information Technology Act, 2000** – Digital Evidence Rules
- **Unlawful Activities (Prevention) Act, 1967** – Section 46 (Intercepted Communication Admissibility)

---

## 🏆 Built for CIDECODE 2026

Garudatva was architected and developed as the flagship submission for **CIDECODE 2026 Hackathon**—India's premier cybercrime detection and investigation challenge.

**Our Unique Selling Proposition:**
- Only platform combining advanced malware analysis with judicial compliance
- Bridges India's law enforcement gap between technical forensics and legal admissibility
- Production-ready dual-node architecture with court-admissible evidence chains

---

## 👥 Team & Contributors

**Development Team**: Disha Lokesh and Contributors  
**Research Advisor**: Cybersecurity & Digital Forensics Specialists  
**Legal Consultant**: Indian Judicial Compliance Expert

---

## 📖 Documentation

- [Architecture Deep Dive](./docs/ARCHITECTURE.md)
- [Legal Compliance Guide](./docs/LEGAL_COMPLIANCE.md)
- [Frida Hooking Guide](./docs/FRIDA_GUIDE.md)
- [Threat Intelligence Workflow](./docs/THREATINTEL_WORKFLOW.md)
- [Case Study: Real-World Malware Analysis](./docs/CASE_STUDIES.md)

---

## 🤝 Contributing

We welcome contributions! Please read [CONTRIBUTING.md](./CONTRIBUTING.md) before submitting issues, feature requests, or pull requests.

### Areas for Contribution:
- Additional Frida hooking modules for specific malware families
- Enhanced ML classification algorithms
- Additional cloud provider scanners (Azure, Alibaba, etc.)
- UI/UX improvements for the dashboard
- Localization for additional Indian jurisdictions

---

## 📝 License

Garudatva is licensed under the **GNU General Public License v3.0** – See [LICENSE](./LICENSE) for details.

---

## 🙏 Acknowledgments

- Indian law enforcement and cybercrime investigation community
- Open-source security research pioneers
- Legal compliance experts who shaped our evidentiary framework
- The CIDECODE 2026 organizing committee for inspiring innovation in digital forensics

---

## 📞 Support & Contact

- **GitHub Issues**: For bug reports and feature requests
- **Documentation**: Full guides available in `/docs`
- **Legal Questions**: Consult the [Legal Compliance Guide](./docs/LEGAL_COMPLIANCE.md)

---

**Made with 🔐 Security & ⚖️ Justice in India**

---

*Last Updated: July 5, 2026*  
*Version: 3.0.0 (CIDECODE 2026 Release)*
