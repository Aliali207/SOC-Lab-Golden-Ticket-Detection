# SOC-Lab-Golden-Ticket-Detection
building a soc lab to detect Kerberos attack using Splunk and Sysmon


Project Overview : this project simulate a golden ticket attack in an active directory environment 

Network Diagram :  Attacket => Kali linux  
                   Victim => Windows Server 2022 (Doamin Controller)
                   SIEM => Splunk Enterprise on ubunto

Tools Used : Splunk , Sysmon , Mimikatz 

<img width="1275" height="901" alt="2026-03-28 11_00_17-windows-server  Running  - Oracle VirtualBox" src="https://github.com/user-attachments/assets/3fccc057-b01c-441f-bcc2-8f4577be0820" />
ensure connecting from windows server to Splunk 
<img width="1280" height="1003" alt="2026-03-28 11_32_47-" src="https://github.com/user-attachments/assets/28866fe0-15f0-41b7-9649-cf769c43126a" />
execute attack locally on domain controller to simulate credential dumping phase after getting access priviliges , using mimikatz to extract krbtgt account's sensitive data 
