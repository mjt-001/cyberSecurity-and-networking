# Security Architecture

## Objective 3.1: `Architecture Models & Infrastructure Concepts`

### Overview & Mechanics
Architecture models and infrastructure concepts define how modern systems, networks, applications, and physical devices are designed, deployed, scaled, and secured. These architectures is vital because security posture shifts dramatically depending on where compute power resides, how networks are segmented, whether infrastructure is managed via code, and how specialized or resource-constrained devices are protected against evolving threat landscapes.

#### Security Implications
1. **Confidentiality:** Architecture models dictate data boundaries, multi-tenancy risks, encryption states (data-at-rest, in-transit, and in-use), and access control granularity. Misconfigurations in cloud shared responsibility, loose logical segmentation, or unencrypted container registries directly compromise confidentiality.
2. **Integrity:** Ensuring systems, code bases, and physical environments have not been tampered with. Infrastructure as Code (IaC) pipelines, immutable infrastructure, and secure boot for embedded/IoT systems protect operational integrity against unauthorized modifications and supply chain injections.
3. **Availability:** High availability, redundancy, fault tolerance, and resilience models ensure business continuity. Single points of failure, unpatched real-time operating systems (RTOS), and distributed denial-of-service (DDoS) vulnerabilities in IoT/ICS environments threaten critical operational availability.

### A. Cloud Architecture & Models
- **Responsibility Matrix (Shared Responsibility Model):** 
  - *IaaS (Infrastructure as a Service):* The cloud service provider (CSP) secures the underlying physical hardware, data center facilities, and hypervisor. The customer is responsible for guest operating systems, network configurations, identity and access management (IAM), patches, and data security.
  - *PaaS (Platform as a Service):* The CSP manages the underlying infrastructure, operating systems, and runtime environments. The customer manages application code, data, and user access configurations.
  - *SaaS (Software as a Service):* The CSP manages virtually the entire stack (infrastructure, application, runtime, storage). The customer is primarily responsible for data governance, user authentication, and endpoint access controls.
- **Hybrid Considerations:** Combining on-premises infrastructure with public and/or private clouds. Security challenges include maintaining consistent security policies across disparate environments, securing hybrid connectivity (VPNs, Direct Connect/ExpressRoute), managing complex identity federation (e.g., SAML, OAuth, Azure AD/Entra ID), and visibility gaps across boundaries.
- **Third-Party Vendors:** Assessing vendor risk, supply chain security, compliance frameworks (SOC 2, ISO 27001), service level agreements (SLAs), and offboarding/data destruction procedures when relying on external cloud and SaaS providers.

### B. Infrastructure as Code (IaC)
- **Mechanics:** The management and provisioning of computing infrastructure (servers, networks, storage) through machine-readable definition files (code) rather than physical hardware configuration or interactive configuration tools. Examples include Terraform, AWS CloudFormation, and Ansible.
- **Security Implications:** 
  - *Version Control and Auditing:* Changes to infrastructure are tracked in Git repositories, allowing for code reviews and rollback capabilities.
  - *Security Misconfigurations:* Hardcoded credentials, overly permissive security groups, or public S3 bucket policies written into IaC scripts can automate vulnerability deployment at scale if not scanned early.
  - *Static Analysis:* Implementing security linters (e.g., Checkov, tfsec) in CI/CD pipelines to catch misconfigurations before deployment (Shift-Left security).

### C. Serverless Architecture
- **Mechanics:** A cloud-computing execution model where the cloud provider dynamically allocates and manages machine resources, abstracting server management away from the developer. Code runs in stateless containerized functions (e.g., AWS Lambda, Azure Functions) triggered by events.
- **Security Implications:** 
  - *Reduced OS-level Attack Surface:* Customers do not manage operating systems, eliminating traditional OS patching burdens.
  - *IAM and Least Privilege:* Functions require tightly scoped execution roles; over-permissioned service accounts can lead to widespread compromise if a function is exploited.
  - *Injection and Event Data Validation:* Security relies heavily on strict input validation because functions process arbitrary external event payloads.

