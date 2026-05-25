# SecurityX (CAS-005) Domain 2.1: Resilient Systems Design

**Given a scenario, analyze requirements to design resilient systems.**

## 📋 Table of Contents

- [Introduction to Resilient Systems Design](#introduction-to-resilient-systems-design)
- [Component Placement and Configuration](#component-placement-and-configuration)
- [Detailed Component Breakdown](#detailed-component-breakdown)
- [Availability and Integrity Design Considerations](#availability-and-integrity-design-considerations)
- [Practical Application: Hybrid Enterprise-DoD Scenario](#practical-application-hybrid-enterprise-dod-scenario)
- [Component Placement in DoD Environments](#component-placement-in-dod-environments)
- [Resilience Frameworks and Standards](#resilience-frameworks-and-standards)
- [Design Trade-offs and Decision Matrices](#design-trade-offs-and-decision-matrices)
- [Emerging Technologies in Resilient Design](#emerging-technologies-in-resilient-design)

---

## Introduction to Resilient Systems Design

Resilient systems design focuses on creating architectures that maintain confidentiality, integrity, and availability (CIA triad) even when facing failures, attacks, or unexpected loads. For SecurityX (CAS-005) candidates, this objective tests your ability to translate business and mission requirements into secure, fault-tolerant placements of security components.

**Core Principles:**
- **Defense-in-Depth**: Multiple overlapping controls rather than single points of failure.
- **Zero Trust Mindset**: Assume breach and verify every access.
- **Continuous Resilience**: Design for graceful degradation and rapid recovery.

In corporate environments, resilience supports business continuity and regulatory compliance (e.g., SOX, GDPR). In DoD environments, it directly supports mission assurance under frameworks like the Risk Management Framework (RMF) and DoDI 8500.01.

---

## Component Placement and Configuration

Security architects must strategically position and configure controls based on network topology, data sensitivity, threat model, and performance requirements. Placement decisions balance security, usability, and operational overhead.

### Detailed Component Breakdown

#### Firewall
**Definition**: A network security device that monitors and controls incoming and outgoing traffic based on predetermined security rules. Next-generation firewalls (NGFW) add deep packet inspection, application awareness, and threat intelligence integration.

**Corporate Application**: Place perimeter firewalls at the internet edge (`edge firewall`) and internal segmentation firewalls between business units. Example configuration: Palo Alto or Cisco Firepower with URL filtering and IPS integration.

**DoD Application**: Boundary protection per DoDI 8510.01 and STIGs. Use firewalls as part of the DoD Information Network (DoDIN) boundary. High Assurance Internet Protocol Encryptor (HAIPE) devices often complement traditional firewalls for classified enclaves.

**Key Configuration Considerations**:
- Rule ordering (most specific first)
- Logging to a central SIEM
- High availability (active/active or active/passive clusters)

#### Intrusion Prevention System (IPS)
**Definition**: An inline security appliance or software that actively blocks detected threats by analyzing traffic in real-time.

**Corporate Application**: Deploy IPS behind the firewall in the DMZ or at critical internal chokepoints. Tune for low false positives to avoid disrupting business applications.

**DoD Application**: Integrated into boundary protection and enclave defenses. DISA STIGs require specific IPS signatures and sensor placement for Command Cyber Readiness Inspection (CCRI) compliance.

#### Intrusion Detection System (IDS)
**Definition**: A monitoring system that alerts on suspicious activity but does not block (out-of-band placement).

**Corporate Application**: Use network-based IDS (NIDS) for broad visibility and host-based IDS (HIDS) on critical servers. Common tools: Snort or Suricata.

**DoD Application**: Often combined with IPS in a single platform. Sensors feed into the Joint Regional Security Stacks (JRSS) for centralized analysis.

#### Vulnerability Scanner
**Definition**: Automated tool that identifies weaknesses in systems, applications, and networks.

**Corporate Application**: Deploy agents or authenticated scans from internal servers. Schedule weekly scans with credentialed access for accurate results.

**DoD Application**: Mandatory under IAVM program. Integrate with eMASS and use tools approved under the DoD Vulnerability Management program.

#### Virtual Private Network (VPN)
**Definition**: Creates encrypted tunnels for secure remote access over untrusted networks.

**Corporate Application**: Client-to-site VPN for remote workers, site-to-site for branch offices. Modern implementations favor SSL/TLS VPNs over legacy IPsec.

**DoD Application**: DoD uses VPNs with CAC authentication and complies with DoD Cloud SRG for Impact Level 4/5. SASE architectures increasingly replace traditional VPN concentrators.

#### Network Access Control (NAC)
**Definition**: Enforces policy on devices attempting to connect to the network, checking posture (patch level, antivirus status, etc.).

**Corporate Application**: 802.1X with RADIUS for wired/wireless. Posture assessment before granting full access.

**DoD Application**: Critical for preventing rogue devices on tactical and garrison networks. Integrates with RMF continuous monitoring.

#### Web Application Firewall (WAF)
**Definition**: Protects web applications by filtering and monitoring HTTP/HTTPS traffic.

**Corporate Application**: Placed in front of web servers or as cloud WAF (e.g., AWS WAF, Cloudflare). Protects against OWASP Top 10 threats.

**DoD Application**: Required for public-facing applications handling CUI. Often virtualized within cloud environments per DoD Cloud SRG.

#### Proxy
**Definition**: Intermediary that forwards client requests to servers, providing anonymity, caching, and content filtering.

**Corporate Application**: Forward proxies for outbound traffic control and user monitoring.

#### Reverse Proxy
**Definition**: Sits in front of backend servers, handling incoming requests, load distribution, and SSL termination.

**Corporate Application**: Used with WAF capabilities (e.g., NGINX, HAProxy).

**DoD Application**: Common in DMZ architectures to shield internal application servers.

#### Application Programming Interface (API) Gateway
**Definition**: Manages, secures, and optimizes API traffic with authentication, rate limiting, and transformation.

**Corporate Application**: Essential for microservices architectures (e.g., Kong, AWS API Gateway).

**DoD Application**: Protects mission-critical APIs in joint systems. Enforces OAuth2/OpenID Connect with DoD PKI.

#### Taps (Test Access Points)
**Definition**: Passive network devices that copy traffic for monitoring without introducing latency.

**Corporate Application**: Used for out-of-band IDS/IPS and network forensics.

**DoD Application**: Required for full visibility in high-security enclaves without disrupting operational traffic.

#### Collectors
**Definition**: Agents or appliances that gather logs, metrics, and telemetry from various sources.

**Corporate Application**: Syslog collectors, NetFlow collectors feeding into SIEM.

**DoD Application**: Feeds into Big Data platforms and JRSS for enterprise visibility.

#### Content Delivery Network (CDN)
**Definition**: Distributed network of servers that delivers content with low latency and high availability.

**Corporate Application**: Protects against DDoS and improves global performance (e.g., Akamai, Cloudflare).

**DoD Application**: Approved CDNs for unclassified content. Impact Level considerations for CUI.

---

## Availability and Integrity Design Considerations

### Load Balancing
**Definition**: Distributes network or application traffic across multiple servers to ensure no single server becomes overwhelmed.

**Types**:
- **Layer 4 (Transport)**: Based on IP and port.
- **Layer 7 (Application)**: Content-aware routing.

**Corporate Application**: Global Server Load Balancing (GSLB) for multi-region deployments.

**DoD Application**: Essential for mission systems requiring 99.999% uptime. Integrates with DoD cloud environments.

### Recoverability
**Definition**: The ability to restore systems and data after an outage or attack.

**Design Elements**:
- Backups (3-2-1 rule: 3 copies, 2 media types, 1 offsite)
- Immutable backups
- Automated failover and orchestration

**Corporate Application**: RTO/RPO targets based on business impact analysis.

**DoD Application**: Aligns with COOP (Continuity of Operations) and disaster recovery requirements under RMF.

### Interoperability
**Definition**: Ensuring components from different vendors or systems work together seamlessly.

**Corporate Application**: Use of open standards (e.g., SAML, OAuth) and API-first designs.

**DoD Application**: Critical due to joint and coalition operations. Adherence to DISA standards and STIGs.

### Geographical Considerations
**Definition**: Accounting for physical location, latency, data sovereignty, and disaster risks.

**Strategies**:
- Multi-region deployments
- Geo-redundancy
- Data residency compliance

**Corporate Application**: Compliance with GDPR data localization.

**DoD Application**: IL5/IL6 cloud requirements and tactical edge computing considerations.

### Vertical vs. Horizontal Scaling
**Vertical Scaling** (Scale Up): Adding resources to a single instance (more CPU/RAM).

**Horizontal Scaling** (Scale Out): Adding more instances.

**Corporate Application**: Cloud-native applications favor horizontal scaling with auto-scaling groups.

**DoD Application**: Horizontal preferred for resilience in contested environments.

### Persistence vs. Non-Persistence
**Definition**:
- **Persistent**: Data and configurations survive reboots.
- **Non-Persistent**: Ephemeral environments that reset to a known good state.

**Corporate Application**: Non-persistent VDI for high-security desktops.

**DoD Application**: Heavily used in tactical and high-threat environments to reduce attack surface (e.g., stateless thin clients).

---

## Practical Application: Hybrid Enterprise-DoD Scenario

**Scenario**: A defense contractor operates a hybrid environment supporting both commercial contracts and DoD programs handling CUI.

**Requirements Analysis**:
- Protect CUI while maintaining performance for R&D teams.
- Ensure 99.95% availability for mission applications.
- Comply with NIST SP 800-171 and DFARS 252.204-7012.

**Design Decisions**:
1. **Perimeter**: NGFW + Cloud WAF + CDN for public interfaces.
2. **Internal Segmentation**: Micro-segmentation with zero-trust policies.
3. **Remote Access**: SASE-based ZTNA replacing traditional VPN.
4. **Monitoring**: Taps and collectors feeding a SIEM with AI-driven anomaly detection.
5. **Resilience**: Active-active load balancers across two availability zones, immutable backups, and automated recovery orchestration.

**RACI Integration**: Security Architect accountable for design, ISSO consulted on RMF controls.

---

## Component Placement in DoD Environments

DoD architectures emphasize **enclave boundaries**, **cross-domain solutions**, and **mission thread analysis**. Key references:

- `https://www.cyber.mil/stigs` (DISA STIGs)
- DoDI 8510.01 (RMF)
- DoD Zero Trust Reference Architecture
- `https://public.cyber.mil/` (public DoD cyber resources)

**Common Patterns**:
- High-to-Low guards for cross-domain transfers.
- JRSS for centralized boundary protection.
- eMASS for documenting component configurations within Authorization Packages.

---

## Resilience Frameworks and Standards

| Framework/Standard | Focus | Relevance to CAS-005 |
|--------------------|-------|----------------------|
| NIST SP 800-160 | Systems Security Engineering | Holistic resilient design |
| NIST SP 800-53 (Control Families: CP, SI) | Contingency Planning & System Integrity | Mandatory controls |
| DoD Cloud SRG | Cloud resilience | Impact Level guidance |
| ISO 22301 | Business Continuity | Corporate alignment |

---

## Design Trade-offs and Decision Matrices

Architects use decision matrices weighing factors like:

- Cost vs. Security
- Performance vs. Resilience
- Complexity vs. Maintainability

**Example Matrix for IPS Placement**:

| Placement | Pros | Cons | Use Case |
|-----------|------|------|----------|
| Inline (Prevention) | Active blocking | Latency risk | High-security perimeter |
| Passive (Detection) | No performance impact | Delayed response | Monitoring internal segments |

---

## Emerging Technologies in Resilient Design

- **SASE and SSE**: Converged networking and security.
- **AI/ML for Anomaly Detection**: Dynamic threat response.
- **Immutable Infrastructure**: Infrastructure as Code (IaC) with GitOps.
- **Quantum-Resistant Cryptography**: For long-term integrity.
- **Digital Twins**: Simulating resilience before deployment.

**DoD Focus**: Alignment with DoD Digital Engineering Strategy and Joint All-Domain Command and Control (JADC2).
