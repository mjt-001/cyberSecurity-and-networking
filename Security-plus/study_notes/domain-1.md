# Domain 1: **General Security Controls**

# Objective 1.1: `Security Controls`
Security controls are the safeguards and countermeasures implemented by an organization to preserve the **Confidentiality, Integrity, and Availability (CIA Triad)** of its assets, mitigate risk, and meet legal or regulatory compliance requirements.
<br>

There are 2 core areas:
1. Categories: *How* the control is implemented
2. Types: *What* the control achieves within the incident timeline.

## Control Categories
Control categories define the underlying nature of the safeguard - whether it is enforced by technical hardware/software, policy and governance, human activity, or physical barriers.

```
┌───────────────────┬────────────────────┬──────────────────┬──────────────────┐
│ Technical         │ Managerial         │ Operational      │ Physical         │
│ (Logical)         │ (Administrative)   │ (Procedural)     │ (Tangible)       │
├───────────────────┼────────────────────┼──────────────────┼──────────────────┤
│ System-enforced   │ Policy, governance │ Human-executed   │ Environment      │
│ software/hardware │ & risk oversight   │ operational tasks│ & infrastructure │
└───────────────────┴────────────────────┴──────────────────┴──────────────────┘
```
Use acronym **`TMOP`** as a memory aid

### Technical Controls
This is hardware, software, or firmware mechanisms implemented within computer systems, networks, and applications to enforce security rules automatically **without** human intervention.
<br>

How it works: 
- They `intercept data` at different layers of the OSI model, inspecting packet headers or payloads, evaluating system state, or enforcing cryptographic algorithms. 
- They act as automated enforcement gates directly within systems.
<br>

Examples:
- **Firewalls:** Inspect traffic flow against Access Control Lists (ACLs) or application-layer inspection algorithms to `permit or block packets` based on IP, port, protocol, or application signature.

- **Intrusion Prevention Systems (IPS):** Analyze network traffic using signature-based detection (comparing packet bytes to known attack vectors) or anomaly-based detection (flagging deviations from a baseline) to inline-drop malicious traffic.

- *Access Control Lists (ACLs):* Enforce identity-based or rules-based decisions directly on routers, switches, or cloud virtual networks (e.g., AWS Security Groups).

- **Endpoint Detection and Response (EDR) / Antivirus (AV):** Software agents executing at the kernel or user level that hook into system APIs to analyze process execution, memory space, and file signatures.

- **Encryption Protocols:** Implementation of algorithms (e.g., AES-256, TLS 1.3) to protect data at rest (Full Disk Encryption via BitLocker) or data in transit (HTTPS/IPsec).

### Managerial Controls
Managerial controls focus on administrative governance, risk evaluation, policy formulation, compliance oversight, and overall security strategy set by executive leadership and security managers.
<br>

How it works: 
- These controls provide the `legal, policy, and framework structure for the organization`. 
- They define what is acceptable, establish liability, allocate resources, and outline consequences for non-compliance.

Examples:
- **Security Policies:** Formal documentation defining organizational expectations (e.g., Acceptable Use Policy (AUP), Password Policy, Data Retention Policy).

- **Risk Assessments:** The process of identifying, analyzing, and evaluating risks (calculating Single Loss Expectancy (SLE), Annualized Rate of Occurrence (ARO), and Annualized Loss Expectancy (ALE)).

- **Vulnerability Management Policies:** Frameworks mandating scanning intervals, remediation SLAs, and risk acceptance protocols.

- **Third-Party Risk Management (TPRM):** Establishing vendor assessment frameworks, Service Level Agreements (SLAs), and Non-Disclosure Agreements (NDAs).

### Operational Controls
Operational controls are administrative and day-to-day security measures executed primarily by people rather than automated systems. They represent the practical, procedural implementation of managerial policies.
<br>

How it works: 
- Operational controls rely on `human execution, daily routines, tactical procedures, and awareness training` to keep security operations running consistently.

Examples:
- **Security Awareness Training:** Educating employees to recognize phishing attempts, social engineering tactics, and poor credential hygiene (e.g., phishing simulation exercises).

