# Recon Pipeline – Ultimate Automated Recon Tool

A fully automated, real-time, beautiful web-based reconnaissance pipeline built with Flask + Socket.IO.
Performs real tool chaining (no fake progress bars):

Subfinder → DNSx → TLSx → Nmap → Nuclei → FFUF

All results saved as pretty JSON, logs in recon.log, final results downloadable as .zip.

100% offline – no CDN, no Cloudflare, no external dependencies.

**Features**

Real-time progress with live updates via WebSocket

Beautiful dark-themed UI (fully offline)

Real subdomain enumeration & live host resolution

HTTPS detection, port scanning, vulnerability scanning, directory brute-force

Smart host chaining (only live hosts passed to next tool)

Pretty JSON output for every stage

Download all results as a single .zip

Simple login protection

Full logging to recon.log

Zero "Not secure" warnings (no external CDN)


**Tools Used (must be in PATH)**
Make sure these tools are installed and accessible:

subfinder

dnsx

tlsx

nmap

nuclei

ffuf

Install them easily:

# ProjectDiscovery tools
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest

go install -v github.com/projectdiscovery/dnsx/cmd/dnsx@latest

go install -v github.com/projectdiscovery/tlsx/cmd/tlsx@latest

go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest


# FFUF
go install -v github.com/ffuf/ffuf/v2@latest

# nmap (via package manager)
sudo apt install nmap -y

Tip: Move binaries to ~/go/bin/ and add to PATH:

export PATH=$PATH:~/go/bin

Installation & Usage


# 1. Clone the repo
git clone https://github.com/yourusername/recon-pipeline.git
cd recon-pipeline

# 2. Install Python dependencies
pip3 install flask flask-socketio

# 3. Run the app
python3 app.py

Open browser: http://YOUR_IP:5000

Default credentials:

Username: administrator
Password: Qwer12#$

Output Structure

All scans saved in scans/ folder:

scans/
 └── 20251202_153045/
     ├── live_hosts.txt
     ├── subfinder.txt
     ├── subfinder.json
     ├── dnsx.json
     ├── tlsx.json
     ├── nmap.xml
     ├── nuclei.json
     ├── ffuf_example.com.json
     ├── wordlist.txt
     └── summary.json


Contributing

Pull requests are welcome! Especially for:

Adding Amass, Httpx, Katana support

Better error handling

Rate limiting / concurrency controls

Dark/light mode toggle

Export to Markdown/HTML report
