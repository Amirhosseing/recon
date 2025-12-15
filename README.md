🛡️ Recon Pipeline
The Ultimate Automated Reconnaissance Framework

Recon Pipeline is a fully automated, real-time, web-based reconnaissance framework built with Flask and Socket.IO. It orchestrates industry-standard tools in a smart, dependency-aware pipeline to perform end-to-end reconnaissance with a beautiful, dark-themed offline UI.

🚀 How It Works
Unlike simple script wrappers, Recon Pipeline performs true tool chaining. It ensures only live, validated targets are passed to subsequent stages to save time and resources.

The Pipeline Flow:
Subfinder ➔ DNSx ➔ HTTPX ➔ TLSx ➔ Nmap ➔ Nuclei ➔ FFUF

✨ Key Features
⚡ Real-Time Updates: Live progress tracking via WebSockets.

🌐 Web-Based UI: Fully offline, dark-themed interface (No CDNs/External calls).

🔗 Smart Chaining: Output of one tool feeds the next (e.g., only HTTP alive hosts go to Nuclei).

📂 VHost Discovery: Dedicated step for Virtual Host brute-forcing on shared IPs.

📦 One-Click Export: Download all results and raw logs as a single ZIP archive.

🔒 Secure: Simple login protection and local execution.

🛠️ Prerequisites
Ensure you have Python 3, Go, and Nmap installed.

1. Install Core Tools
You must have the following tools in your system $PATH:

bash
# Install Nmap
sudo apt install nmap -y

# Install ProjectDiscovery Tools (Go required)
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
go install -v github.com/projectdiscovery/dnsx/cmd/dnsx@latest
go install -v github.com/projectdiscovery/httpx/cmd/httpx@latest
go install -v github.com/projectdiscovery/tlsx/cmd/tlsx@latest
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest

# Install FFUF
go install -v github.com/ffuf/ffuf/v2@latest

# Add Go binaries to PATH (if not already done)
export PATH=$PATH:~/go/bin
📥 Installation
bash
# 1. Clone the repository
git clone https://github.com/amirhosseing/recon-pipeline.git
cd recon-pipeline

# 2. Install Python dependencies
pip3 install flask flask-socketio
🖥️ Usage
Start the Server:

bash
python3 app.py
Access the UI:
Open your browser and navigate to: http://localhost:5000

Login:

Username: administrator

Password: Qwer12#$

⚠️ Please change these credentials in app.py before use!

📂 Output Structure
All results are organized in the scans/ directory. Each stage produces JSON output for easy parsing.

text
scans/
├── subfinder.json       # Passive Subdomains
├── dnsx.json            # Resolved IPs
├── httpx.json           # Active Web Servers & Tech Stack
├── tlsx.json            # Certificates Info
├── nmap.xml             # Port Scan Results
├── nuclei.json          # Vulnerabilities
├── ffuf_dir.json        # Directory Fuzzing
├── live_hosts.txt       # Validated Host List
└── summary.json         # Scan Metadata
🔍 Virtual Host Scanning
This framework includes a dedicated step for VHost discovery. It bypasses reverse proxies by fuzzing the Host header against the direct IP address found during the DNS resolution phase.

Logic:
http://<Shared_IP> -H "Host: FUZZ.target.com"

🤝 Contributing
Pull requests are welcome! We are looking for:

Integrations (Amass, Katana).

Dark/Light mode toggles.

Improved error handling.

⚠️ Disclaimer
This project is intended for authorized security testing and research only. The user is responsible for complying with all applicable laws and regulations. The authors are not responsible for misuse.

Made with ❤️ by AmirhosseinG
