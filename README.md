# SOC-Lab-Golden-Ticket-Detection
building a soc lab to detect Kerberos attack using Splunk and Sysmon


Project Overview : this project simulate a golden ticket attack in an active directory environment 

Network Diagram :  Attacket => Kali linux  
                   Victim => Windows Server 2022 (Doamin Controller)
                   SIEM => Splunk Enterprise on ubunto

Tools Used : Splunk , Sysmon , Mimikatz 

<img width="1275" height="901" alt="2026-03-28 11_00_17-windows-server  Running  - Oracle VirtualBox" src="https://github.com/user-attachments/assets/3fccc057-b01c-441f-bcc2-8f4577be0820" />
ensure connecting from windows server to Splunk 
<img width="1114" height="960" alt="mimikatz-result" src="https://github.com/user-attachments/assets/ab7bcc46-a064-4587-8158-9e33c45f54fc" />
execute attack locally on domain controller to simulate credential dumping phase after getting access priviliges , using mimikatz to extract krbtgt account's sensitive data 
<img width="1920" height="942" alt="2026-03-29 16_55_04-kali-linux-2025 4-virtualbox-amd64 ()  Running  - Oracle VirtualBox" src="https://github.com/user-attachments/assets/1c8050fb-7f98-4e62-bf12-754e299d0744" />
this screenshot from SPLUNK confirm the successful detection of Credentail Dumping attack . The Sysmon Event ID 10 (Process Access) was triggered when the source process mimikatz.exe attempted to access the memory of the target process lsass.exe 
Key Indicators in the Log:

SourceImage: mimikatz.exe (The attacker tool).

TargetImage: lsass.exe (The target system process containing credentials).

GrantedAccess: 0x143a (A high-fidelity indicator showing full read access to LSASS memory).

MITRE Mapping: This aligns with MITRE ATT&CK Technique T1003.001 (LSASS Memory)
