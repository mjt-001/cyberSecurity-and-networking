# Security Operations

## Domain 4.1: Apply Security Techniques

### Overview & Mechanics
Hardening and baseline management form the cornerstone of defense-in-depth, ensuring that systems are configured securely from inception through decommissioning. Security engineers must establish rigorous configuration baselines, harden endpoints and infrastructure, secure wireless and mobile architectures, enforce application-level defenses, utilize sandboxing for isolated execution, and maintain continuous monitoring to detect and mitigate drift, vulnerabilities, and unauthorized activities.

#### Security Implications
1. **Confidentiality:** Proper baselining, hardening, and cryptographic controls prevent unauthorized disclosure of sensitive data stored on endpoints, transmitted over wireless networks, or processed within applications and cloud environments.
2. **Integrity:** Secure configurations, input validation, code signing, and integrity monitoring ensure that system binaries, configurations, data payloads, and firmware remain free from unauthorized tampering, injection attacks, or malicious modifications.
3. **Availability:** Hardened infrastructure, robust mobile device management, redundancy, and continuous monitoring protect against denial-of-service (DoS) conditions, resource exhaustion, and operational downtime caused by misconfigurations or zero-day exploits.

### A. Secure Baselines
A secure baseline is a standardized, hardened configuration set for systems, applications, and networks that meets organizational security policies and regulatory frameworks (e.g., CIS benchmarks, NIST SP 800-53).

- **Establish:**
  - Define minimum security requirements based on industry standards, threat intelligence, and compliance mandates.
  - Remove unnecessary services, disable default accounts, change default credentials, close unused network ports, and enforce strong password policies.
  - Document the golden image or configuration template containing all required patches, group policy objects (GPOs), and security settings.

- **Deploy:**
  - Apply the established baseline consistently across all target assets during provisioning or deployment (e.g., using automated deployment tools like Ansible, Terraform, or Microsoft Intune).
  - Ensure zero-touch or automated deployment pipelines inject hardening settings before the asset connects to production networks.

- **Maintain:**
  - Implement configuration management and continuous monitoring to detect **configuration drift**—the gradual deviation of a system's settings from the approved baseline over time.
  - Use file integrity monitoring (FIM) and automated auditing tools to identify unauthorized changes.
  - Perform regular patch management and baseline updates to address newly discovered vulnerabilities without breaking operational dependencies.

### B. Hardening Targets
Hardening involves reducing the attack surface of specific assets by disabling unnecessary functionality and strengthening defenses.

- **Mobile Devices:**
  - Enforce full-disk encryption (FDE), biometric authentication, remote wipe capabilities, and application whitelisting.
  - Restrict side-loading of applications and enforce corporate containerization.

- **Workstations:**
  - Disable legacy protocols (e.g., SMBv1, LLMNR, NetBIOS).
  - Enforce disk encryption (BitLocker, FileVault), local firewall rules, user account control (UAC), and endpoint detection and response (EDR) agents.

- **Switches:**
  - Disable unused physical switch ports and place them into an unused VLAN.
  - Implement Port Security (MAC limiting), 802.1X network access control, DHCP snooping, Dynamic ARP Inspection (DAI), and root guard on Spanning Tree Protocol (STP).
  - Secure management planes using SSHv2, HTTPS, and disabled Telnet/HTTP.

- **Routers:**
  - Filter traffic using Access Control Lists (ACLs).
  - Secure routing protocols with authentication (e.g., OSPF MD5/SHA authentication, BGP TTL security).
  - Disable source routing, IP redirects, and ICMP broadcast responses.

- **Cloud Infrastructure:**
  - Follow the shared responsibility model.
  - Harden Identity and Access Management (IAM) using the principle of least privilege and Multi-Factor Authentication (MFA).
  - Implement secure storage configurations (e.g., private S3 buckets, encryption at rest and in transit), security groups, and cloud posture management (CSPM) tools.

- **Servers:**
  - Role-based hardening (e.g., stripping a database server of web services and compilers).
  - Disable interactive local logins where possible, enforce strict permission boundaries on file systems, and harden operating system kernels.

- **ICS/SCADA (Industrial Control Systems / Supervisory Control and Data Acquisition):**
  - Isolate operational technology (OT) networks from enterprise IT networks using industrial firewalls and air-gapping where necessary.
  - Implement unidirectional security gateways (data diodes).
  - Restrict physical access to Remote Terminal Units (RTUs) and Programmable Logic Controllers (PLCs).

