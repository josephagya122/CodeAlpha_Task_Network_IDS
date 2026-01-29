# 🔍 Traffic Analysis & Logging

## 📡 Real-Time Monitoring
Snort was executed in console alert mode for immediate visibility:

```bash
sudo snort -A console -q -u snort -g snort -c /etc/snort/snort.conf -i enp0s3
🧪 Validation Tests
ping google.com

nmap -F localhost

These actions successfully triggered alerts, validating rule functionality.

📁 Log Files Location
After stopping Snort (Ctrl + C), logs were analyzed from:

/var/log/snort/
📄 Alert Logs
sudo cat /var/log/snort/alert

📦 PCAP Analysis
sudo snort -r /var/log/snort/snort.log.[timestamp]

🛠️ Troubleshooting
Fixed syntax errors related to missing semicolons
Prevented corrupted PCAPs by allowing proper process termination