### D. Microservices Architecture
- **Mechanics:** An architectural style that structures an application as a collection of loosely coupled, independently deployable services organized around specific business capabilities, communicating typically via lightweight APIs (e.g., REST, gRPC).
- **Security Implications:** 
  - *Increased Attack Surface:* Each microservice has its own entry points, dependencies, and APIs, increasing the overall attack surface.
  - *Service-to-Service Authentication:* Requires robust zero-trust mechanisms (mTLS, service meshes like Istio) to authenticate and encrypt traffic moving east-west across internal network boundaries.
  - *Supply Chain Risks:* Heavy reliance on third-party software libraries and container base images for individual services.

### E. Network Infrastructure Isolation & Segmentation
- **Physical Isolation (Air-gapped):** Networks or systems that are physically disconnected from any unsecured networks (such as the public internet) and other network nodes. Used for critical national infrastructure, military systems, and high-security R&D environments.
- **Logical Segmentation:** Dividing a physical network into smaller virtual networks (VLANs, subnets, software-defined perimeters) using routers, firewalls, and access control lists (ACLs) to restrict lateral movement during a breach.
- **Software-Defined Networking (SDN):** An approach to network management that enables dynamic, programmatically efficient network configuration and routing decoupled from underlying physical hardware (separating the control plane from the data plane). Enhances security through centralized policy enforcement, micro-segmentation, and rapid automated response to security incidents.

### F. On-Premises Architecture
- **Mechanics:** Traditional deployment model where computing hardware, data storage, and networking equipment are housed locally within an organization's own data center facility.
- **Security Implications:** 
  - *Full Control & Responsibility:* Organization maintains complete ownership and physical control over hardware, physical security, access logs, and data residency.
  - *Physical Security Dependency:* Relies heavily on physical access controls (guards, biometric entry, server rack locks, CCTV).
  - *Maintenance Overhead:* Requires internal resources for hardware procurement, physical lifecycle replacement, manual patching, and facility environmental controls (HVAC, fire suppression).

### G. Centralized vs. Decentralized Models
- **Centralized:** Security controls, policies, identity management, logging, and incident response are managed from a single focal point (e.g., a central SOC or master domain controller). Offers high visibility and consistent policy enforcement, but represents a single point of failure and high-value target.
- **Decentralized:** Authority, data storage, and compute resources are distributed across multiple business units, branches, or nodes (e.g., edge computing, decentralized autonomous architectures). Improves localized resilience and autonomy, but increases the risk of configuration drift, shadow IT, and fragmented logging/monitoring.

### H. Containerization
- **Mechanics:** Operating system-level virtualization method used to deploy and run distributed applications without launching an entire virtual machine for each application. Containers share the host OS kernel while isolating application processes (e.g., Docker, Kubernetes).
- **Security Implications:** 
  - *Kernel Exploitation:* Because containers share the host kernel, a kernel vulnerability can compromise all containers running on that host.
  - *Image Vulnerabilities:* Vulnerabilities in base images or third-party packages included in container layers. Requires runtime security monitoring and container image scanning.
  - *Namespace and Cgroup Isolation:* Misconfigured security contexts or running containers with root privileges inside the container can allow container breakout attacks.

### I. Virtualization
- **Mechanics:** The creation of a virtual (rather than actual) version of something, such as a hardware platform, OS, storage device, or network resources, managed by a hypervisor (Type 1 Bare-Metal or Type 2 Hosted).
- **Security Implications:** 
  - *Hypervisor Escape:* A vulnerability allowing malicious guest VMs to break out of isolation and execute code on the host hypervisor or other guest VMs.
  - *VM Sprawl:* Rapid, unmanaged proliferation of virtual machines leading to unpatched systems, forgotten assets, and visibility gaps.
  - *Snapshot Security:* Unencrypted VM snapshots containing sensitive memory data, credentials, and configuration files left exposed in storage.

