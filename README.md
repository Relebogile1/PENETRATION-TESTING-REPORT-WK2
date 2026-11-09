PENETRATION TESTING REPORT

Footprinting & Network Scanning Phases

Project: W2-PM-FINAL | Cybersecurity | Networkwalks
Program: Cybersecurity & Ethical Hacking Internship

---

👤 Author Information

Field| Details
Pentester Name| Relebogile Majatladi
Program / Batch| B084 – Networkwalks
Date| 9 November 2026
Modules Completed| W2-PM1 (Multiple Kali Tools), W2-PM5 (Zenmap Scanning)
Client / Target| Networkwalks and my own local LAN
Written Permission| Yes
Phases Covered| Phase 1: Reconnaissance & Footprinting; Phase 2: Scanning & Network Discovery
Remaining Phases| Phases 3–5: In Progress

---

⚠️ 1. Liability Disclaimer

All activities documented in this report were performed only on systems and devices for which I had secured written permission or that I personally own.

This project is intended strictly for educational and research purposes. The knowledge and techniques demonstrated must not be used for unauthorized access or illegal activities.

The instructor, authors, and Networkwalks are not responsible for any misuse of the information provided. All actions taken using this knowledge remain the responsibility of the individual.

Unauthorized access to computer systems is a criminal offence in many jurisdictions, even when no damage occurs.

---

📖 2. Introduction

This report documents the practical cybersecurity activities completed during Week 2 of my Cybersecurity and Ethical Hacking internship at Networkwalks.

The practical work focused on two important stages of penetration testing:

1. Footprinting and Reconnaissance: Gathering publicly available information about the "networkwalks.com" domain using multiple Kali Linux tools (W2-PM1).
2. Scanning and Network Discovery: Identifying active devices on my own local network using Zenmap (W2-PM5).

These activities demonstrate how a security professional can move from collecting publicly available information to identifying active devices within an authorized network.

All commands were executed using Kali Linux for footprinting and a Windows PC with Zenmap installed for network scanning.

Each activity includes the command used, observations, findings, and supporting screenshots as evidence.

---

🛠️ 3. Tools Used

Tool| Purpose
Kali Linux| Operating system used for reconnaissance
Windows| Operating system used for local network scanning
WHOIS| Retrieves domain registration information and name servers
WhatWeb| Identifies website technologies, CMS platforms, and plugins
Nslookup| Resolves domain names into IP addresses
Curl| Retrieves HTTP response headers
Wafw00f| Identifies Web Application Firewall technologies
DNSRecon| Enumerates DNS records
Zenmap| Graphical interface for Nmap network scanning
Windows CMD| Identifies local IP and MAC address information

---

🔍 4. Activities Performed

4.1 Footprinting & Reconnaissance

I performed reconnaissance against the "networkwalks.com" domain using six Kali Linux tools. Each tool helped me collect a different type of information about the target.

1. WHOIS – Domain Information

Command:

whois networkwalks.com

Findings:

- Domain expiry date: "2027-11-06T22:51:46Z"
- Name server 1: "NS6135.HOSTGATOR.COM"
- Name server 2: "NS6136.HOSTGATOR.COM"

Observation:

WHOIS provided publicly available domain registration information and details about the domain's name servers.

Security relevance:

This information helps build an initial profile of the target's domain and hosting infrastructure.

2. WhatWeb – Website Technology Fingerprinting

Command:

whatweb networkwalks.com

Findings:

- Apache
- Bootstrap 7.0.4
- WordPress 7.0.4
- WP Download Manager 3.3.58

Observation:

WhatWeb identified technologies and software components used by the website.

Security relevance:

Technology fingerprinting helps security professionals identify software that may require further security review and update checks.

3. Nslookup – DNS Resolution

Command:

nslookup networkwalks.com

Finding:

- Resolved IP address: "192.232.216.135"

Observation:

The command successfully resolved the domain name to its associated IP address.

Security relevance:

DNS resolution helps identify the server address associated with a website.

