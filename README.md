🛡️ Network Intrusion Detection & Prevention System (NIDS/NIPS)
An Implementation of Snort & Iptables on Ubuntu 22.04 LTS

📖 Project Overview
This project demonstrates the deployment of Snort as both a passive detection system (IDS) and an active prevention system (IPS). By authoring custom signature-based rules and integrating Linux iptables, I established a robust mechanism to monitor, log, and drop malicious network traffic in real-time.

🛠️ Tech Stack & Environment
OS: Ubuntu 22.04.5 LTS (VirtualBox)

Security Tools: Snort (IDS/IPS), Nmap (Testing), Iptables (Firewall)

Traffic Analysis: AFPacket DAQ, PCAP Analysis

✍️ Implementation Phases
1. Custom Rule Development
Authored granular signatures in /etc/snort/rules/local.rules to detect reconnaissance and brute-force patterns:

ICMP Recon: Identified ping sweeps and discovery attempts.

SSH Monitoring: Tracked unauthorized access attempts on Port 22.

SYN Scan Detection: Implemented detection_filter to alert on rapid port scanning (5+ attempts/10s).

2. Real-Time Detection & Logging
Executed live monitoring with optimized console output:

Bash
sudo snort -A console -q -u snort -g snort -c /etc/snort/snort.conf -i enp0s3
Validation: Verified logic via nmap and ping triggers.

Forensics: Analyzed binary logs (PCAPs) for post-capture incident response.

3. Active Response (IPS)
Transitioned from monitoring to mitigation using two methods:

Inline Mode: Leveraged AFPacket DAQ to drop packets matching "drop" rules.

Kernel-Level Blocking: Integrated manual iptables rules to permanently blacklist malicious source IPs.

🚀 Key Learning Outcomes
Signature Logic: Translated security policies into actionable Snort rules.

IDS vs. IPS: Mastered the switch from passive alerting to active packet discarding.

Troubleshooting: Resolved syntax errors in rule options and addressed binary file corruption during high-traffic dumps.

Legacy vs. Modern: Researched Filebeat as a modern alternative to the deprecated Barnyard2 for log ingestion.
