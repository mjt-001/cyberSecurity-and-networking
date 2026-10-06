# Threats, Vulnerabilties, and Mitigations

## Objective 2.1: `Threat Actors and Motivations`

### Overview & Mechanics
In cybersecurity risk management, a **threat actor** (or malicious actor) is an individual, group, or entity that executes or facilitates actions causing security incidents that negatively affect the confidentiality, integrity, or availability of systems, networks, and data. Understanding the nature, capabilities, structural origin, and intent of a threat actor is vital for network engineers and security administrators. It allows organizations to contextualize attacks, perform accurate threat modeling, implement targeted defensive controls, and determine attribution during incident response.

Threat actors do not possess uniform capabilities or objectives. They vary widely across several defining attributes, including their operational location relative to the target, financial backing, and technical sophistication. By evaluating these baseline attributes alongside the actor's primary motivation, security teams can anticipate tactics, techniques, and procedures (TTPs) used throughout an attack lifecycle.

#### Security Implications
1. **Confidentiality:** Threat actors frequently target sensitive assets—such as personally identifiable information (PII), intellectual property (IP), financial records, or state secrets - resulting in unauthorized disclosure, corporate espionage, and regulatory non-compliance through data exfiltration.
2. **Integrity:** Malicious actors alter, corrupt, or destroy system files, source code, database records, and operational configurations, leading to unauthorized system modifications, compromised data trust, website defacement, or physical hardware destruction (e.g., centrifuges or industrial control equipment).
3. **Availability:** Threat actors intentionally disrupt business operations, critical infrastructure, and network access using denial-of-service (DoS/DDoS) attacks, wiper malware, or widespread encryption via ransomware, rendering critical systems inaccessible to legitimate users.

### A. Attributes of Threat Actors

CompTIA Security+ classifies threat actors using three key attributes. Evaluating these attributes provides actionable intelligence regarding the level of risk a specific actor poses to an enterprise environment.

#### 1. Internal vs. External (Location)
* **External Actors:** Operate entirely outside the organizational security boundary. They must discover and exploit external exposure points, such as public-facing web applications, open firewall ports, edge routers, or vulnerable remote access mechanisms (e.g., VPNs). They frequently utilize spear-phishing or credential harvesting to establish an initial foothold.
* **Internal Actors:** Operate inside the physical and logical security perimeter. They possess existing network access, employee credentials, or physical admittance to facility assets. Because they already operate within the trusted zone, internal actors present significant challenges to traditional boundary defenses and often bypass initial perimeter controls entirely.

#### 2. Resources and Funding
* **Limited / No Funding:** Individual actors or unsophisticated attackers operating on personal budgets with open-source, freely available exploit kits and scripts.
* **Moderate / Departmental Budget:** Groups like hacktivists or internal Shadow IT departments. Hacktivists may rely on crowdsourced donations, while Shadow IT uses unauthorized departmental funds or corporate credit cards.
* **Extensive / State-Level Backing:** Organized crime syndicates and nation-state entities possessing multi-million or multi-billion-dollar budgets. These resources allow actors to acquire expensive zero-day exploits, maintain complex command-and-control (C2) infrastructures, hire specialized talent, and sustain prolonged campaigns.

#### 3. Level of Sophistication and Capability
* **Low / Unskilled:** Actors who run pre-written scripts or automated vulnerability scanners without understanding the underlying mechanics or code. If an attack fails or is blocked by an IPS/WAF, they lack the technical capability to modify the payload or pivot.
* **Medium / Functional:** Insiders and Shadow IT personnel who possess functional system administration knowledge. They know where core data assets reside and understand how to navigate around specific internal security controls using legitimate administrative tools (Living off the Land).
* **High / Advanced:** Highly skilled developers and exploit authors capable of discovering zero-day vulnerabilities, building custom obfuscated malware, crafting multi-stage attack chains, and maintaining stealthy persistence over extended periods (Advanced Persistent Threats - APTs).


### B. Threat Actor Categories

