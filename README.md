**Ethical Hacking & Network Security Lab Portfolio**

A hands-on security lab portfolio demonstrating practical skills in network reconnaissance, vulnerability exploitation, and web application security testing. All work was conducted in isolated, controlled virtual environments for educational purposes.


📁**Repository Structure**

├── 01-reconnaissance/
│   └── Nmap port scanning, NSE scripts, SSL/TLS analysis, technology fingerprinting

├── 02-network-exploitation/
│   └── Metasploit-based exploitation, post-exploitation analysis, executive pentest report

├── 03-web-application-security/
│   └── SQL Injection vulnerability assessment on DVWA


🧪 **Lab Environment**

ComponentDetailsAttacker MachineKali Linux (64-bit VM)Target MachineMetasploitable 2 / Real-world bug bounty targetVirtualisationVMware Workstation / VirtualBoxNetworkIsolated NAT/Host-only virtual network


📂 **Lab 01 — Network Reconnaissance**

Target: luno.com (via Bugcrowd bug bounty programme — in-scope assets only)

Tools Used: Nmap, Nmap NSE Scripts, Wappalyzer

**What was done:**

Performed IP resolution and port scanning using nmap -sV -Pn

Identified open ports and confirmed Cloudflare proxy infrastructure

Ran ssl-enum-ciphers NSE script on port 443 to analyse TLS configuration

Used Wappalyzer to fingerprint the technology stack (React, HTTP/2, Cloudflare Bot Management, HSTS)

Researched CVEs relevant to the detected stack including CVE-2025-55182 (React RCE, CVSS 10.0) and CVE-2023-44487 (HTTP/2 Rapid Reset DDoS)


**Key Findings:**

Target uses Cloudflare CDN — origin IP hidden, attack surface minimised

TLS 1.2 and TLS 1.3 supported with all-A grade cipher suites and Perfect Forward Secrecy (PFS)

996 filtered ports confirm active firewall rules

📂 **Lab 02 — Network Exploitation & Penetration Test**

Target: Metasploitable 2 (192.168.74.129) — isolated lab environment

Tools Used: Metasploit Framework, Nmap


**What was done:**

Conducted service version detection scan (nmap -sV -Pn) identifying 20+ open ports

Identified critical vulnerability: VSFTPD v2.3.4 backdoor (CVE-2011-2523)

Exploited backdoor using exploit/unix/ftp/vsftpd_234_backdoor Metasploit module

Gained unauthenticated root shell (uid=0, gid=0) on the target system

Documented full attack chain in both a technical report and a professional executive summary report


**Attack Chain:**

Reconnaissance (Nmap) → Vulnerability Identification (VSFTPD v2.3.4) 

→ Exploitation (Metasploit) → Root Access → Post-Exploitation Verification

**Key Findings:**

CVE-2011-2523 allows unauthenticated RCE via malformed FTP username sequence

Root access confirmed via whoami, hostname, ifconfig

Overall risk rating: Critical


**Remediation Recommended:**

Decommission VSFTPD v2.3.4 — replace with SFTP

Enforce strict patch management policy

Apply principle of least privilege for all running services

Deploy continuous vulnerability scanning (Nessus / OpenVAS)



📂 **Lab 03 — Web Application Security: SQL Injection**

Target: DVWA (Damn Vulnerable Web Application) on Metasploitable 2 (192.168.56.101)

Tools Used: Nmap, Firefox, Metasploitable 2

**What was done:**

Identified Port 80 running Apache via Nmap service scan

Accessed DVWA and confirmed SQL Injection vulnerability by triggering a MySQL error

Injected ' OR '1'='1 payload to bypass authentication logic

Successfully extracted all user records from the backend database

Documented risk analysis and remediation recommendations


**Key Findings:**


Application passes user input directly to SQL queries without sanitisation

Authentication bypass and full data extraction achieved with a basic payload

Risk rating: Critical


**Remediation Recommended:**

Implement prepared statements (parameterised queries)

Apply input validation and whitelisting

Enforce least-privilege database user permissions



🛠️ **Tools & Technologies**

Kali Linux Metasploit Framework Nmap Nmap NSE Scripts Wappalyzer VMware VirtualBox DVWA Bugcrowd


⚠️ **Disclaimer**

All security testing documented in this portfolio was conducted exclusively within isolated, controlled virtual lab environments or against authorised targets via a public bug bounty programme (Bugcrowd). No unauthorised systems were accessed at any point. This work is intended solely for educational and portfolio purposes.