- **Embedded Systems:**
  - Secure firmware update mechanisms using cryptographic signing.
  - Remove debug interfaces (JTAG/UART) in production units.
  - Minimize software footprint to reduce attack surface.

- **RTOS (Real-Time Operating Systems):**
  - Secure deterministic timing constraints while applying necessary authentication and minimal privilege controls.
  - Protect against priority inversion attacks and buffer overflows in memory-constrained environments.

- **IoT Devices (Internet of Things):**
  - Eliminate hardcoded hardcoded/default credentials.
  - Implement secure boot, regular firmware patching over-the-air (OTA), and network segmentation (placing IoT on isolated guest or VLAN segments).

### C. Wireless Devices
Wireless security requires careful planning during physical installation to ensure coverage meets business needs while minimizing leakage outside physical perimeters.

- **Installation Considerations:**
  - **Site Surveys:** Comprehensive physical and RF (Radio Frequency) assessments conducted prior to deployment to determine optimal Access Point (AP) placement, measure signal strength, identify dead zones, and detect rogue access points or sources of interference (e.g., microwave ovens, Bluetooth devices).
  - **Heat Maps:** Visual graphical representations generated by site survey software that map RF signal propagation, coverage overlap, channel allocation, and signal-to-noise ratio (SNR) across facility floor plans. They ensure adequate coverage while preventing excessive signal leakage outside the building perimeter.

### D. Mobile Solutions
Managing mobile endpoints requires specialized frameworks to balance security and usability.

- **Mobile Device Management (MDM):**
  - Centralized administrative software that allows security teams to manage, monitor, configure, and secure mobile devices over-the-air.
  - Enables policy enforcement, certificate distribution, app deployment, geolocation tracking, and remote lock/wipe capabilities.

- **Deployment Models:**
  - **Bring Your Own Device (BYOD):** Employees use personal devices for work. Offers cost savings but introduces data privacy and device control challenges; mitigated via containerization (separating personal and work data).
  - **Corporate-Owned, Personally Enabled (COPE):** Devices are purchased by the organization and issued to employees, who are permitted limited personal use. Balances corporate security control with user satisfaction.
  - **Choose Your Own Device (CYOD):** Employees select a device from a pre-approved, vetted catalog provided by the organization. Ensures compatibility with enterprise management tools.

- **Connection Methods:**
  - **Cellular:** Utilizes mobile carrier networks (4G/5G). Offers broad geographic coverage and hardware-backed security via SIM/eSIM authentication, though vulnerable to IMSI catchers (stingrays) if unencrypted.
  - **Wi-Fi:** Local wireless networking. Requires enterprise-grade encryption and authentication (WPA3-Enterprise, 802.1X).
  - **Bluetooth:** Short-range wireless protocol. Vulnerable to attacks such as bluesnarfing and bluejacking; mitigated by disabling discovery mode and using pairing confirmation.

### E. Wireless Security Settings
Securing wireless transmissions prevents eavesdropping, unauthorized network access, and credential harvesting.

- **Wi-Fi Protected Access 3 (WPA3):**
  - **WPA3-Personal:** Replaces Pre-Shared Key (PSK) with Simultaneous Authentication of Equals (SAE), protecting against offline dictionary attacks even with weak passwords.
  - **WPA3-Enterprise:** Mandates a 128-bit minimum security baseline (with optional 192-bit mode for high-security environments), utilizing GCMP-256 encryption and robust cryptographic key management.

- **AAA / RADIUS (Remote Authentication Dial-In User Service):**
  - Centralized authentication, authorization, and accounting framework used heavily in enterprise 802.1X deployments.
  - RADIUS servers validate user credentials against directories (e.g., Active Directory) and issue dynamic encryption keys.

- **Cryptographic Protocols:**
  - Modern wireless relies on robust encryption suites such as CCMP (Counter Mode with Cipher Block Chaining Message Authentication Code Protocol) using AES for WPA2, and GCMP (Galois/Counter Mode Protocol) for WPA3. Obsolete protocols like WEP and WPA-TKIP must be disabled.

- **Authentication Protocols:**
  - **EAP (Extensible Authentication Protocol):** Framework supporting various authentication methods.
  - **PEAP (Protected EAP):** Creates a TLS tunnel between the client and authentication server before transmitting credentials inside.
  - **EAP-TLS:** Requires mutual certificate-based authentication (client and server), representing the highest standard of wireless security.
  - **EAP-TTLS:** Extends EAP by allowing older authentication methods within a TLS-secured tunnel.