4. Curl – HTTP Response Headers

Command:

curl -I https://networkwalks.com

Findings:

- Retrieved HTTP response headers.
- Identified the WordPress REST API endpoint: "/wp-json/".

Observation:

Curl provided information about the website's HTTP response and exposed additional technical details.

Security relevance:

HTTP headers and exposed endpoints can provide useful information during web application reconnaissance.

5. Wafw00f – Web Application Firewall Detection

Command:

wafw00f networkwalks.com

Finding:

- Detected Web Application Firewall: ModSecurity (SpiderLabs).

Observation:

The tool identified ModSecurity as the Web Application Firewall protecting the website.

Security relevance:

Identifying a WAF helps security professionals understand the security controls protecting a web application.

6. DNSRecon – DNS Enumeration

Command:

dnsrecon -d networkwalks.com

Findings:

- SOA: "ns6135.hostgator.com"
- NS: "50.87.144.87", "192.232.216.131"
- MX: "mail.networkwalks.com" / "192.232.216.135"
- A record: "192.232.216.135"
- TXT: SPF records
- SRV: Autodiscover records ("184.94.203.x")

Observation:

DNSRecon collected different DNS records associated with the target domain, including name server, mail exchange, text, and service records.

Security relevance:

DNS enumeration provides a broader understanding of an organization's publicly exposed DNS infrastructure.

---

4.2 Network Scanning with Zenmap

For the second practical activity, I used Zenmap to perform network discovery on my own local network.

Step 1: Identify Local Network Configuration

I opened Windows Command Prompt and executed:

ipconfig

Findings:

- Local IP address: "192.168.1.191"
- Network subnet: "192.168.1.0/24"

Step 2: Perform Network Discovery

I entered the subnet "192.168.1.0/24" into Zenmap and selected the Ping Scan option to identify active hosts on the local network.

Step 3: Scan Results

The scan successfully identified four live hosts:

IP Address| Device Information
192.168.1.1| Network gateway
192.168.1.20| Discovered host
192.168.1.191| My local PC
192.168.1.248| Discovered host

MAC Address Information:

IP Address| MAC Address / Vendor
192.168.1.1| D4:0D:AB:2E:E0:02 – Shenzhen Cudy Technology
192.168.1.20| BA:12:46:78:D8:B6
192.168.1.248| 46:F5:BB:99:6A:2F

Step 4: Network Topology

After completing the scan, I opened the Topology section in Zenmap, enabled the legend, and exported the network topology into a PDF file named "Topology.pdf", as required by the practical task.

Observation:

Zenmap successfully identified active hosts on my local subnet and provided information that helped me understand how devices are connected within a network.

---

⚠️ 5. Risk Analysis & Impact

Based on the information collected during the footprinting and network scanning activities, I identified the following potential security considerations.

No.| Risk / Finding| Evidence / Observation| Potential Impact| Risk Level
1| Web technology information exposed| WhatWeb identified WordPress and WP Download Manager| Could help attackers identify software requiring further security review| Medium
2| Server IP address identifiable| Nslookup resolved the domain to 192.232.216.135| Provides information about the network location of the web service| Low
3| HTTP technical information exposed| Curl retrieved response headers and identified "/wp-json/"| May assist further technology fingerprinting and enumeration| Low
4| WAF technology identifiable| Wafw00f identified ModSecurity| Reveals information about the website's security architecture| Low
5| DNS infrastructure information exposed| DNSRecon identified DNS, mail, and service-related records| Helps build a broader infrastructure profile| Medium
6| Multiple live hosts visible| Zenmap identified four live hosts on the local subnet| Unknown devices may introduce security risks if not properly managed| Medium

Risk Level Key:

- 🔴 Critical
- 🟠 Medium
- 🟢 Low

Important Note:

The findings above represent observations from the footprinting and scanning exercises. They are not confirmed vulnerabilities.

No exploitation or vulnerability validation was performed during these two modules. The presence of software version information, an IP address, or DNS records does not automatically mean that a system is vulnerable.

