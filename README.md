# Incident-handling-with-Splunk-command-control

## Project Report: Investigating the Cyber Attack on Wayne Enterprises
        ![image](https://github.com/user-attachments/assets/6d3d5e1c-846c-4908-8497-1654c98e3e93)


#### 1. Overview

Wayne Enterprises recently experienced a significant cyber attack, in which attackers infiltrated their network, compromised their web server, and successfully defaced their website, http://www.imreallynotbatman.com. The defaced website displayed a message stating, "YOUR SITE HAS BEEN DEFACED," along with the attackers' trademark. I was engaged as a Security Analyst to investigate the incident, identify the root cause, and trace all attacker activities within their network.

### 2. Command and Control Phase

During the investigation, I discovered that the attacker uploaded a malicious file to the server before executing the defacement. The file, named poisonivy-is-coming-for-you-batman.jpeg, was instrumental in the attack. The attacker utilized a Dynamic DNS (Domain Name System) to resolve a malicious IP address, enabling communication between the compromised server and the attacker's Command and Control (C2) server. My objective was to identify the IP address that the attacker resolved through the DNS and to trace all related activities.

To investigate the communication to and from the adversary’s IP addresses, I examined network-centric log sources, starting with the Fortinet firewall logs. The firewall logs provided valuable insights, including the source IP, destination IP, and the URL associated with the attack.

Search Query:


index=botsv1 sourcetype=fortigate_utm "poisonivy-is-coming-for-you-batman.jpeg"

![image](https://github.com/user-attachments/assets/eab338ee-2f35-4067-bd56-dcf23e6686a6)

By analyzing these logs, I identified critical details, including the Fully Qualified Domain Name (FQDN) associated with the malicious activities. The field url in the logs contained the FQDN, which confirmed the attacker's use of a dynamic DNS service.

![image](https://github.com/user-attachments/assets/dca0b558-5f86-40b1-8ad1-8c932957a16f)

To further verify the findings, I cross-referenced the data with another log source, stream:http. This log source provided additional evidence of the suspicious domain being used as a Command and Control server.

Search Query:


index=botsv1 sourcetype=stream:http dest_ip=23.22.63.114 "poisonivy-is-coming-for-you-batman.jpeg" src_ip=192.168.250.70

![image](https://github.com/user-attachments/assets/2018cecf-3388-424a-a769-937549b45576)


This query confirmed the communication between the compromised server and the Command and Control server. Additionally, by examining the stream:dns log source, I was able to verify the DNS queries sent from the web server during the infection period, further confirming the domain used in the attack.

### 3. Identified FQDN

The investigation revealed that the Fully Qualified Domain Name (FQDN) associated with the attack was:

FQDN: prankglassinebracket.jumpingcrab.com

### 4. Conclusion

The cyber attack on Wayne Enterprises was a sophisticated operation that leveraged a Dynamic DNS service to communicate with a malicious Command and Control server. Through meticulous analysis of various log sources, I was able to trace the attacker's activities, identify the root cause, and determine the specific FQDN used in the attack.

### 5. Experience Gained

This project provided me with invaluable experience in investigating complex cyber attacks, particularly those involving the use of Dynamic DNS and Command and Control servers. I honed my skills in analyzing firewall logs, HTTP traffic logs, and DNS queries, as well as in using Splunk to perform detailed search queries and log analysis.

### 6. Benefits

The investigation not only strengthened my expertise in cybersecurity but also underscored the importance of thorough log analysis in identifying and mitigating cyber threats. The knowledge gained from this project will be instrumental in future incident response efforts, enabling me to quickly identify and neutralize similar threats, ultimately contributing to a more secure network environment for organizations.