- **User Onboarding and Offboarding Procedures:** Manual human checklists followed by HR and IT admins to grant or revoke access privileges, recover company assets, and deactivate accounts.

- **Security Guard Patrols:** Human personnel physically walking the perimeter or monitoring facility access points.

- **Configuration & Patch Management:** The operational routine of testing, approving, and scheduling software patches and standard build deployments across infrastructure.

- **Incident Response Plan Execution:** Human incident responders conducting triage, containment, and root-cause analysis following an alert.

### Physical Controls
Physical controls are tangible, real-world measures designed to prevent physical access to facility grounds, buildings, equipment rooms, and physical assets, as well as protect against environmental hazards.
<br>

How it works: 
- They establish `physical barriers or environmental conditions` that prevent unauthorized physical entry, protect hardware from physical tampering/theft, or mitigate environmental disasters (fire, heat, power failure).

Examples:
- **Perimeter Fencing & Gates:** Structural barriers delaying or preventing unauthorized access to facility grounds.

- **Bollards:** Physical posts engineered to stop vehicle ramming attempts against buildings.

- **Locks and Smart Cards / Badges:** Electronic Access Control (EAC) systems using RFID badges, keycards, or mechanical deadbolts to restrict entry to server rooms.

- **Mantrap / Air Lock Systems:** Dual-door physical access control systems where the second door cannot open until the first door closes, preventing tailgating/piggybacking.

- **Environmental Controls:** HVAC systems maintaining server room temperature/humidity, fire suppression systems (e.g., FM-200 or dry-pipe sprinkler systems), and uninterrupted power supplies (UPS) / diesel backup generators.

## Control Types
Control types define when and why a control operates during an incident lifecycle - whether it prevents, deters, detects, corrects, compensates, or directs security posture.
```
+---------------------------------------------------------------------------------------+
|                                    CONTROL TYPES                                      |
+--------------+-------------+---------------+---------------+--------------+-----------+
| Preventive   | Deterrent   | Detective     | Corrective    | Compensating | Directive |
+--------------+-------------+---------------+---------------+--------------+-----------+
| Stops an     | Discourages | Identifies &  | Restores      | Alternative  | Mandates  |
| attack before| an attack   | logs active or| system back to| workaround   | required  |
| execution    | attempt     | past breaches | normal state  | safeguard    | behavior  |
+--------------+-------------+---------------+---------------+--------------+-----------+
```
Memory aid:  `Please Don't Delay, Correct Countermeasures Directly` === **PDDCCD**
- P - Preventive
- D - Deterrent
- D - Detective
- C - Corrective
- C - Compensating
- D - Directive

### Preventive Controls
Preventive controls act **proactively** to stop an unwanted or unauthorized activity from occurring in the first place.

Underlying Mechanics: They enforce strict access rules, drop unauthorized connection requests, or physically lock out attackers so that a breach attempt fails at the threshold.

Examples across Categories:
- **Technical:** 
    - Firewalls blocking incoming unauthorized ports.
    - IPS inline-dropping malicious payloads.
    - Least Privilege access policies enforced via Active Directory/IAM.
- **Managerial:** Onboarding security policy prohibiting account creation without multi-factor authorization approval.
- **Operational:** Separation of Duties (SoD) requiring two administrators to authorize a critical system change.
- **Physical:** Door locks, biometric scanners, and mantraps physically blocking access to a server closet.

### Deterrent Controls
Deterrent controls do not technically or physically stop an attack, but they are `designed to discourage a potential attacker from attempting` an exploit by increasing perceived cost, effort, or legal risk.

Underlying Mechanics: They leverage psychological disincentives, explicit warnings of legal liability, or visible security presences that alter an adversary's risk-versus-reward calculation.

Examples across Categories:
- **Technical:** Warning banners displayed on system login terminals (e.g., "Unauthorized access is prohibited and monitored under federal law").
- **Managerial:** Clear organizational policy stating that unauthorized data access results in immediate termination and legal prosecution.
- **Operational:** Uniformed security guards patrolling a facility perimeter; visible security personnel in reception.
- **Physical:** Highly visible warning signs ("Premises Under 24/7 Video Surveillance"), dummy security cameras, or high-intensity perimeter lighting.