Further authorized security testing would be required to confirm any actual vulnerabilities.

---

🛡️ 6. Security Recommendations

Based on the observations made during the practical exercises, I recommend the following security improvements:

1. Review Publicly Exposed Technology Information: Organizations should regularly review the technical information exposed by their websites, CMS platforms, and plugins.

2. Keep Software Updated: CMS platforms, plugins, and other web technologies should be updated regularly and checked against relevant security advisories.

3. Review HTTP Headers: HTTP response headers should be reviewed to identify and minimize unnecessary technical information disclosure.

4. Review DNS Records: DNS records should be checked periodically to ensure that only required information and services are publicly exposed.

5. Configure and Monitor the WAF: ModSecurity should remain properly configured, updated, and monitored to help protect web applications against malicious requests.

6. Perform Regular Network Discovery: Organizations should periodically scan their internal networks to identify active devices.

7. Investigate Unknown Devices: Unexpected devices discovered during network scanning should be investigated and verified.

8. Maintain Network Documentation: Network topology, IP addresses, and device information should be documented and updated regularly.

9. Conduct Authorized Security Testing: All reconnaissance, scanning, and penetration-testing activities should be performed within an approved scope and with appropriate authorization.

---

🎯 7. Conclusion

During Week 2 of my Cybersecurity and Ethical Hacking internship at Networkwalks, I completed practical activities covering footprinting, reconnaissance, and network scanning.

In the footprinting activity, I used six Kali Linux tools to gather information about a target domain. I learned how WHOIS retrieves domain registration information, WhatWeb identifies website technologies, Nslookup resolves domain names, Curl inspects HTTP response headers, Wafw00f detects Web Application Firewalls, and DNSRecon enumerates DNS records.

In the network scanning activity, I used Zenmap to identify my local network configuration and discover active hosts. I also collected IP and MAC address information and generated a network topology.

These practical exercises helped me understand that information gathering is an important part of cybersecurity. Before attempting to exploit a system, security professionals can learn a great deal about an environment by carefully analyzing publicly available information and network responses.

I also learned the importance of documenting technical findings clearly, understanding potential risks, and recommending appropriate security improvements.

Most importantly, these activities reinforced the importance of ethical hacking, responsible security testing, and obtaining authorization before performing any security assessment.

Week 2 has strengthened my practical understanding of reconnaissance and network discovery as I continue developing my cybersecurity skills.

---

📸 8. Evidence & Screenshots

The following screenshots and supporting files provide evidence of the practical activities completed.

8.1 WHOIS Reconnaissance Output

Command: "whois networkwalks.com"

<!-- Add your WHOIS screenshot here -->8.2 WhatWeb Technology Fingerprinting Output

Command: "whatweb networkwalks.com"

<!-- Add your WhatWeb screenshot here -->8.3 Nslookup DNS Resolution Output

Command: "nslookup networkwalks.com"

<!-- Add your Nslookup screenshot here -->8.4 Curl HTTP Response Headers Output

Command: "curl -I https://networkwalks.com"

<!-- Add your Curl screenshot here -->8.5 Wafw00f WAF Detection Output

Command: "wafw00f networkwalks.com"

<!-- Add your Wafw00f screenshot here -->8.6 DNSRecon Enumeration Output

Command: "dnsrecon -d networkwalks.com"

Target: "192.168.1.0/24"

Result: Four live hosts discovered.

---

📌 9. Project Information

Field| Details
Program| Cybersecurity Program – Networkwalks
Week| 02
Task| W2-PM-FINAL
Batch| B084
Repository| GitHub
Status| Phases 1 and 5 completed; Phases 2–4 in progress

---

👩‍💻 Author

Relebogile Majatladi
Cybersecurity Professional | Networkwalks – Batch B084

LinkedIn: https://www.linkedin.com/in/bethuel-ntsetse-majatladi-48a62524a?

---

End of Report

Learning. Practising. Securing. Growing in Cybersecurity.