### F. Application Security
Software vulnerabilities must be addressed throughout the Software Development Life Cycle (SDLC).

- **Input Validation:**
  - Never trust user input. Implement strict validation, sanitization, and parameterized queries (prepared statements) to prevent injection flaws (SQL injection, Command injection, Cross-Site Scripting).
  - Employ allow-listing (positive validation) over block-listing.

- **Secure Cookies:**
  - Ensure session cookies use security flags:
    - **Secure Flag:** Ensures cookies are only transmitted over encrypted HTTPS connections.
    - **HttpOnly Flag:** Prevents client-side scripts (JavaScript) from accessing the cookie, mitigating Cross-Site Scripting (XSS) session theft.
    - **SameSite Flag:** Controls whether cookies are sent with cross-site requests (`Strict`, `Lax`, or `None`), mitigating Cross-Site Request Forgery (CSRF).

- **Static Code Analysis (SAST):**
  - Analyzing source code or compiled code for vulnerabilities without executing the program (white-box testing).
  - Integrated into CI/CD pipelines to catch bugs, insecure function calls, and logic flaws early in development.

- **Code Signing:**
  - Developers digitally sign software binaries using a private key tied to a trusted Certificate Authority (CA).
  - Operating systems verify the digital signature prior to execution to confirm software authenticity, integrity, and non-repudiation (ensuring the code has not been tampered with since signing).

### G. Sandboxing
- An isolated, restricted execution environment (virtualized or containerized) that separates running programs from the host operating system and network.
- Used for running untrusted code, analyzing malware behavior, or executing high-risk browser tasks to ensure that any malicious actions or exploits cannot escape the sandbox boundary and compromise the underlying system.

### H. Monitoring
- Continuous observation of systems, networks, applications, and logs to detect anomalies, policy violations, and active intrusions.
- Utilizes tools such as SIEM (Security Information and Event Management), IDS/IPS, EDR, and FIM to collect telemetry, generate real-time alerts, and feed incident response workflows.

---
---

## Domain 4.2: Security Implications of Proper Hardware, Software, and Data Asset Management

### Overview & Mechanics
Asset management is foundational to cybersecurity because an organization cannot secure what it does not know it owns. Proper governance ensures that supply chain risks are minimized, data is appropriately classified and handled, assets are continuously tracked against unauthorized modifications or losses, and end-of-life media is securely sanitized or destroyed to prevent data leakage.

#### Security Implications
1. **Confidentiality:** Proper data classification, ownership assignment, inventory tracking, and secure disposal/sanitization prevent unauthorized exposure, extraction, or theft of sensitive corporate and customer data throughout the asset lifecycle.
2. **Integrity:** Procurement controls, software bills of materials (SBOMs), and configuration tracking ensure that acquired hardware and software components are genuine, unmodified, and free from embedded backdoors or supply chain tampering.
3. **Availability:** Comprehensive asset tracking, lifecycle management, and planned decommissioning prevent operational bottlenecks, ghost assets, unpatched legacy hardware failures, and resource exhaustion caused by unmanaged infrastructure.

### A. Acquisition/Procurement Process
The acquisition process governs how hardware, software, and services are vetted, purchased, and integrated into the enterprise environment.
- **Supply Chain Security:** Evaluating third-party vendors, suppliers, and manufacturers to ensure they adhere to strict security standards, minimizing the risk of hardware/software tampering or counterfeit components.
- **Approved Vendor Lists (AVL):** Restricting purchases to pre-vetted, trusted suppliers who meet organizational compliance and security requirements.
- **Software Bills of Materials (SBOM):** Requiring software vendors to provide a formal inventory of all components, libraries, and open-source dependencies included in an application to rapidly identify vulnerabilities (e.g., Log4j).
- **Hardware Root of Trust:** Procuring hardware equipped with trusted platform modules (TPMs) or cryptographic secure elements to verify boot integrity.

### B. Assignment/Accounting
Once assets are acquired, they must be formally accounted for, assigned to responsible parties, and categorized based on sensitivity.
- **Ownership:** 
  - Designating a specific individual or business unit (data owner, asset custodian) accountable for the security, usage, and maintenance of the asset.
  - Ensures clear lines of responsibility for access control reviews and risk management.