```
| Threat Actor       | Location          | Resources / Funding   | Sophistication Level      |
|--------------------|-------------------|-----------------------|---------------------------|
| Nation-State       | External          | Extensive (State)     | Very High (APT)           |
| Unskilled Attacker | External/Internal | Very Limited          | Low                       |
| Hacktivist         | External          | Limited / Crowdfunded | Medium to High            |
| Insider Threat     | Internal          | Internal Corporate    | Medium (Domain Knowledge) |
| Organized Crime    | External          | High (Commercial)     | High (Structured)         |
| Shadow IT          | Internal          | Departmental Budget   | Low to Limited            |
```

#### 1. Nation-State
* **Operational Profile:** State-sponsored organizations or intelligence/military units operating on behalf of a national government. Often designated as **Advanced Persistent Threats (APTs)** due to their ability to launch long-term, covert, and highly targeted operations.
* **Target Objectives:** Military installations, defense contractors, critical utilities (power grids, water treatment), financial systems, and state infrastructure.
* **Capabilities:** Unlimited state resources, custom zero-day exploits, specialized tool development, and multi-vector infiltration tactics.
* **Key Example:** The **Stuxnet worm**, a sophisticated joint operation developed by the United States and Israel specifically designed to physically sabotage Iranian nuclear centrifuges at the Natanz enrichment facility by altering industrial control system (ICS/SCADA) parameters while spoofing monitoring telemetry.

#### 2. Unskilled Attacker
* **Operational Profile:** Commonly referred to as "script kiddies." These attackers rely entirely on publicly available, pre-packaged tools, executable scripts, and exploit kits (such as automated scanning software or public Metasploit modules).
* **Operational Limitations:** Lacks deep technical understanding of network protocols, operating system kernels, or application code. If a script fails, the actor cannot diagnose the error, modify the shellcode, or evade signature-based detection mechanisms.
* **Targeting Style:** Highly opportunistic. They look for easy targets, unpatched public systems, or default configurations rather than targeting specific organizations.

#### 3. Hacktivist
* **Operational Profile:** A synthesis of "hacker" and "activist." Hacktivists execute cyber operations to advance political, social, ideological, or philosophical agendas.
* **Tactics & Methods:**
  * **Website Defacement:** Replacing an organization's homepage content with political propaganda, banners, or manifestos.
  * **Distributed Denial of Service (DDoS):** Overwhelming web servers or service endpoints to silence targeted organizations or draw public attention.
  * **Data Dumps / Doxxing:** Stealing private emails, internal documents, or customer records and leaking them publicly to embarrass or financially harm the victim entity.
* **Funding:** Typically low to moderate, relying on community donations, fundraising drives, or decentralized volunteer networks.

#### 4. Insider Threat
* **Operational Profile:** Current or former employees, contractors, trusted partners, or vendors who misuse authorized access to inflict harm on an organization's systems or data.
* **Mechanics:** Unlike external actors who must breach the perimeter, insider threats leverage legitimate credentials, authorized access rights, and intimate knowledge of internal systems, data repositories, and backup locations.
* **Inherent Risks:** Extremely difficult to detect using standard perimeter controls (e.g., firewalls, external IDPS). Security teams rely on User and Entity Behavior Analytics (UEBA), Data Loss Prevention (DLP), Principle of Least Privilege (PoLP), and mandatory background vetting during the onboarding process to mitigate this risk.

#### 5. Organized Crime
* **Operational Profile:** Motivated strictly by monetary profit and structured like modern corporate enterprises. These syndicates operate complex business models in the cyber underground.
* **Corporate Hierarchy:**
  * **Exploit Developers:** Research vulnerabilities and code custom malware/ransomware strains.
  * **Attack Operators / Affiliates:** Execute network breaches and deploy payloads (Ransomware-as-a-Service model).
  * **Data Brokers:** Sell exfiltrated database records, credit card numbers, and credentials on dark web marketplaces.
  * **Customer Support:** Staff helpdesks to negotiate ransom payments, assist victims with Bitcoin transactions, and provide decryption keys upon payment.