### Detective Controls
Detective controls `operate during or after an attack` attempt to discover, identify, and log unauthorized activity or policy violations.

Underlying Mechanics: 
- They continuously monitor state changes, log output, traffic patterns, file integrity hashes, or physical movement, alerting administrators so action can be taken. 
- They **do not block the attack on their own**.

Examples across Categories:
- **Technical:** 
    - Intrusion Detection Systems (IDS) sniffing network traffic and alerting on signature matches.
    - Security Information and Event Management (SIEM) aggregating logs.
    - File Integrity Monitoring (FIM) calculating SHA-256 hashes of critical system files to detect modification.
- **Managerial:** Periodic audit reviews of user privileges and access log reports.
- **Operational:** 
    - Guard patrols conducting routine checks of lock integrity.
    - Threat hunting activities performed by SOC analysts.
- **Physical:** 
    - CCTV security cameras recording entryways.
    - Motion sensors in data centers.

### Corrective Controls
Corrective controls are `applied after a detective control` discovers an incident. Their objective is to reverse the damage, contain the impact, patch the underlying vulnerability, and return systems to a known-good operational state.

Underlying Mechanics: They alter system configuration, eliminate malicious artifacts, invoke failover procedures, or restore data from isolated backups.

Examples across Categories:
- **Technical:** 
    - Automatically restoring encrypted files from clean offline/cloud backups following a ransomware attack; running anti-malware quarantine/cleaning routines.
    - Applying vendor patch updates to fix exploited software bugs.
- **Managerial:** Incident Response Policy execution guidelines outlining escalation pathways and lessons-learned post-mortems.
- **Operational:** 
    - Calling emergency law enforcement after a break-in.
    - Isolating an infected endpoint from the VLAN via network access control (NAC).
- **Physical:** Fire extinguisher systems or dry-pipe fire suppression systems deployed to put out server room fires.

### Compensating Controls
Compensating controls are `alternative, backup countermeasures` implemented when a primary security control is impossible, too expensive, or technically unfeasible to deploy (e.g., legacy systems that cannot support modern encryption or authentication protocols).

Underlying Mechanics: They build a secondary protective boundary around a vulnerable asset to mitigate the specific risk that the absent primary control was meant to handle.

Examples across Categories:
- **Technical:** Placing a legacy, unpatchable industrial SCADA machine on an isolated virtual local area network (VLAN) with strict firewall microsegmentation because the vendor application cannot run on a modern, secure OS.
- **Managerial:** Requiring dual-signature sign-off for wire transfers exceeding $10,000 to compensate for the lack of automated transactional limits in an accounting system.
- **Operational:** Implementing temporary 24/7 security guard watch at a server room door while an electronic badge reader system is undergoing repair.
- **Physical:** Deploying portable emergency diesel generators to supply power during a total municipal utility failure.

### Directive Controls
Directive controls `mandate compliance` with explicit operational requirements, standards, or legal guidelines.

Underlying Mechanics: They set explicitly dictated terms for acceptable behavior through policies, organizational mandates, signs, or regulatory standard enforcement.

Examples across Categories:
- **Technical:** System storage policies directing employees to save sensitive files strictly within encrypted cloud directories rather than local drives.
- **Managerial:** Mandating compliance frameworks such as PCI-DSS or GDPR across the organization.
- **Operational:** Security awareness training sessions instructing employees on how to handle sensitive media (e.g., Clean Desk Policy).
- **Physical:** "Authorized Personnel Only" signs posted on doors leading to sensitive operational areas.

## Exam Tips:
Ask myself these questions in the exam or when unsure:
1. Identify the Core Mechanism First (`Category`):
    - Ask: Is this enforced by software/code/hardware? $\rightarrow$ **Technical**
    - Ask: Is this an executive policy, documentation, or risk assessment? $\rightarrow$ **Managerial**
    - Ask: Is a human physically executing a daily routine or training? $\rightarrow$ **Operational**
    - Ask: Can I physically touch it, or does it protect physical space? $\rightarrow$ **Physical**