- **Classification:**
  - Categorizing data and assets based on their criticality and sensitivity to the organization (e.g., Public, Internal, Confidential, Restricted).
  - Determines the baseline security controls, encryption requirements, access permissions, and handling procedures applied to the asset.
- **Labeling & Tagging:** Applying physical barcode/RFID tags to hardware and metadata tags to digital assets to maintain clear visibility of their classification level.

### C. Monitoring/Asset Tracking
Continuous oversight of enterprise assets ensures that unauthorized devices or unpatched software do not introduce vulnerabilities into the network.
- **Inventory:**
  - Maintaining an up-to-date, centralized repository (such as a Configuration Management Database - CMDB) listing all hardware assets, software licenses, and data repositories.
  - Tracking metrics such as serial numbers, IP/MAC addresses, firmware versions, and assigned owners.
- **Enumeration:**
  - The active or passive discovery process of scanning the network environment to identify connected devices, operating systems, running services, and installed software.
  - Helps detect **shadow IT** (unauthorized hardware or software deployed by employees without IT/security department approval).

### D. Disposal/Decommissioning
When assets reach the end of their operational lifecycle, they must be retired securely to prevent data remnants from falling into unauthorized hands.
- **Sanitization:**
  - The process of removing data from storage media so that it cannot be recovered by ordinary or advanced forensic techniques.
  - Methods include **overwriting** (zeroing out sectors), **degaussing** (disrupting magnetic domains on hard drives using a powerful magnetic field), and **cryptographic erasure / crypto-shredding** (destroying the encryption keys used to encrypt data on the media, rendering ciphertext unrecoverable).
- **Destruction:**
  - Physical destruction of hardware media to guarantee complete data elimination.
  - Techniques include physical shredding, crushing, disintegrating, or incinerating hard drives, solid-state drives (SSDs), and mobile devices.
- **Certification:**
  - Issuing a formal **Certificate of Destruction** or sanitization report verifying that specific assets (identified by serial number) were destroyed or wiped in compliance with regulatory standards (e.g., NIST SP 800-88).
- **Data Retention:**
  - Legal and organizational policies governing how long specific types of data must be kept for compliance, tax, or operational purposes before they are legally eligible for sanitization and disposal.
  - Balances regulatory mandates with privacy risks associated with over-retention.

---
---

## Domain 4.3: Vulnerability Management Activities

### Overview & Mechanics
Vulnerability management is an ongoing, cyclical process of identifying, analyzing, remediating, validating, and reporting security weaknesses across an organization's digital and physical infrastructure. Rather than a one-time scan, a mature vulnerability management program integrates threat intelligence, penetration testing, automated discovery tools, and business context to prioritize risk reduction before threat actors can weaponize flaws.

#### Security Implications
1. **Confidentiality:** Timely identification and patching of unauthenticated information disclosure bugs, misconfigured access controls, and software vulnerabilities prevent unauthorized data exfiltration and intellectual property theft.
2. **Integrity:** Rigorous vulnerability tracking, package monitoring, and code integrity verification stop attackers from injecting malicious payloads or modifying system state through known exploit vectors.
3. **Availability:** Prioritizing remediation for critical denial-of-service (DoS) vulnerabilities and resource exhaustion flaws ensures continuous operational uptime and service reliability.

---

### A. Vulnerability Identification & Discovery
Organizations use diverse methods and intelligence sources to discover security weaknesses before attackers find them.

- **Dynamic Analysis:** Evaluating an application or system while it is actively running (runtime testing), such as Dynamic Application Security Testing (DAST) or runtime application self-protection (RASP), to identify flaws exposed during execution.
- **Package Monitoring:** Tracking third-party software packages, libraries, and open-source dependencies (via tools checking Software Bills of Materials or SBOMs) to alert teams when a component becomes vulnerable.
- **Threat Feeds:** Subscribing to commercial or open-source real-time feeds that deliver indicators of compromise (IoCs), active exploit trends, and newly released vulnerability advisories.
- **Open-Source Intelligence (OSINT):** Gathering publicly available data (e.g., social media, public code repositories, forums, paste sites) to identify leaked credentials, exposed infrastructure, or unannounced asset details.
- **Proprietary / Third-Party Feeds:** Specialized vulnerability feeds provided by vendors (e.g., Microsoft security bulletins, Cisco PSIRT) or security research firms tailored to specific vendor stacks.
- **Information-Sharing Organizations:** Collaborating within industry-specific structures such as ISACs (Information Sharing and Analysis Centers) and ISAOs (Information Sharing and Analysis Organizations) to exchange threat intelligence and vulnerability trends.
- **Dark Web Monitoring:** Scanning illicit forums, marketplaces, and chat channels to detect corporate credentials, stolen data, or zero-day exploits targeting the organization.
- **Penetration Testing:** Authorized, simulated cyber-attacks conducted by ethical hackers (red teams) to discover complex, multi-layered security weaknesses that automated scanners miss.
- **Responsible Disclosure Program:** A structured framework providing a safe, legal channel for security researchers to report vulnerabilities to an organization so they can be patched before public disclosure.
- **Bug Bounty Program:** A formalized crowdsourced security initiative offering financial rewards or recognition to researchers who discover and report valid vulnerabilities.
- **System / Process Audit:** Periodic, systematic evaluations of operating procedures, configurations, and system controls against regulatory standards or internal baselines.

