# 🛠️ Environment & Tool Setup

## 🖥️ System Environment
- OS: Ubuntu 22.04.5 Desktop
- Virtualization: VirtualBox
- Network Interface: enp0s3

## 🔧 Snort Installation
Snort was installed using the Ubuntu package manager:

```bash
sudo apt update && sudo apt install snort -y

Checked Snort version:

snort -V


Verified configuration file:

/etc/snort/snort.conf

🧪 Testing Interface

Confirmed the correct network interface using:

ip a