* **Primary Vectors:** High-volume ransomware campaigns, Business Email Compromise (BEC) fraud, wire fraud, and large-scale data exfiltration for extortion.

#### 6. Shadow IT
* **Operational Profile:** Internal business departments, working groups, or individual employees who procure, deploy, and manage IT hardware, software, or cloud resources (SaaS/PaaS) without the authorization, oversight, or knowledge of the official IT and Information Security departments.
* **Drivers:** Initiated to bypass rigid administrative procedures, Change Control boards, or ticketing delays in order to complete departmental tasks faster using personal credit cards or departmental expense budgets.
* **Security Hazards:**
  * Operating outside security logging, SIEM monitoring, and vulnerability scanning.
  * Lack of data backup routines and disaster recovery plans.
  * Non-compliance with regulatory frameworks (e.g., HIPAA, GDPR, PCI-DSS) due to unvetted cloud storage of sensitive corporate data.



### C. Threat Actor Motivations

Understanding *why* an actor targets an enterprise dictates the likely vector and impact. CompTIA Security+ specifies 10 distinct motivations:

1. **Data Exfiltration:** The intentional, unauthorized transfer of sensitive data out of an enterprise perimeter. Used to steal trade secrets, customer records, PII, or intellectual property for competitive advantage or sale.
2. **Espionage:** Covertly gathering secret commercial, industrial, or state intelligence to gain a strategic, economic, or military advantage over a rival enterprise or nation-state.
3. **Service Disruption:** Impairing, degrading, or disabling network infrastructure, application services, or business workflows to inflict financial damage, operational inconvenience, or public embarrassment.
4. **Blackmail:** Coercing an organization into paying money or complying with demands under threat of releasing stolen confidential data, exposing corporate misconduct, or permanently deleting encrypted systems (extortion/ransomware).
5. **Financial Gain:** The primary driver for cybercrime. Generating direct monetary profit through ransomware ransoms, credit card theft, fraudulent wire transfers, or monetizing stolen database records.
6. **Philosophical / Political Beliefs:** Conducting cyber attacks to highlight perceived injustices, promote a specific political party or cause, or advance ideological viewpoints (the primary driver for hacktivism).
7. **Ethical:** Actions guided by an individual's moral principles or ethical code. Examples include "gray hat" security researchers exposing vulnerabilities publicly when a vendor ignores private reports, or whistleblowers exposing illegal corporate activities.
8. **Revenge:** Retaliation by a disgruntled current or former employee, contractor, or business partner following a termination, demotion, or perceived personal slight.
9. **Disruption / Chaos:** Executing cyber attacks without a specific commercial, financial, or political goal, driven purely by personal thrill, notoriety, or the desire to create widespread panic and operational confusion.
10. **War:** State-sanctioned military cyber operations launched concurrently with or prior to conventional physical warfare. Targets adversary defense command-and-control, communications grids, power generation, water utilities, and national banking systems to undermine military capability and civilian infrastructure.

---

## Objective 2.2: Common `Threat Vectors and Attack Surfaces`

### Overview & Mechanics
In cybersecurity, an **attack surface** refers to the total sum of vulnerabilities, pathways, or methods that a threat actor can use to gain unauthorized access to a network or system. A **threat vector** (or attack vector) is the specific path or mechanism the attacker uses to cross that attack surface and deliver a payload. As a network engineer or security analyst, identifying and minimizing your organization's attack surface is a primary defensive strategy. By understanding exactly how attackers attempt to infiltrate environments—whether through technological vulnerabilities, third-party supply chains, or the human element—security teams can deploy appropriate administrative, technical, and physical controls to secure those pathways.