### J. Internet of Things (IoT)
- **Mechanics:** Network of physical objects ("things") embedded with sensors, software, and other technologies for the purpose of connecting and exchanging data with other devices and systems over the internet (e.g., smart office devices, environmental sensors, medical IoT).
- **Security Implications:** 
  - *Weak Authentication:* Default hardcoded passwords, lack of multi-factor authentication, and insecure management interfaces.
  - *Patching Challenges:* Many IoT devices lack mechanisms for firmware updates, resulting in long-term vulnerability exposure (lifecycle issues).
  - *Botnet Recruitment:* Frequently targeted by malware (e.g., Mirai) to enlist devices into large-scale DDoS attacks.

### K. Industrial Control Systems (ICS) / SCADA
- **Mechanics:** Specialized control systems used in industrial environments (manufacturing, water treatment, electrical grids, oil and gas). SCADA (Supervisory Control and Data Acquisition) systems gather real-time data from remote plants to control equipment and conditions.
- **Security Implications:** 
  - *Availability Priority:* In ICS/SCADA, Availability (A) is paramount above Confidentiality (C) and Integrity (I); shutting down a process for emergency patching can cause catastrophic physical or economic damage.
  - *Legacy Hardware & Protocols:* Many ICS networks use decades-old proprietary protocols lacking encryption or authentication.
  - *Air-Gap Fallacy:* Historically assumed to be isolated from enterprise networks, modern convergence with IT networks (IT/OT convergence) has introduced severe cyber-attack vectors (e.g., Stuxnet, ransomware targeting operational technology).

### L. Real-Time Operating Systems (RTOS)
- **Mechanics:** An operating system intended to serve real-time applications that process data as it comes in, typically without buffer delays. Used in critical embedded systems, aerospace, automotive braking systems, and medical devices where deterministic timing is required.
- **Security Implications:** 
  - *Resource Constraints:* Limited CPU and memory prevent the implementation of heavy security agents, complex encryption algorithms, or robust endpoint detection and response (EDR) tools.
  - *Deterministic Timing Vulnerabilities:* Security patches or logging mechanisms that introduce latency can cause system failure or missed deadlines in safety-critical loops.

### M. Embedded Systems
- **Mechanics:** Computer systems with a dedicated function within a larger mechanical or electrical system, often featuring real-time computing constraints (e.g., routers, automotive ECUs, smart appliances, industrial robots).
- **Security Implications:** 
  - *Firmware Integrity:* Risk of malicious firmware flashing, lack of cryptographic secure boot mechanisms.
  - *Limited Cryptographic Support:* Insufficient hardware capabilities to support modern TLS/encryption standards.
  - *Physical Tampering:* Devices are often deployed in unattended physical locations, exposing them to hardware-level debugging interfaces (JTAG, UART) and side-channel attacks.

### N. High Availability (HA)
- **Mechanics:** Systems designed to operate continuously for a long period without failure, achieved through redundancy, failover mechanisms, load balancing, and fault tolerance across components, data centers, or cloud regions.
- **Security Implications:** 
  - *Complex Replication Security:* Replicating data across multiple geographic locations or redundant nodes expands the data attack surface and complicates compliance with data residency laws.
  - *Failover Vulnerabilities:* During failover scenarios, security controls (such as stateful firewalls or authentication tokens) might drop or fail to synchronize, potentially allowing unauthorized access or unmonitored traffic flow.
  - *Denial of Service Resilience:* High availability architectures mitigate availability risks from hardware failures and localized DDoS attacks, maintaining operational resilience.

---
### Architectural & Operational Considerations for Secure Design

### Overview & Mechanics
When designing secure enterprise networks, cloud environments, and hybrid infrastructures, security professionals must balance security controls with operational and environmental constraints. Architectural decisions are rarely driven by security alone; cost, power, compute limitations, and business agility dictate how systems are built. These are core operational considerations directly impact your overall security posture and risk management strategy.

### Core Architectural Considerations

1. **Availability**
   - **Mechanics:** Ensuring that systems, network links, data, and applications are accessible to authorized users whenever required.
   - **Security Impact:** Unplanned downtime impacts business operations, while denial-of-service (DoS) attacks specifically target availability. Achieved through redundancy, clustering, failover mechanisms, and robust incident response.