2. Identify the Timing & Objective Second (`Type`):
    - Ask: Did it stop the attack before it happened? $\rightarrow$ **Preventive**
    - Ask: Did it try to discourage or scare the attacker away? $\rightarrow$ **Deterrent**
    - Ask: Did it log, alert, or record what happened without stopping it? $\rightarrow$ **Detective**
    - Ask: Did it fix, restore, or clean up after detection? $\rightarrow$ **Corrective**
    - Ask: Is it a workaround covering for a missing primary control? $\rightarrow$ **Compensating**
    - Ask: Is it a written or posted command mandating behavior? $\rightarrow$ **Directive**
<br>
---

# Objective 1.2: `Security Concepts`

## 1. CIA Triad (Confidentiality, Integrity, Availability)
The CIA triad is the foundational framework used to evaluate and implement information security controls.
```

                  [ Confidentiality ]
                     /           \
                    /   Security  \
                   /    Balance    \
                  /                 \
        [ Integrity ] ------------- [ Availability ]
```
### Confidentiality
Ensures that sensitive information is `accessible only to authorized subjects` (users, processes, or systems) and is protected against unauthorized disclosure or eavesdropping.

Underlying Mechanics:
- **Symmetric Encryption:** Uses a single shared key to encrypt bulk data at rest or in transit.
- **Asymmetric Encryption:** Uses key pairs (Public Key for encryption, Private Key for decryption) for secure key exchanges and token validation.
- **Access Control Lists (ACLs):** Enforces permissions at the filesystem or network level (firewall rule sets) using security identifiers (SIDs).
- **Obfuscation & Steganography:** Hides plain text within other data carriers or transforms code structure without changing execution logic to slow down reverse engineering.

### Integrity
Guarantees that `data remains accurate, complete, and untampered` with during storage, transit, or processing.

Underlying Mechanics:
- **Cryptographic Hashing:** 
    - One-way mathematical algorithms (e.g., SHA-256) generate a fixed-length digest from variable-length input. 
    - Any single-bit change in the source changes the resulting hash (aka avalanche effect).
- **Digital Signatures:** 
    - Combines a cryptographic hash of a payload with the sender’s private key. 
    - Recipients verify the origin and integrity using the sender's public key.
- **Message Authentication Codes (MAC / HMAC):** Combines a secret key with a cryptographic hash function to ensure both data integrity and data authenticity over network channels.

### Availability
Ensures systems, networks, applications, and data remain `accessible and fully operational` for authorized users when needed.

Underlying Mechanics:
- **Redundancy & Clustering:** High Availability (HA) pairs, active-active or active-passive server clusters running load balancers (e.g., round-robin or least-connections algorithms) to prevent Single Points of Failure (SPOFs).
- **RAID Storage Configurations:** Disk mirroring (RAID 1) or block-level striping with distributed parity (RAID 5/6) allowing continuous array operation during physical drive failures.
- **Site Fault Tolerance:** 
    - Hot sites (near-zero RTO with active replication).
    - Warm sites (pre-configured hardware requiring data restoration).
    - Cold sites (power/cooling available without operational hardware).
- **DDoS Mitigation:** Upstream traffic scrubbing centers, rate limiting, and Anycast network routing to absorb volumetrically saturated link attacks.

## 2. Non-Repudiation
Non-repudiation provides `indisputable proof of the origin, authenticity, and integrity of a transaction or message`, preventing an entity from denying their involvement in an action.

Underlying Technical Mechanics:
- **Digital Signatures:** When a user signs a transaction, their local system hashes the document digest and encrypts it using their private key. Because only the user possesses that private key, successful decryption via their public key proves they initiated the transaction.
- **Asymmetric Key Lifecycle:** Enforced through a Public Key Infrastructure (PKI) where a Certificate Authority (CA) binds a verified user identity to a public/private key pair via x.509 digital certificates.
- **Centralized Immutable Logging:** Audit logs shipped to Write-Once-Read-Many (WORM) storage or cryptographic log chains (append-only ledgers) tagged with NTP-synchronized timestamps prevent post-event log tampering by administrators or attackers.