#### Security Implications
1. **Confidentiality:** Exploitation of threat vectors such as unprotected wireless networks, default credentials, or social engineering often leads to unauthorized data access, credential harvesting, and the exfiltration of sensitive proprietary data.
2. **Integrity:** Vectors like file-based attacks, unsupported systems, and supply chain compromises allow threat actors to install malware, alter application source code, or modify network configurations, destroying the trustworthiness of the environment.
3. **Availability:** Open service ports and vulnerable software can be weaponized to launch denial-of-service (DoS) attacks, while message-based vectors often deliver ransomware that encrypts mission-critical data, halting business operations.

### A. Communication and Media-Based Vectors

#### 1. Message-Based 
Attackers leverage common communication platforms to deliver malicious links, payloads, or social engineering lures.
* **Email:** The most common threat vector for enterprise environments. Attackers use email to deliver malware attachments or links to credential-harvesting websites. Bypassing email filtering requires constant vigilance via spam filters, SPF, DKIM, and DMARC.
* **Short Message Service (SMS):** SMS messages bypass corporate network filters and go directly to user devices. They frequently include shortened URLs linking to malicious sites designed for mobile platforms.
* **Instant Messaging (IM):** Platforms like Microsoft Teams, Slack, WhatsApp, and Telegram. If an attacker compromises an internal account, they can use IM to distribute malware laterally across the organization under the guise of a trusted colleague.

#### 2. Image-Based
Threat actors embed malicious code within image files. 
* **Mechanics:** Attackers use **steganography** to hide scripts, malware, or exfiltrated data within the pixels or metadata (EXIF data) of seemingly benign images (e.g., .jpg or .png). When the image is processed by a vulnerable application, the hidden payload is extracted and executed, often evading traditional antivirus scanners.

#### 3. File-Based
Malicious payloads disguised as standard business documents.
* **Mechanics:** Attackers weaponize common file types, such as Microsoft Office documents (using malicious VBA macros) or Adobe PDF files (embedding malicious JavaScript). When a user opens the file, the embedded script executes locally to establish a backdoor or download additional malware (a dropper).

#### 4. Voice Call
Exploiting legacy and modern telephony for direct human manipulation.
* **Mechanics:** Attackers use voice over IP (VoIP) systems, caller ID spoofing, and increasingly, AI-generated "deepfake" audio to impersonate executives or IT personnel. The goal is to extract passwords, multi-factor authentication (MFA) codes, or authorize wire transfers in real-time.

#### 5. Removable Device
Bypassing perimeter security controls via physical media.
* **Mechanics:** Devices like USB flash drives, external hard drives, or malicious charging cables (e.g., O.MG cable). These devices can be dropped in parking lots for employees to find. When plugged into a workstation, they can act as a "BadUSB" (emulating a keyboard to instantly inject malicious keystrokes) or bypass air-gapped networks to introduce malware directly behind corporate firewalls.

### B. System and Network Infrastructure Vectors

#### 6. Vulnerable Software (Client-Based vs. Agentless)
Exploiting flaws in software code, architecture, or design.
* **Client-Based:** Vulnerabilities residing in software that requires a local agent or application installed on the endpoint (e.g., VPN clients, endpoint security agents, or mobile device management (MDM) agents). If the agent runs with system-level privileges, exploiting it grants the attacker full control of the device.
* **Agentless:** Vulnerabilities in systems that do not require local software installation to interact with them. This includes web applications, browser-based portals, or network protocols (like SSH or WMI). Attackers exploit these over the network without needing an initial footprint on the machine.

#### 7. Unsupported Systems and Applications
Systems that have reached End of Life (EOL) or End of Support (EOS).
* **Mechanics:** The vendor no longer provides security patches or firmware updates. Any zero-day vulnerabilities discovered in these systems will remain permanently unpatched, creating a permanent, highly exploitable attack surface (e.g., legacy Windows OS versions, old industrial control systems).

#### 8. Unsecure Networks
Exploiting weak configurations in data transmission mediums.
* **Wireless:** Wi-Fi networks using weak encryption (WEP, WPA), open guest networks without captive portals, or "rogue access points" and "evil twins" set up by attackers to capture over-the-air traffic (packet sniffing).
* **Wired:** Physical network jacks in lobbies or conference rooms lacking port security (e.g., 802.1X). Attackers plug directly into the corporate LAN to bypass the perimeter firewall completely.
* **Bluetooth:** Short-range wireless attacks like Bluejacking (sending unsolicited messages) or Bluesnarfing (unauthorized access and theft of data from a Bluetooth device).