---

### B. Analysis & Confirmation
Once vulnerabilities are identified, security teams must validate their authenticity and evaluate their operational impact.

- **Analysis & Confirmation:** The process of validating raw scanner output or researcher reports to determine if the flaw is genuine, reachable, and exploitable in the target environment.
- **False Positive:** An incorrect finding where a scanner or report indicates a vulnerability exists when the system is actually secure (e.g., banner grabbing misidentifying a patched software version).
- **False Negative:** A dangerous scenario where a scanner fails to detect an existing vulnerability, leading to a false sense of security.
- **Prioritization:** Ranking vulnerabilities based on severity, exploit availability, asset value, and business context to determine remediation order.
- **Common Vulnerability Scoring System (CVSS):** An open industry standard (numeric score from 0.0 to 10.0) used to assess the severity of computer system security vulnerabilities based on metrics like attack vector, complexity, and impact.
- **Common Vulnerabilities and Enumeration (CVE):** A standardized dictionary and naming system for publicly known cybersecurity vulnerabilities (e.g., CVE-2024-XXXXX).
- **Vulnerability Classification:** Categorizing flaws by type (e.g., remote code execution, privilege escalation, injection, broken authentication) to understand systemic weaknesses.
- **Exposure Factor:** The percentage of asset value or operational capability lost if a specific vulnerability is successfully exploited.
- **Environmental Variables:** Local network architecture details, compensating controls, and deployment context that can increase or decrease the effective severity of a vulnerability.
- **Industry / Organizational Impact:** Assessing how a successful exploit would affect business reputation, regulatory compliance, legal liability, and revenue.
- **Risk Tolerance:** The degree of risk an organization is willing to accept or retain based on its strategic goals, financial capacity, and risk appetite.

---

### C. Vulnerability Response & Remediation
Deciding how to address validated vulnerabilities through technical and administrative controls.

- **Patching:** Applying vendor-supplied software updates, firmware revisions, or hotfixes to eliminate the underlying vulnerability code.
- **Cybersecurity Insurance:** Transferring residual financial risk by purchasing policies that cover losses resulting from data breaches or cyber incidents.
- **Segmentation:** Isolating vulnerable assets within restricted network zones or VLANs to limit lateral movement if an exploit occurs.
- **Compensating Controls:** Implementing alternative security mechanisms (e.g., a Web Application Firewall or extra monitoring) when direct patching is temporarily impossible due to operational constraints.
- **Exceptions and Exemptions:** A formal, documented risk acceptance process where management or security governance approves delaying remediation due to legacy compatibility or business justification, subject to regular review.

---

### D. Validation of Remediation
Confirming that remediation efforts were successful and did not introduce secondary issues.

- **Rescanning:** Running automated vulnerability scans against remediated assets to verify that the target signatures or conditions are resolved.
- **Audit:** Conducting independent checks or code reviews to ensure remediation aligns with internal policies and standards.
- **Verification:** Manual confirmation by engineers or security analysts that patches were applied correctly and services function as expected.

---

### E. Reporting
Documenting vulnerability management metrics, residual risks, and remediation progress for stakeholders.
- **Executive Summaries:** High-level overviews tailored for leadership, highlighting overall risk posture, critical trends, and budget requirements.
- **Technical Reports:** Detailed findings, asset lists, CVSS scores, and step-by-step remediation guidance for sysadmins and developers.
- **Compliance Reporting:** Documentation proving adherence to regulatory frameworks (e.g., PCI-DSS, HIPAA, SOC 2) regarding vulnerability discovery and patching SLAs.