# SOC-Lab-Golden-Ticket-Detection
A comprehensive SOC lab environment designed to simulate and detect the Credential Dumping phase, a prerequisite for the Golden Ticket attack, using Splunk (SIEM) and Sysmon


🚀 Project Overview
This project simulates an Active Directory environment attack. It focuses on detecting the initial stage of a Kerberos Golden Ticket attack: extracting the KRBTGT account hash by dumping the memory of the LSASS process

🏗️Network Architecture & Lab Setup :
Victim Node: Windows Server 2022 (Domain Controller) - Monitored by Sysmon.

SIEM Platform: Splunk Enterprise on Ubuntu Server.

Data Transport: Splunk Universal Forwarder .

🛠️Tools Used :
Splunk: Log indexing, analysis, and alerting.

Sysmon: Enhanced Windows event logging (Event ID 10).

Mimikatz: Credential extraction and memory manipulation.

Oracle VirtualBox: Lab virtualization. 

🛡️ Implementation Steps : 
1. Connectivity & Data Ingestion
The Windows Server (Victim) was successfully integrated with the Splunk (SIEM) instance. I verified the connection to ensure that Sysmon logs were being ingested into the main index in real-time.
<img width="1275" height="901" alt="2026-03-28 11_00_17-windows-server  Running  - Oracle VirtualBox" src="https://github.com/user-attachments/assets/3fccc057-b01c-441f-bcc2-8f4577be0820" />


2. Attack Simulation: Credential Dumping
After gaining administrative access, I executed Mimikatz locally on the Domain Controller. The goal was to extract sensitive data from the KRBTGT account, which is essential for forging a Golden Ticket.
<img width="1114" height="960" alt="mimikatz-result" src="https://github.com/user-attachments/assets/ab7bcc46-a064-4587-8158-9e33c45f54fc" />




3. Detection & Investigation (The "Smoking Gun")
Using Splunk, I performed a targeted search to identify the attack. The logs confirm a High-Fidelity Detection of the Credential Dumping attempt.

Key Indicators of Compromise (IoCs) Found:
Event ID: 10 (Process Access).

Source Image: mimikatz.exe (The malicious tool).

Target Image: lsass.exe (The system process containing credentials).

Granted Access: 0x143a (A specific access mask indicating full read/query permissions to LSASS memory—highly suspicious).
<img width="1920" height="942" alt="2026-03-29 16_55_04-kali-linux-2025 4-virtualbox-amd64 ()  Running  - Oracle VirtualBox" src="https://github.com/user-attachments/assets/1c8050fb-7f98-4e62-bf12-754e299d0744" />

🔍 MITRE ATT&CK Mapping : 
Tactic: Credential Access (TA0006)
Technique: OS Credential Dumping: LSASS Memory (T1003.001)