#### 9. Open Service Ports
Unnecessary doorways left open on network appliances or servers.
* **Mechanics:** Every open port represents a listening service. If unencrypted management ports like Telnet (23) or FTP (21), or remote access ports like RDP (3389) are exposed to the public internet, attackers will use automated scanners (like Nmap) to find them and launch brute-force or vulnerability-specific attacks.

#### 10. Default Credentials
Failing to change factory-assigned usernames and passwords.
* **Mechanics:** Many routers, switches, IoT devices, and web cameras ship with well-known default credentials (e.g., admin/admin). Attackers maintain massive dictionaries of these factory defaults. Deploying a device without changing these credentials grants immediate administrative access to the attacker.

### C. Third-Party and Supply Chain Vectors

#### 11. Supply Chain
Targeting a highly secure organization by compromising their weaker third-party partners.
* **Managed Service Providers (MSPs):** Outsourced IT firms manage networks for dozens or hundreds of clients. By breaching the MSP's remote management tools (RMM), attackers gain a master key to deploy malware (like ransomware) to all of the MSP’s downstream clients simultaneously.
* **Vendors and Suppliers:** Compromising a software vendor to inject malicious code into legitimate, digitally signed software updates (e.g., the SolarWinds Orion breach). Alternately, hardware suppliers can be intercepted in transit to install physical backdoor implants before equipment reaches the customer.

### D. Human Vectors and Social Engineering

The human element is often the weakest link in any security posture. Social engineering relies on psychological manipulation—creating urgency, fear, or trust—to trick users into making security mistakes.

#### 12. Types of Social Engineering
* **Phishing:** A broad, mass-distributed email campaign attempting to trick users into clicking malicious links, opening infected attachments, or giving up credentials.
* **Vishing (Voice Phishing):** Social engineering conducted over voice calls. Attackers often spoof caller ID to appear as internal IT or a trusted bank, creating a sense of urgency to extract information.
* **Smishing (SMS Phishing):** Phishing conducted via text messages, often pretending to be delivery services, banks, or the victim's boss needing an emergency favor.
* **Misinformation / Disinformation:** 
  * *Misinformation:* The accidental spread of false information without malicious intent.
  * *Disinformation:* The deliberate, malicious creation and sharing of false information to manipulate public opinion, damage a brand's reputation, or influence stock prices.
* **Impersonation:** An attacker pretending to be someone they are not, either digitally (CEO email) or physically (dressing as a delivery driver or maintenance worker to gain physical facility access).
* **Business Email Compromise (BEC):** A highly targeted attack where a threat actor compromises a legitimate corporate email account (usually an executive or finance officer). They use this trusted account to request fraudulent wire transfers or invoice payments from employees or partners.
* **Pretexting:** The attacker creates an elaborate fabricated scenario (a pretext) to engage the victim. This backstory builds trust before the attacker asks for sensitive data (e.g., "I am from corporate HR conducting an urgent payroll audit...").
* **Watering Hole Attack:** Instead of attacking the target directly, the attacker infects a specific third-party website that they know the target demographic frequently visits (e.g., a specific industry forum or a local restaurant menu page).
* **Brand Impersonation:** Hijacking a company's corporate identity. Attackers use stolen logos, similar email templates, and spoofed domains to trick customers or employees into believing they are interacting with the legitimate brand.
* **Typosquatting (URL Hijacking):** Registering domain names that are typographical errors of legitimate, popular websites (e.g., substituting a zero for an "O", like `microsoft.com` vs. `micr0soft.com`). When a user accidentally mistypes the URL, they are directed to a malicious lookalike site designed to harvest their credentials.

---

## Objective 2.3: Various `Types of Vulnerabilities`

