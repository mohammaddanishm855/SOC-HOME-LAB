# ⚙️ SOC Home Lab Setup

This guide covers the installation and basic configuration of the tools used in the SOC Home Lab.

## 1. Prerequisites

Recommended:

- 8 GB RAM or more
- 4 CPU cores or more
- 50 GB+ free storage
- VirtualBox or another hypervisor
- Ubuntu
- Windows 10/11

Create separate virtual machines for:

- Ubuntu security-testing system
- Windows monitored endpoint
- Ubuntu Wazuh server

Use an isolated or host-only network for the lab.

---

## 2. Ubuntu Setup

Update the system:

```bash
sudo apt update
sudo apt upgrade -y
```

Install required tools:

```bash
sudo apt install -y curl wget git nmap wireshark
```

Verify:

```bash
nmap --version
wireshark --version
```

---

## 3. Wazuh Server

The lab uses **Wazuh 4.14.7**.

Download the Wazuh installation assistant:

```bash
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
```

Run the all-in-one installation:

```bash
sudo bash wazuh-install.sh -a
```

After installation, check the Wazuh Manager:

```bash
sudo /var/ossec/bin/wazuh-control status
```

Check the installed version:

```bash
sudo /var/ossec/bin/wazuh-control info -v -r -t
```

Expected:

```text
v4.14.7
```

Access the Wazuh Dashboard:

```text
https://<WAZUH_SERVER_IP>
```

Replace `<WAZUH_SERVER_IP>` with the IP address of the Wazuh server.

> Store Wazuh passwords, certificates, private keys, and other credentials securely. Do not commit them to GitHub.

---

## 4. Windows Wazuh Agent

Download the **Wazuh Agent 4.14.7** installer for Windows.

During installation, configure the Wazuh Manager address:

```text
<WAZUH_SERVER_IP>
```

Start the agent from PowerShell as Administrator:

```powershell
Start-Service WazuhSvc
```

Verify:

```powershell
Get-Service WazuhSvc
```

The agent should appear as connected in the Wazuh Dashboard.

---

## 5. Sysmon

Download Sysmon from Microsoft's Sysinternals tools.

Extract the archive and open PowerShell as Administrator.

Navigate to the Sysmon directory:

```powershell
cd C:\Sysmon
```

Install Sysmon:

```powershell
.\Sysmon64.exe -accepteula -i
```

Verify:

```powershell
Get-Service Sysmon64
```

Sysmon events can be viewed in:

```text
Event Viewer
→ Applications and Services Logs
→ Microsoft
→ Windows
→ Sysmon
→ Operational
```

---

## 6. Suricata

Install Suricata:

```bash
sudo apt update
sudo apt install -y suricata
```

Verify:

```bash
suricata --build-info
```

Test the configuration:

```bash
sudo suricata -T -c /etc/suricata/suricata.yaml
```

Start Suricata:

```bash
sudo systemctl start suricata
```

Enable it at boot:

```bash
sudo systemctl enable suricata
```

Check the service:

```bash
sudo systemctl status suricata
```

Suricata logs are located in:

```text
/var/log/suricata/
```

---

## 7. Wireshark

Install Wireshark:

```bash
sudo apt update
sudo apt install -y wireshark
```

Verify:

```bash
wireshark --version
```

Launch:

```bash
wireshark
```

Wireshark can be used to capture and investigate network traffic.

---

## 8. Nmap

Install Nmap:

```bash
sudo apt update
sudo apt install -y nmap
```

Verify:

```bash
nmap --version
```

Example scan inside the lab:

```bash
nmap -sV <TARGET_IP>
```

Only scan systems that you own or are authorized to test.

---

## 9. Verify the Lab

### Wazuh

```bash
sudo /var/ossec/bin/wazuh-control status
```

### Windows Agent

```powershell
Get-Service WazuhSvc
```

### Sysmon

```powershell
Get-Service Sysmon64
```

### Suricata

```bash
sudo systemctl status suricata
```

### Network Connectivity

From Ubuntu:

```bash
ping <WINDOWS_IP>
ping <WAZUH_SERVER_IP>
```

From Windows:

```powershell
ping <WAZUH_SERVER_IP>
```

Once these components are operational, the SOC Home Lab is ready for security monitoring, detection, alert investigation, network analysis, and incident response practice.
