# ✍️ Custom Snort Rule Authoring

Custom detection rules were created in:

/etc/snort/rules/local.rules


## 📌 Implemented Detection Rules

### 🔍 ICMP Reconnaissance
Detects ping sweeps and reconnaissance activity.

```snort
alert icmp any any -> any any (msg:"ICMP Ping Detected"; sid:1000001; rev:1;)

🔐 SSH Connection Monitoring
Alerts on SSH access attempts.

alert tcp any any -> any 22 (msg:"SSH Connection Attempt"; sid:1000003; rev:1;)

📡 SYN Scan Detection
Identifies potential port scanning behavior using thresholding.

alert tcp any any -> any any (msg:"SCAN DETECTED"; flags:S; detection_filter:track by_src, count 5, seconds 10; sid:1000004; rev:1;)

🧠 Lessons Learned
Importance of correct rule syntax
Use of sid and rev for rule management
Thresholding to reduce alert noise