### Overview & Mechanics
In information security, a **vulnerability** is a weakness or flaw in a system's design, implementation, operation, or internal controls that a threat actor can exploit to compromise the system. While a *threat* is an external force (like a hacker) and a *risk* is the probability of an incident occurring, a *vulnerability* is the actual gap in your armor. As network engineers and security professionals, our primary job in vulnerability management is to identify, classify, and remediate these weaknesses before they can be weaponized. Vulnerabilities can exist anywhere in the technology stack—from the physical hardware and operating systems up to the applications, cloud architectures, and even the human-configured settings.

#### Security Implications
1. **Confidentiality:** Vulnerabilities like SQL injection, cryptographic flaws, or cloud misconfigurations often allow attackers to bypass authentication and read sensitive, proprietary, or regulated data.
2. **Integrity:** Web-based vulnerabilities (like XSS), malicious supply chain updates, or mobile device jailbreaking allow attackers to alter data, modify application behavior, or corrupt the operating system environment.
3. **Availability:** Application vulnerabilities such as buffer overflows or hardware vulnerabilities like legacy failing equipment can crash services, cause kernel panics, or render systems entirely unresponsive to legitimate users.

### A. Application Vulnerabilities
Flaws within the source code or runtime environment of a specific software application.
* **Memory Injection:** An attacker inserts malicious code into the memory space of a running process. This allows the attacker to manipulate the application's behavior or execute arbitrary commands within the context of that application.
* **Buffer Overflow:** Occurs when an application receives more input data than it was programmed to handle in its allocated memory block (the buffer). The excess data spills over into adjacent memory spaces, potentially overwriting executable code. Attackers use this to crash the system or execute malicious code (shellcode) with the privileges of the compromised application.
* **Race Conditions:** A vulnerability that occurs when a system's behavior depends on the sequence or timing of uncontrollable events. The attacker manipulates this timing to force the system to perform unauthorized actions.
  * **Time-of-Check (TOC) vs. Time-of-Use (TOU):** A specific type of race condition. The system *checks* a condition (like verifying a user has permission to read a file), but there is a slight delay before the system actually *uses* or accesses the file. During that microsecond gap, the attacker swaps the authorized file for an unauthorized one. The system, having already completed the TOC, blindly executes the TOU on the malicious file.
* **Malicious Update:** Attackers compromise the update mechanism of a legitimate application. When the application reaches out to download its routine software patch, it downloads and installs malware instead, automatically granting the attacker a foothold.

### B. Operating System (OS)-Based Vulnerabilities
Flaws located within the core operating system (Windows, Linux, macOS) itself.
* **Mechanics:** These vulnerabilities often exist within the OS kernel, file system drivers, or built-in authentication modules. Because the OS sits beneath all other applications, exploiting an OS vulnerability often grants complete, system-level control (privilege escalation). Mitigation requires rigorous OS patch management and hardening.

