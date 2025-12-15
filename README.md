Recon Pipeline

Ultimate Automated Reconnaissance Framework

Recon Pipeline is a fully automated, real-time, web-based reconnaissance framework built with Flask + Socket.IO. It performs true tool chaining (no simulated progress) and provides a fully offline, dark-themed UI for end-to-end reconnaissance.

The framework orchestrates industry-standard tools in a smart, dependency-aware pipeline, ensuring that only validated targets are passed to subsequent stages.

Recon Pipeline Flow
Subfinder
   ↓
DNSx
   ↓
HTTPX        (HTTP/S probing, status, title, tech)
   ↓
TLSx         (TLS & certificate inspection)
   ↓
Nmap         (Port & service scanning)
   ↓
Nuclei       (Vulnerability scanning)
   ↓
FFUF         (Directory + Virtual Host brute-force)


Only live, reachable hosts progress through the pipeline.

Key Features

Real-time progress with live WebSocket updates

Fully offline, dark-themed web UI

Passive subdomain enumeration and live DNS resolution

HTTP/S probing with metadata collection

TLS and certificate inspection

Port scanning and service fingerprinting

Vulnerability scanning using Nuclei templates

Directory and virtual host enumeration

Smart host chaining (no wasted scans)

Pretty JSON output for every stage

Download all results as a single ZIP archive

Simple login protection

Full execution logging to recon.log

No CDN, no external JS/CSS, no Cloudflare

Tools Used (Complete & Accurate)
Core Reconnaissance Tools

All tools must be installed and available in PATH

Subfinder – Passive subdomain enumeration

DNSx – DNS resolution and live host discovery

HTTPX – HTTP/S probing, status codes, titles, technologies

TLSx – TLS support and certificate analysis

Nmap – Port scanning and service detection

Nuclei – Template-based vulnerability scanning

FFUF – Directory fuzzing and virtual host enumeration

Supporting Technologies

Python 3 – Orchestration, execution control, parsing

Flask – Web backend

Flask-SocketIO – Real-time WebSocket updates

Go – Runtime for ProjectDiscovery tools and FFUF

JSON – Structured output format

ZIP utilities – Result packaging

Linux shell utilities – Process execution and piping

Installation
1. Clone the Repository
git clone https://github.com/amirhosseing/recon-pipeline.git
cd recon-pipeline

2. Install Recon Tools
ProjectDiscovery Tools
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
go install -v github.com/projectdiscovery/dnsx/cmd/dnsx@latest
go install -v github.com/projectdiscovery/httpx/cmd/httpx@latest
go install -v github.com/projectdiscovery/tlsx/cmd/tlsx@latest
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest

FFUF
go install -v github.com/ffuf/ffuf/v2@latest

Nmap
sudo apt install nmap -y

Add Go Binaries to PATH
export PATH=$PATH:~/go/bin

3. Install Python Dependencies
pip3 install flask flask-socketio

Running the Application
python3 app.py


Open your browser:

http://YOUR_IP:5000

Default Credentials
Username: administrator
Password: Qwer12#$


Change these credentials before any production or shared use.

Virtual Host Scanning (Example)

Recon Pipeline performs virtual host discovery using FFUF with the Host header against shared IPs.

Example Command
ffuf \
  -u http://180.140.0.1 \
  -H "Host: FUZZ.x.com" \
  -w wordlist.txt \
  -ac \
  -of json \
  -o ffuf_vhost_x.json

Example Result (Excerpt)
{
  "host": "payment.x.ir",
  "status": 200,
  "content-type": "text/html; charset=utf-8",
  "length": 8248
}


This technique uncovers:

Hidden subdomains behind shared IPs

Misconfigured reverse proxies

Internal or staging services

Sample HTTPX JSON Output
{
  "input": "https://c.com",
  "url": "https://x.com",
  "status_code": 200,
  "title": "x | Payment",
  "scheme": "https",
  "port": "443",
  "webserver": "nginx",
  "content_type": "text/html; charset=utf-8",
  "tech": [
    "Nginx",
    "React",
    "HTTP/2"
  ],
  "tls": true
}


HTTPX output is used to:

Filter live web services

Identify HTTPS support

Feed validated targets into TLSx, Nmap, and Nuclei

Output Structure

All results are saved under the scans/ directory:

scans/

    ├── subfinder.txt
    ├── subfinder.json
    ├── dnsx.json
    ├── httpx.json
    ├── tlsx.json
    ├── nmap.xml
    ├── nuclei.json
    ├── ffuf_example.com.json
    ├── wordlist.txt
    ├── live_hosts.txt
    └── summary.json


Each phase produces machine-readable, auditable output.

Contributing

Pull requests are welcome, especially for:

Adding Amass, Katana, or Httpx enhancements

Improved error handling and retries

Rate limiting and concurrency controls

Dark / light theme toggle

Markdown / HTML report generation

Disclaimer

This project is intended only for authorized security testing and research.
The user is responsible for complying with all applicable laws and regulations.