## 3. AAA Framework (Authentication, Authorization, Accounting)
The AAA framework governs `how access is identity-verified, permission-bounded, and audited` across modern enterprise infrastructure.
```
  [ Subject / User claiming to be someone ]
         |
         |---> 1. AUTHENTICATION ("Are they who they say they are?")  --> Identity Store / Directory
         |
         |---> 2. AUTHORIZATION  ("What can you do?") --> Access Matrix / RBAC / ABAC
         |
         |---> 3. ACCOUNTING     ("What did you do?") --> Centralized Syslog / SIEM
```
### Authenticating `People`
Human identity verification relies on validating one or more distinct authentication factors:

1. **Something You Know:** Passwords, passphrases, or PINs (vulnerable to brute-force, dictionary attacks, and credential stuffing).

2. **Something You Have:** Hardware security keys (FIDO2/WebAuthn YubiKeys), software time-based one-time password (TOTP) authenticators, smart cards (PIV/CAC), or push notification tokens.

3. **Something You Are:** Inherent biometric attributes measured via sensors (fingerprint readers, facial recognition via infrared depth mapping, retina scanning, or iris scanning).

4. **Somewhere You Are:** Geolocation coordinates bounded by GPS data, IP address ranges, or cellular tower triangulation (geofencing).

5. **Something You Do:** Behavioral attributes like typing dynamics (keystroke dynamics), signature motion signatures, or gait analysis.

**Multi-Factor Authentication (MFA):** Requires two or more distinct categories (e.g., Password + TOTP App). 
- **Note:** Combining two items from the same factor (e.g., a password and a PIN) is **Dual-Factor**, not MFA.

### Authenticating `Systems`
Non-human entities (servers, microservices, network gear, IoT devices) authenticate using automated mechanisms:

- **x.509 Digital Certificates (Mutual TLS / mTLS):** Both client and server present TLS certificates signed by a trusted internal CA during the initial TLS handshake to validate mutual identities before establishing an encrypted tunnel.

- **Pre-Shared Keys (PSK):** Static cryptographic strings configured on both endpoints (common in site-to-site IPsec VPNs or WPA3-Personal networks).

- **Kerberos Service Tickets:** Service Principals (SPNs) request Ticket Granting Service (TGS) tickets from a Domain Controller (Key Distribution Center / KDC) to establish machine-to-machine trust without passing raw credentials.

- **API Keys & Managed Identities:** Unique alphanumeric tokens or cloud-native Managed Identities (e.g., AWS IAM Roles, Microsoft Entra Managed Identities) that eliminate hardcoded secrets from source code by pulling temporary credentials from a secure key vault.

### Authorization Models
Authorization determines what resources an authenticated subject can access and what actions they can perform.

**1. Discretionary Access Control (DAC):**
- The resource owner has complete discretion to assign permissions to other users.
- Implementation: NTFS file permissions where a file creator can manually add or remove user permissions via an Access Control Entry (ACE) within the file's Access Control List (ACL).

**2. Mandatory Access Control (MAC):**
- Access is enforced centrally by the operating system based on hardcoded security labels (e.g., Top Secret, Secret, Unclassified) assigned to objects and clearance levels assigned to subjects.
- Implementation: SELinux or TrustedBSD environments enforcing clearance-level matching regardless of file creator preferences.

**3. Role-Based Access Control (RBAC):**
- Access permissions are mapped to specific job roles or group memberships rather than individual user accounts.
- Implementation: Adding a user to an "Active Directory HR-Finance" security group which automatically inherits read/write access to specific network shares.

**4. Attribute-Based Access Control (ABAC):**
- Dynamic evaluation of rules using boolean logic over multiple attributes: 
    - Subject (role, department), 
    - Resource (sensitivity classification), 
    - Action (read, write, delete), and 
    - Environment (time of day, device health, current IP address).
- Implementation: eXtensible Access Control Markup Language (XACML) or cloud zero-trust conditional access policies.

### Accounting
Tracks, records, and logs user activity and consumption of network resources for security monitoring, forensic analysis, and auditing compliance.