2. **Resilience**
   - **Mechanics:** The capacity of a system or network to withstand, absorb, recover from, and adapt to adverse conditions, disruptions, or active cyber attacks without catastrophic failure.
   - **Security Impact:** Unlike mere fault tolerance, resilience assumes breaches or failures will happen and focuses on maintaining core functionality under fire and bouncing back rapidly.

3. **Cost**
   - **Mechanics:** The total financial expenditure required to design, procure, implement, maintain, and secure an architecture (including Capital Expenditure [CapEx] vs. Operating Expenditure [OpEx]).
   - **Security Impact:** Budget constraints often force security compromises. Security architects must perform risk-benefit analyses to ensure high-value assets receive adequate protection without creating unsustainable financial overhead.

4. **Responsiveness**
   - **Mechanics:** The speed and low-latency performance with which a system processes requests, interacts with users, or reacts to security events and telemetry.
   - **Security Impact:** Crucial for real-time security operations (SIEM/SOAR alert response, DDoS mitigation, intrusion prevention systems) and user experience. High latency can compromise time-sensitive applications.

5. **Scalability**
   - **Mechanics:** The ability of an architecture to seamlessly grow or shrink its capacity (compute, storage, bandwidth) to handle fluctuating workloads.
   - **Security Impact:** Vertical scaling (adding resources to a single node) vs. horizontal scaling (adding more nodes). Automated scaling must incorporate automated security provisioning (e.g., dynamic security groups, automated certificate issuance) to avoid security gaps during traffic spikes.

6. **Ease of Deployment**
   - **Mechanics:** The speed, simplicity, and repeatability with which new infrastructure, applications, or patches can be rolled out across an organization.
   - **Security Impact:** Tied closely to Infrastructure as Code (IaC) and CI/CD pipelines. Streamlined deployments reduce human configuration errors and ensure consistent security baseline enforcement across environments.

7. **Risk Transference**
   - **Mechanics:** Shifting the financial or operational burden of a potential risk to a third party.
   - **Security Impact:** Common examples include purchasing cyber insurance, outsourcing managed security services (MSSP), or leveraging cloud provider compliance frameworks. Note that while financial impact is transferred, ultimate organizational and legal accountability remains with the enterprise.

8. **Ease of Recovery**
   - **Mechanics:** How quickly and easily systems and data can be restored to a secure, operational state following a failure, disaster, or ransomware attack.
   - **Security Impact:** Measured by Recovery Time Objective (RTO) and Recovery Point Objective (RPO). Immutable backups, automated snapshotting, and well-tested disaster recovery runbooks directly reduce dwell time and operational disruption.

9. **Patch Availability**
   - **Mechanics:** The frequency, reliability, and promptness with which software vendors release security updates, bug fixes, and firmware updates for known vulnerabilities.
   - **Security Impact:** Essential for maintaining vulnerability management lifecycles. Open-source or actively supported vendor products offer rapid patch availability, closing windows of exposure quickly.

10. **Inability to Patch**
    - **Mechanics:** Scenarios where systems cannot be updated due to legacy dependencies, proprietary software, proprietary hardware constraints, or continuous uptime requirements (common in ICS/SCADA and embedded medical devices).
    - **Security Impact:** Requires compensating controls, such as strict network segmentation, air-gapping, virtual patching via web application firewalls (WAF), host-based intrusion detection, and strict egress/ingress filtering.

11. **Power**
    - **Mechanics:** The physical electrical requirements and power continuity (UPS, dual power supplies, backup diesel generators) needed to keep data centers and hardware operational.
    - **Security Impact:** Power loss causes immediate availability failures. Environmental monitoring (temperature, humidity, power draw) protects against physical hardware degradation and environmental attacks.

12. **Compute**
    - **Mechanics:** The processing power (CPU cores, RAM, GPU capacity) available to run workloads, cryptographic operations, virtualization layers, and security analytics.
    - **Security Impact:** Insufficient compute resources can prevent the execution of heavy security controls like full-disk encryption, complex multi-factor authentication, deep packet inspection, and EDR agents.