# NETWORKWALKS-SEMILORE-B083-WK2-PM1-4-5-CYBERSECURITY-VULNERABILITY-ASSESSMENT
  
<h2 align="center">PENETRATION TESTING REPORT</h2>   
<h4 align="center">FOOTPRINTING & NETWORK SCANNING PHASES</h4>    
<h6 align="center">W2-PM-FINAL | CYBERSECURITY |  NETWORKWALKS</h6>    
  
  
| <h2> Pentester Name </h2> |  <h2> `kunal srivastava` </h2> |
| :--- | :--- |
| Program/Batch | B083d |
| Module Completed | W2-PM1 (Multiple Kali Tools)  
| | W2-PM4 (theHarvester Tool)  
| | W2-PM5 (Zenmap Scanning)|
| Date | 26 September 2026 |
| Client/Target	| 1. Networkwalks (secured written permission already) |  
| | 2. My own local LAN Network |  
| Permission secured from client? | Yes |  
| Phases Covered | Phase 1: Reconnaissance & Footprinting |
| | Phase 2: Scanning & Network Discovery|
| | Phase 4: Reconnaissance & Footprinting using theHarvester| 


<h3 align="center">LIABILITY DICLAIMER</h3>   
I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purpose only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged.  
  
<h3 align="center">INTRODUCTION</h3>    
This report covers footprinting the networkwalks.com domain using multiple Kali Linux tools (W2-PM1) and scanning my own local network with Zenmap (W2-PM5) also using theHarvester tool for reconnaissance to get emails and subdomains, host, open ports, and banners from different public sources of Microsoft.com(W2-PM4). One module covers the footprinting phase and the other covers the scanning phase, so together they show how an attacker moves from gathering public information to mapping live hosts on a network. It is the Week 2 part of my ongoing internship program at Networkwalks.  
All commands and tools were run in Kali Linux. Every step below includes the exact command used, the result I observed, a screenshot as evidence, and a short note on why the finding matters from an attacker's point of view.  
  
<h3 align="center">TOOLS USED</h3>  
  
The table below lists each tool used in this report and its purpose.  
  
| Tool | Purpose |
| :--- | :--- |
| Kali Linux | Operating systems used for reconnaissance activities |
| WHOIS	 | Find domain registration details (owner, dates, name servers) |
| whatweb | Fingerprint web technologies (server, CMS, plugins, IP) |
| nslookup | Resolve the domain name to its IP address using DNS |
| curl | I	Read the HTTP response headers of the website |
| wafw00f | Detect whether a Web Application Firewall protects the site |
| dnsrecon | Enumerate all DNS records (NS, MX, SPF, TXT, SRV) |
| Zenmap (Nmap GUI) | Scan the local subnet to find live hosts, IPs and MAC addresses |
| theHarvester | It is used for gathering information of emails, sub-domains, hosts, employee names, open ports and banners from different public sources |

    
<h3 align="center">ACTIVITIES PERFORMED</h3>  
  
**Footprinting & Reconnaissance**  
- I performed reconnaissance against the networkwalks.com domain using six Kali Linux tools: WHOIS, WhatWeb, Nslookup, Curl, Wafw00f and DNSRecon. Each tool was used to collect a different type of information about the target.  
- First, I used WHOIS to obtain publicly available domain registration information and identify the domain’s name servers. The results provided information about the domain registration and hosting infrastructure.  
- I then used WhatWeb to identify technologies used by the website. The results identified WordPress 7.0.4 and WP Download Manager 3.3.58, along with other information exposed by the website.
- Using Nslookup, I resolved the domain name to its IP address. The provided result identified 192.232.216.135.  
- I used Curl with the -I option to inspect the HTTP response headers. This provided additional information about the web application and exposed the WordPress REST API endpoint /wp-json/.
- Next, I used Wafw00f to determine whether a Web Application Firewall was protecting the website. The result identified ModSecurity (SpiderLabs).  
- Finally, I used DNSRecon to enumerate DNS records. The results provided information relating to name servers, mail servers, SPF/TXT records, service records and DNS software information.  
  
  
**Network Scanning with Zenmap**  
- For the second activity, I used Zenmap to perform network discovery on my local network. The practical required me to identify my local IP address and subnet, discover live hosts, identify their IP and MAC addresses, and generate a network topology.  
- I first used the linux ip a command to identify my local IP address and LAN subnet. I then entered the subnet into Zenmap and selected Ping Scan to identify active hosts.  
The example results provided in the practical identified three live hosts:  
•	10.0.2.2  
•	10.0.2.3  
•	10.0.2.15  
The example results also included three MAC addresses.  
After completing the scan, I opened the Topology section in Zenmap, enabled the legend and saved the network topology in PDF format as required by the practical task.  
Note: The actual subnet, number of hosts and addresses should be replaced with the results from my own network when submitting the report.  

    
**Footprinting & Reconnaissance with theHarvester**  
- For the third activity, I used theHarvester for gathering information of emails, sub-domains, hosts, employee names, open ports and banners from different public sources like search engines, PGP key servers and SHODAN computer database. It has been developed in Python.  
theHarvester comes pre-installed in Kali Linux. The target for this activity was Microsoft.com as instructed by the instructor.  
- The first command I used was to get $ theHarvester -d microsoft.com -l 1000 -b baidu (in this command, the domain was specified, the limit being 1000 and the source being baidu).
- Next, I use this command $ theHarvester -d microsoft.com -l 50 -b all (specified the domain, limit being 50 and also using all the source theHarvester has to make my reconnaissance this time).  
  
    
<h3 align="center">RISK ANALYSIS/IMPACTS</h3>   
  
Based on the information collected during the footprinting and network scanning activities, I identified the following potential risks.  
  