Underlying Protocols:
- TACACS+ (Terminal Access Controller Access-Control System Plus): 
    - Cisco proprietary/RFC standard operating over TCP port 49. 
    - Encrypts the entire packet payload (header and data) and strictly separates Authentication, Authorization, and Accounting into distinct processes. 
    - Ideal for network device administration.

- RADIUS (Remote Authentication Dial-In User Service): 
    - Industry-standard protocol operating over UDP ports 1812 (Auth) and 1813 (Acct). 
    - Encrypts only the password field within the packet, leaving the rest of the payload unencrypted.
    - Combines authentication and authorization into a single transaction step.

## 4. Gap Analysis
A Gap Analysis is a structured assessment process that compares an organization's current baseline security posture against a desired target state, framework benchmark, or regulatory compliance standard (e.g., NIST CSF, ISO 27001, PCI-DSS).

```
+-------------------------+       IDENTIFIED GAPS       +------------------------+
|  Current State (As-Is)  | --------------------------> | Target State (To-Be)   |
| Baseline Controls Active|  (Missing Controls, Risk)   | NIST CSF / PCI-DSS     |
+-------------------------+                             +------------------------+
```
Steps in performing a gap analysis:
1. **Define Target Framework:** Select the target compliance framework or baseline standard (e.g., CIS Benchmarks).
2. **Assess Current Controls (As-Is):** Perform audits, interviews, and vulnerability assessments to document active controls.
3. **Identify Discrepancies (Gaps):** Detail control deficiencies, missing policies, or misconfigured technical systems where the current state falls short of the target framework.
4. **Develop Remediation Roadmap:** Prioritize corrective actions based on risk impact, estimate required budget, assign ownership, and establish timeline metrics to close identified gaps.

## 5. Zero Trust Architecture (ZTA)
Zero Trust is an architectural framework built on the fundamental philosophy of "Never Trust, Always Verify." It assumes that threats exist both outside and inside the network perimeter, eliminating implicit trust based on network location.
<br>

- ZTA is divided into 2 sections:
    - Control Plane
    - Data Plane

### Control Plane
The Control Plane serves as the centralized brain of the Zero Trust architecture. It gathers telemetry, evaluates access requests against security policies, and dictates access decisions.

- **Adaptive Identity:** Continually calculates identity risk dynamically using real-time signals (e.g., user behavioral baseline deviations, login location shifts, impossible travel alerts, device health compliance checks) rather than relying on a one-time initial login event.

- **Threat Scope Reduction:** Segments the infrastructure using microsegmentation to isolate workloads into minimal granular trust zones, drastically limiting lateral movement if a single endpoint or account is breached.

- **Policy-Driven Access Control:** Evaluates contextual rules using Attribute-Based Access Control (ABAC) dynamically before issuing access grants.

#### Control Plane Components:

- **Policy Engine (PE):** The core decision-making component of the Control Plane. It ingests identity, device, threat intelligence, and resource attributes to make the ultimate decision to grant, deny, or revoke access to a requested resource.

- **Policy Administrator (PA):** The engine execution component that communicates with the Policy Engine and issues commands to the Policy Enforcement Point (PEP) to open or close communication channels in the data plane (e.g., generating short-lived access tokens or dynamically configuring firewall rules).

![alt text](image.png)

### Data Plane
The Data Plane contains the actual underlying network infrastructure, workload traffic, and resources being accessed. It is explicitly controlled and managed by commands issued from the Control Plane.

- **Implicit Trust Zones:** The shrinking perimeter within a Zero Trust architecture where resources are assumed safe after passing through the Policy Enforcement Point. Modern ZTA reduces implicit trust zones down to individual workloads or microservices.

- **Subject / System:** The client user, endpoint device, service account, or automated software process attempting to access a specific protected resource.

- **Policy Enforcement Point (PEP):** 
    - The operational gateway or inline agent in the Data Plane that sits directly between the Subject and the Target Resource. 
    - It intercepts network traffic, enforces decisions received from the Policy Administrator (e.g., un-suspending a session, establishing an encrypted micro-tunnel, or dropping packets), and continually monitors active sessions.

## 6. Physical Security
Physical security measures protect physical assets, hardware, personnel, and building infrastructure from unauthorized physical access, environmental risks, and physical damage.