### C. Web-Based Vulnerabilities
Vulnerabilities specific to web applications and how they interact with users and backend servers.
* **Structured Query Language Injection (SQLi):** An attacker enters malicious SQL commands into a web form or URL parameter that is passed directly to the backend database without proper input validation. This tricks the database into executing the attacker's commands, allowing them to read, modify, or delete database records (e.g., entering `' OR 1=1; --` to bypass a login prompt).
* **Cross-Site Scripting (XSS):** An attacker injects malicious client-side executable scripts (usually JavaScript) into a trusted website. When a legitimate user visits the compromised page, their browser blindly executes the script. This is used to steal session cookies, redirect users to malicious sites, or deface websites. Unlike SQLi (which attacks the database), XSS attacks the *user's browser*.

### D. Hardware Vulnerabilities
Weaknesses inherent to physical devices, silicon chips, or the code embedded directly on them.
* **Firmware:** The low-level software programmed directly into hardware devices (routers, IoT devices, BIOS/UEFI). Firmware vulnerabilities are dangerous because they operate below the operating system layer, making them invisible to standard antivirus software.
* **End-of-Life (EOL):** Hardware that the manufacturer no longer supports. Once a device reaches EOL, the vendor stops releasing firmware updates or security patches, meaning any newly discovered vulnerabilities will remain permanently exploitable.
* **Legacy:** Older hardware that may still technically function but relies on outdated, inherently insecure architectures or protocols that cannot be secured to modern standards.

### E. Virtualization Vulnerabilities
Flaws specific to virtualized environments (Hyper-V, VMware ESXi, KVM) where multiple virtual machines (VMs) share physical hardware.
* **Virtual Machine (VM) Escape:** The most severe virtualization vulnerability. An attacker compromises a guest VM and exploits a vulnerability in the hypervisor to "escape" the virtualized sandbox. This grants the attacker access to the host operating system and, consequently, all other VMs running on that host.
* **Resource Reuse:** When a hypervisor reallocates hardware resources (like RAM or storage blocks) from one VM to another without properly clearing or zeroing out the data first. The new VM might be able to read sensitive residual data left behind by the previous VM (data remanence).

### F. Cloud-Specific Vulnerabilities
Weaknesses introduced by the dynamic, distributed nature of cloud computing (IaaS, PaaS, SaaS).
* **Mechanics:** These include insecure APIs used to manage cloud resources, improper multi-tenancy isolation, or weaknesses in the cloud provider's management plane. A major cloud vulnerability is the failure to properly implement the "Shared Responsibility Model," where the customer mistakenly assumes the cloud provider is securing data that the customer is actually responsible for.

### G. Supply Chain Vulnerabilities
Compromises that occur not within your organization, but within the organizations that supply your goods and services.
* **Service Provider:** Vulnerabilities in Managed Service Providers (MSPs). If an attacker breaches the MSP, they can pivot into the networks of all the MSP's clients using trusted remote management tools.
* **Hardware Provider:** Interdiction during manufacturing or shipping where malicious components (like hardware backdoors or counterfeit chips) are physically installed into routers or servers before they ever reach your data center.
* **Software Provider:** Attackers infiltrate a software vendor's development environment and insert malicious code into the application's source code repository. When the vendor compiles and distributes the software, all customers are infected (e.g., the SolarWinds attack).

### H. Cryptographic Vulnerabilities
Weaknesses in how data is encrypted, hashed, or digitally signed.
* **Mechanics:** These occur when systems use deprecated, weak algorithms (like DES for encryption or MD5 for hashing) that can be easily cracked by modern computing power. It also includes poor key management (storing decryption keys in plain text alongside the encrypted data) or using weak random number generators (predictable entropy) to create encryption keys.

### I. Misconfiguration
Security gaps caused by human error or failure to follow security best practices.
* **Mechanics:** This is one of the most common vulnerabilities. It includes leaving default administrator passwords unchanged, opening unnecessary firewall ports (like leaving RDP port 3389 open to the internet), misconfiguring cloud storage buckets (like AWS S3) to be publicly readable, or failing to apply the principle of least privilege.

### J. Mobile Device Vulnerabilities
Weaknesses specific to smartphones and tablets (iOS, Android).
* **Side Loading:** The practice of installing mobile applications from unapproved, third-party sources (like downloading an APK directly from a website) rather than the official Apple App Store or Google Play Store. Sideloaded apps bypass official security vetting and frequently contain malware.
* **Jailbreaking (iOS) / Rooting (Android):** The process of removing the manufacturer's software restrictions to gain administrative (root) access to the device's operating system. While it allows deep customization, it intentionally disables the OS's built-in security sandboxing, leaving the device highly vulnerable to malicious applications.

### K. Zero-Day
The most critical timeframe for any vulnerability.
* **Mechanics:** A zero-day is a software vulnerability that is currently unknown to the software vendor or the cybersecurity community. Because the vendor has had "zero days" to develop a patch, no security update exists. Threat actors (especially Nation-State APTs) highly prize zero-days because they guarantee a successful exploit against fully updated systems until the vulnerability is eventually discovered and patched.