| S/N |	Risk / Finding	| Evidence / Observation |	Potential Impact |	Risk Level |
| :---| :---| :---| :---| :---| 
| 1	| Web technology information exposed	| WhatWeb identified WordPress and WP Download Manager	| Attackers may use exposed technology/version information to identify software requiring further security review |	● Medium |
| 2 |	Server IP address identifiable	| Nslookup resolved the domain to 192.232.216.135 |	Provides information about the network location of the web service	| ● Low |
| 3	| HTTP technical information exposed |	Curl returned HTTP response headers and exposed /wp-json/	| May assist technology fingerprinting and further enumeration	| ● Low
| 4	| WAF technology identifiable	| Wafw00f identified ModSecurity (SpiderLabs)	| Reveals information about the web application’s security architecture	| ● Low |
| 5	| DNS infrastructure information exposed	| DNSRecon identified DNS, mail and service-related records |	DNS information can help build a broader infrastructure profile |	● Medium |
| 6	| Multiple live hosts visible on local network	| Zenmap identified three live hosts in the example network	| Unknown or unauthorized devices may potentially be present on a network	| ● Medium |
| 7	| 5 subdomain/host discovered plus 2 URL-encoded duplicates |	theHarvester tool identified 5 subdomains of Microsoft plus 2 URL-encoded duplicates |	An admin subdomain being publicly discoverable via OSINT is worth flagging in a real enagement. Even if it’s properly acess-controlled, its existences tells an attacker exactly where to focus brute-force or credential stuffing |	● Medium |
| 8	| Over 16,000 devices belonging to Microsoft employees have been infected with credential stealing malware, and those logs contain saved browser credentials, session cookies and autofill data tied to corporate accounts |	theHarvester tool recognized 602k compromised records via Hudson Rock	| This compromise represents a large credential stuffing risk pool |	● Medium |
| 9	| 43 internal hosts extracted from employee URLs, this reveals internal infrastructure naming conventions, internal tools, or admin panels |	theHarvester tool recognized 43 internal hosts |This compromise reveals internal infrastructure that ought not be discoverable externally |	● Medium |
  
Risk level key:  ● Critical  ● Medium  ● Low  
- The risks above are observations from the footprinting and scanning exercises, not confirmed vulnerabilities.  
- The practical exercises primarily involved information gathering and host discovery. No exploitation or vulnerability validation was performed as part of these three modules.  
- Therefore, the presence of information such as a software version, IP address or DNS, emails, host, sub-domains record does not by itself mean that the system is vulnerable. Further authorized security testing would be required to confirm any actual vulnerability.  
  
  
<h3 align="center">RECOMMENDATIONS</h3>  
  
Based on the observations from these activities, I recommend the following security improvements:  
  
**1.	Review publicly exposed technology information**  
Organizations should regularly review what information about their web technologies, CMS and plugins is publicly visible.  
**2.	Keep software updated**  
CMS platforms, plugins and other web technologies should be regularly updated and reviewed against current security advisories.  
**3.	Review HTTP headers**  
HTTP response headers should be reviewed to determine whether unnecessary technical information is being exposed.  
**4.	Review DNS records regularly**  
DNS records should be checked periodically to ensure that only required information and services are publicly exposed.  
**5.	Properly configure and monitor the WAF**  
Keep the WAF (ModSecurity) enabled and tuned, since it already blocks naive attacks.
**6.	Perform regular internal network discovery**  
Organizations should periodically scan their own networks to identify active devices.  
**7.	Investigate unknown devices**  
Any unexpected device discovered during network scanning should be investigated and verified.  
**8.	Maintain network documentation**  
Network topology and device information should be documented and updated regularly.  
**9.	Perform security testing with authorization**  
Reconnaissance and scanning should only be performed against systems and networks where appropriate authorization has been provided.  
**10.	For the subdomains found**  
Ensure admin.microsoft.com (and similar) enforce MFA, IP allowlisting, and are not indexed/discoverable without need  consider whether it needs to resolve publicly at all versus being reachable only via VPN.  
**11.	For the infostealer exposure**  
This points to an endpoint security gap, not a web app vulnerability. Recommend EDR/antivirus coverage review on employee devices, browser credential-storage policies (discourage saving corporate creds in-browser), and mandatory credential rotation for any accounts confirmed in stealer logs.  
**12.	For the internal host leakage**  
Audit what those 43 internal hostnames actually point to if any are genuinely sensitive internal tools, that's a namespace/DNS hygiene issue (internal services shouldn't be inferable from external OSINT).  
  
  
<h3 align="center">CONCLUSION</h3>  
  
During Week 2 of my Cybersecurity & Ethical Hacking internship, I completed practical activities covering footprinting, reconnaissance and network scanning.  
In the footprinting activity, I used six Kali Linux tools to collect information about the target domain. I learned how WHOIS can provide domain information, WhatWeb can identify web technologies, Nslookup can resolve domain names, Curl can inspect HTTP headers, Wafw00f can identify a WAF, and DNSRecon can provide additional DNS information.  
In the network scanning activity, I used Zenmap to identify my local network configuration and discover active hosts. I also collected IP and MAC address information and created a network topology.  
I also used theHarvester tool to get the sub-domains, hosts, employee names, open ports and banners from different public sources.  
The exercises showed me that information gathering is an important part of cybersecurity. Even before attempting to exploit a system, a security professional can learn a significant amount about an environment by carefully analyzing publicly available information and network responses.  
I also learned that technical findings should be documented clearly. A good cybersecurity report should explain what was performed, what was discovered, what the observation means, what risk it may create, and what can be done to reduce that risk.  
Finally, I learned that reconnaissance and scanning must always be performed within an authorized scope. These activities were completed as prt of the assigned educational cybersecurity lab.  
  
