# ethical-hacking-assignment-2
This repository contains report for ethical hacking in the isolated virtual environment for learning and report generation purpose only.
Assignment-2
Penetration Testing Report (SME - LAB)
Target Environment
I have created a simulated SME environment using vulnerable virtual machines from TryHackMe, Vulnhub, and other sources:
Machines:
o	Kali-Linux: Attack-Box,
o	Blue: Winows-7 Host
o	Server: Metasploitable2
Isolated Virtual NAT Network: I have created a small, isolated network for this lab, here is the network IP range.
o	AssNet – 10.0.22.0/24
1. Reconnaissance and Target Analysis
1.1 Network Discovery
•	Tool Used: 
o	netdiscover
•	Command:
o	netdiscover -r 10.0.22.0/24

Result:
•	Detected 3 active hosts: 
o	10.10.10.3 – Kali-Linux (Attack-Box)
o	10.10.10.5 – Windows 7 (TryHackMe: Blue)
o	10.10.10.6 – Linux Server (Metasploitable2)


1.2 Port Scanning For Server IP – 10.0.22.6
•	Command:
o	nmap -p- -sV -oN Server.txt 10.0.22.6

Result:

1.3 Vulnerability Analysis
•	Tools Used: searchsploit, nikto, enum4linux
•	CVEs found: 
o	SMBv1 RCE (EternalBlue - CVE-2017-0144)
o	Default web app credentials on Overpass
📸 [Insert screenshots of scan results here]
________________________________________
🧨 2. Exploitation
2.1 Target: Blue (10.10.10.5)
•	Exploit Used: EternalBlue via Metasploit
•	Commands:
•	bash
•	CopyEdit
•	use exploit/windows/smb/ms17_010_eternalblue
•	set RHOST 10.10.10.5
•	run
•	
✅ Result:
•	Reverse shell obtained as NT AUTHORITY\\SYSTEM
📸 [Screenshot of Metasploit session]
2.2 Target: Overpass (10.10.10.6)
•	Exploit Used: Credential reuse & SSH login
•	Process: 
o	Extracted credentials from /etc/passwd
o	Logged in via SSH using ssh johndoe@10.10.10.6
📸 [Screenshot of shell access]
________________________________________
🧬 3. Post-Exploitation
Blue:
•	Checked for privilege escalation vectors
•	Extracted password hashes with mimikatz
Overpass:
•	Gained root using sudo -l trick
•	Read /etc/shadow, uploaded a backdoor
📁 Files accessed:
•	C:\\Users\\Administrator\\Desktop\\secrets.txt
•	/var/www/html/config.php
📸 [Screenshots of whoami, ls, cat]
________________________________________
🛡️ 4. Recommendations
Vulnerability	Recommendation
SMBv1 enabled	Disable SMBv1 protocol; upgrade to SMBv3
Outdated OS	Migrate from Windows 7 to a supported version
Default credentials	Enforce strong password policy, use MFA
SSH brute-forceable	Restrict SSH access to internal IPs only
________________________________________
📌 5. Conclusion
•	Successful exploitation of multiple machines using real-world techniques.
•	Demonstrated post-exploitation and privilege escalation.
•	All steps documented with screenshots.
Alternative Approaches:
•	Could have used crackmapexec for automated enumeration
•	Web applications could have been fuzzed with Burp Suite

