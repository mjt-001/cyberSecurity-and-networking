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

