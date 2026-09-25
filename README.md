# 🛡️ SOC Home Lab

### Hands-on Security Operations Center Lab for Detection, Monitoring, Investigation & Incident Response

---

## 📑 Table of Contents

- [Introduction](#-introduction)
- [Lab Architecture](#-lab-architecture)
- [Lab Environment](#-lab-environment)
- [Security Tools](#-security-tools)
- [Detection Pipeline](#-detection-pipeline)
- [Attack & Detection Scenarios](#-attack--detection-scenarios)
- [Alert Investigation Workflow](#-alert-investigation-workflow)
- [MITRE ATT&CK Mapping](#-mitre-attck-mapping)
- [Repository Structure](#-repository-structure)
- [Skills Demonstrated](#-skills-demonstrated)
- [Future Improvements](#-future-improvements)
- [Conclusion](#-conclusion)

---

# 🔎 Introduction

The **SOC Home Lab** is a hands-on cybersecurity environment built to practice the core activities of a Security Operations Center.

The lab simulates security activity against a monitored Windows endpoint and uses centralized monitoring and network security tools to:

> **Generate Activity → Collect Telemetry → Detect → Investigate → Map → Respond**

The project focuses on practical SOC skills including security monitoring, alert triage, network analysis, endpoint investigation, detection engineering, and incident response.

---

# 🏗️ Lab Architecture

```text
                 ┌──────────────────────┐
                 │    Ubuntu Attacker   │
                 │   Recon / Testing    │
                 └──────────┬───────────┘
                            │
                            │ Network Activity
                            ▼
                 ┌──────────────────────┐
                 │    Windows Victim    │
                 │   Monitored Endpoint │
                 │                      │
                 │       Sysmon         │
                 └──────────┬───────────┘
                            │
                            │ Security Telemetry
                            ▼
                 ┌──────────────────────┐
                 │        Wazuh         │
                 │         SIEM         │
                 │                      │
                 │ Log Collection       │
                 │ Detection Rules      │
                 │ Alert Generation     │
                 │ Investigation        │
                 └──────────┬───────────┘
                            ▲
                            │
                   Network Detection
                            │
                 ┌──────────┴───────────┐
                 │       Suricata       │
                 │      Network IDS     │
                 └──────────────────────┘
```

---

# 💻 Lab Environment

| Component | Purpose |
|---|---|
| **Ubuntu** | Attacker and security testing machine |
| **Windows** | Monitored victim endpoint |
| **Wazuh** | SIEM, log collection, detection and alert management |
| **Suricata** | Network intrusion detection |
| **Sysmon** | Windows endpoint telemetry |
| **Wireshark** | Network packet analysis |
| **Nmap** | Network reconnaissance and service discovery |
| **MITRE ATT&CK** | Attack technique mapping |

---

# 🛠️ Security Tools

### Wazuh

Used as the central SIEM for:

- Log collection
- Security event monitoring
- Detection rules
- Alert generation
- Alert investigation

### Suricata

Used for network-based detection through:

- IDS signatures
- Network traffic inspection
- Protocol analysis
- Suspicious traffic detection

### Sysmon

Used to collect detailed Windows endpoint telemetry, including:

- Process creation
- Network connections
- Process relationships
- Other endpoint activity

### Wireshark

Used for packet-level investigation of:

- IP addresses
- Ports
- Protocols
- Network connections
- Suspicious traffic

### Nmap

Used to generate controlled reconnaissance activity and analyze:

- Hosts
- Open ports
- Running services
- Network exposure

---

# 🔄 Detection Pipeline

```text
       Attack / Suspicious Activity
                    │
                    ▼
        Network / Endpoint Activity
                    │
             ┌──────┴──────┐
             ▼             ▼
         Suricata        Sysmon
             │             │
             └──────┬──────┘
                    │
                    ▼
                  Wazuh
                    │
                    ▼
              Detection Rule
                    │
                    ▼
                  Alert
                    │
                    ▼
              Investigation
                    │
                    ▼
             MITRE ATT&CK
                    │
                    ▼
                 Response
```

---

# ⚔️ Attack & Detection Scenarios

The lab is used to generate and investigate different categories of security activity.

| Scenario | Activity | Investigation Focus |
|---|---|---|
| **Network Reconnaissance** | Host, port and service discovery | Source IP, destination IP, ports and connection patterns |
| **Authentication Activity** | Repeated or abnormal authentication attempts | Username, source, result, timestamp and frequency |
| **Suspicious Network Traffic** | Traffic matching IDS signatures | Signature, protocol, source, destination and severity |
| **Windows Endpoint Activity** | Process and network activity | Process information, network connections and user context |
| **Custom Detection Rules** | Specific behaviors detected by Wazuh rules | Rule ID, rule level and matching conditions |

---

# 🔍 Alert Investigation Workflow

When an alert is generated, the investigation follows a structured process:

| Step | Action |
|---|---|
| **1. Identify** | Review alert severity, rule ID, timestamp and description |
| **2. Locate** | Identify source, destination, host, user or process |
| **3. Analyze** | Determine what activity generated the alert |
| **4. Correlate** | Compare related Wazuh, Suricata and Sysmon events |
| **5. Map** | Identify the relevant MITRE ATT&CK technique |
| **6. Respond** | Apply the appropriate defensive response based on the investigation |

---

# 🧩 MITRE ATT&CK Mapping

Security activity is mapped to relevant MITRE ATT&CK techniques during investigation.

| Observed Activity | MITRE ATT&CK Technique |
|---|---|
| Network service scanning | **T1046 — Network Service Scanning** |
| Repeated authentication attempts | **T1110 — Brute Force** |
| Command or script execution | **T1059 — Command and Scripting Interpreter** |

> Technique mappings are based on the behavior observed during the investigation.

---

# 📁 Repository Structure

```text
SOC-Home-Lab/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── architecture/
│   └── architecture.png
│
├── screenshots/
│   ├── wazuh-dashboard.png
│   ├── suricata-alert.png
│   ├── sysmon-event.png
│   ├── nmap-detection.png
│   ├── alert-investigation.png
│   └── mitre-mapping.png
│
├── wazuh/
│   ├── rules/
│   │   └── local_rules.xml
│   └── configuration/
│       └── ossec.conf.example
│
├── suricata/
│   └── rules/
│       └── local.rules
│
├── sysmon/
│   └── sysmon-config.xml
│
├── attacks/
│   ├── reconnaissance.md
│   ├── authentication-attacks.md
│   └── other-scenarios.md
│
├── investigations/
│   ├── alert-investigation.md
│   └── incident-response.md
│
└── mitre/
    └── attack-mapping.md
```

---

# 🧠 Skills Demonstrated

- SIEM monitoring with Wazuh
- Security alert triage
- Network reconnaissance analysis
- Network IDS monitoring
- Windows endpoint monitoring
- Sysmon event analysis
- Packet analysis with Wireshark
- Wazuh detection rule development
- Event correlation
- MITRE ATT&CK mapping
- Incident investigation
- Basic incident response

---

# 🚀 Future Improvements

- Expand custom Wazuh detection rules
- Add additional endpoints
- Expand Suricata detection coverage
- Add more controlled attack scenarios
- Perform structured threat-hunting exercises
- Expand MITRE ATT&CK coverage
- Improve event correlation

---

# 🏁 Conclusion

The **SOC Home Lab** provides a practical environment for developing core SOC analyst skills using open-source security tools.

The project combines:

**Wazuh + Suricata + Sysmon + Wireshark + Nmap**

to practice the security operations lifecycle:

> **Detection → Triage → Investigation → Threat Mapping → Response**

This project provides a foundation for progressing into more advanced areas such as **threat hunting, detection engineering, cloud security, and security automation**.
