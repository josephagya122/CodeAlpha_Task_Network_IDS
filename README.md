🛡️ Network Intrusion Detection System (NIDS/NIPS)
Cybersecurity Internship Project: Snort & Iptables Implementation
📖 Project Overview
This project demonstrates the deployment of Snort, an open-source Network Intrusion Detection System (IDS), on an Ubuntu 22.04 LTS environment. The objective was to monitor live network traffic, identify malicious patterns using custom signature-based rules, and implement active response mechanisms (IPS) using both Snort’s Inline mode and Linux iptables to drop unauthorized traffic.

🛠️ Phase 1: Environment & Tool Setup
The system was built within a virtualized environment to simulate a corporate network segment.
OS: Ubuntu 22.04.5 Desktop (VirtualBox)
Interface: enp0s3
Installation:
Bash
sudo apt update && sudo apt install snort -y




Verification: Installation was verified by checking the version (snort -V) and ensuring the configuration file was accessible at /etc/snort/snort.conf.

✍️ Phase 2: Custom Rule Authoring
I authored specific signatures in /etc/snort/rules/local.rules to detect and alert on suspicious behaviors.
Implemented Rules
Attack Type
Logic
Rule Snippet
ICMP Recon
Detection of Pings
alert icmp any any -> any any (msg:"ICMP Ping Detected"; sid:1000001; rev:1;)
SSH Monitoring
Access Attempts
alert tcp any any -> any 22 (msg:"SSH Connection Attempt"; sid:1000003; rev:1;)
SYN Scan
Threshold Filter
alert tcp any any -> any any (msg:"SCAN DETECTED"; flags:S; detection_filter:track by_src, count 5, seconds 10; sid:1000004; rev:1;)


🔍 Phase 3: Traffic Analysis & Logging
Monitoring was conducted in real-time with alerts output directly to the console for immediate analysis.
Real-Time Detection
Bash
sudo snort -A console -q -u snort -g snort -c /etc/snort/snort.conf -i enp0s3


Validation Results: Successfully triggered alerts via ping google.com and nmap -F localhost to verify the detection_filter logic.
Post-Capture Analysis
After stopping the process (Ctrl+C), logs were verified in /var/log/snort/:
Text Alerts: sudo cat /var/log/snort/alert
Binary PCAPs: Analyzed using sudo snort -r /var/log/snort/snort.log.[timestamp]

🛑 Phase 4: Active Response Mechanisms (IPS)
The system was transitioned from passive monitoring to active prevention using two distinct methods.
Method A: Snort Inline Mode (AFPacket)
Using the drop action, Snort was configured to actively discard packets matching the signature.
Bash
sudo snort -q -Q --daq afpacket -i enp0s3 -c /etc/snort/snort.conf


Method B: Manual IP Blocking via Iptables
For persistent threats, I implemented kernel-level blocks to drop all traffic from specific malicious source IPs:
Bash
sudo iptables -A INPUT -s 192.168.10.50 -j DROP


Verification: Used sudo iptables -L -v -n to confirm the rule was active and monitored the packet loss during test pings.

🛠️ Troubleshooting & Fixes
Syntax Errors: Resolved Unknown rule option errors by ensuring proper semicolon (;) separators and colon (:) usage for sid values.
Binary Corruptions: Addressed truncated dump file errors by ensuring the Snort process had sufficient time to write to disk before being interrupted.
Legacy Tools: Identified that Barnyard2 is deprecated in modern Ubuntu 22.04 repositories; investigated Filebeat as a modern alternative for log ingestion.

🚀 Key Takeaways
Learned to translate high-level security policies into signature-based detection rules.
Understood the critical difference between Passive (IDS) and Inline (IPS) monitoring modes.
Gained experience with the AFPacket DAQ for high-performance packet processing.
Mastered the integration of IDS alerts with iptables for manual threat mitigation.