### Physical Barriers & Monitoring
- Bollards: Short, heavy-duty concrete or steel posts anchored into the ground outside facility entrances to block vehicle ramming attempts while permitting foot traffic.

- Access Control Vestibule (Mantrap): A specialized physical entryway configured with two interlocking doors where the second door will not unlock until the first door fully closes and locks. Used to prevent tailgating and enforce single-person authentication via badge readers or biometrics.

- Fencing: Physical perimeter barriers designed to deter scaling and delay unauthorized entry. Fencing heights correlate to security levels (e.g., 8-foot fencing topped with barbed wire or razor tape for high-security perimeters).

- Video Surveillance (CCTV): Closed-circuit television networks utilizing IP cameras, infrared night vision, and PTZ (Pan-Tilt-Zoom) capabilities recorded to a Network Video Recorder (NVR) for real-time monitoring and forensic review.

- Security Guard: Human operational guards stationed at access control points to verify credentials, manage visitor logs, check bags, and conduct physical perimeter patrols.

- Access Badge: RFID, NFC, or magnetic stripe smart cards presented to physical badge readers to actuate electronic door strike locks and log entry timestamps into a physical access control database.

- Lighting: Perimeter and entryway illumination engineered to eliminate dark spots, deter trespassers, and ensure adequate light levels for video surveillance camera capture.

### Sensor Technologies
Physical detection systems use different sensing modalities to detect physical intrusion:

#### Infrared Sensors (PIR):

Mechanics: Passive Infrared (PIR) sensors monitor ambient blackbody thermal radiation (heat signatures) within their field of view. When a human body moves across the sensor's baseline thermal grid, the sudden shift in infrared energy trips the alarm circuit.

#### Pressure Sensors:

Mechanics: Uses electromechanical switches, piezoelectric mats, or buried strain-gauge cables under flooring or perimeter grounds. Applying physical weight closes the electrical circuit or alters light wave reflection inside fiber-optic cables to trigger an alert.

#### Microwave Sensors:

Mechanics: Active motion detectors that continuously emit high-frequency radio wave pulses (microwave signals) into an enclosed area. The sensor measures the frequency shift of reflected waves returning to the receiver via the Doppler Effect. Movement alters the return frequency and triggers the alarm. Works through light walls/glass, but susceptible to false positives from external movement.

#### Ultrasonic Sensors:

Mechanics: Active sensors that bounce high-frequency sound waves (inaccessible to human hearing) throughout a room. Changes in the reflected acoustic wave interference pattern caused by moving objects trip the sensor circuit.

## 7. Deception and Disruption Technology
Deception technologies deploy deceptive targets within an enterprise network to lure, identify, divert, and analyze attacker behavior in real time without risking production assets.

```
[ Production Environment ] ------------> (Attacker Probing)
       |                                       |
       v                                       v
[ Isolated Honeynet ] <--- (Diverted) --- [ Honeypot Node ]
       |
       +---> [ Honeyfile (Lure) ] ---> Triggers Alert on Access
       +---> [ Honeytoken (Token) ] --> Alerts SOC when used externally
```

- **Honeypot:** A single non-production network node or server intentionally exposed to attract adversaries. It mimics a vulnerable production system (e.g., an unpatched RDP host) to capture attacker tools, techniques, and procedures (TTPs) while triggering immediate high-fidelity SOC alerts upon any connection attempt.

- **Honeynet:** A complex network segment populated with multiple virtualized honeypots designed to simulate an entire enterprise environment (e.g., fake domain controllers, database servers, and workstations) to study complex multi-stage attacks and lateral movement techniques.

- **Honeyfile:** An enticing, fake file placed on a file share or host system (e.g., Passwords_2026.xlsx or Q3_Financials.pdf). The file contains no legitimate corporate data but is configured with auditing scripts or file access alerts that trigger immediately when opened or modified.

- **Honeytoken:** Fake credentials, fake API keys, embedded canary URLs, or dummy database records inserted quietly into production applications or code repositories. If an attacker exfiltrates and attempts to use the honeytoken (e.g., using a fake AWS API key), the target system flags the credential as a honeytoken and instantly alerts security operations.

# 