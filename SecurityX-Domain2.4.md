# SecurityX (CAS-005) Domain 2.4: Access, Authentication, and Authorization Systems

**Given a scenario, apply security concepts to the design of access, authentication, and authorization systems.**

## 📋 Table of Contents

- [Introduction to Access, Authentication, and Authorization Design](#introduction-to-access-authentication-and-authorization-design)
- [Provisioning and Deprovisioning](#provisioning-and-deprovisioning)
- [Federation and Single Sign-On (SSO)](#federation-and-single-sign-on-sso)
- [Conditional Access and Policy Enforcement](#conditional-access-and-policy-enforcement)
- [Access Control Models](#access-control-models)
- [Logging and Auditing](#logging-and-auditing)
- [Public Key Infrastructure (PKI) Architecture](#public-key-infrastructure-pki-architecture)
- [Access Control Systems](#access-control-systems)
- [Practical Application: Hybrid Enterprise-DoD Scenario](#practical-application-hybrid-enterprise-dod-scenario)
- [Implementation in DoD Environments](#implementation-in-dod-environments)
- [Comparison Tables and Decision Frameworks](#comparison-tables-and-decision-frameworks)
- [Key Resources and Standards](#key-resources-and-standards)

---

## Introduction to Access, Authentication, and Authorization Design

At the SecurityX (CAS-005) level, designing access, authentication, and authorization systems requires a mastery of identity and access management (IAM) principles that balance security, usability, and scalability. This objective tests your ability to architect systems that verify "who you are," control "what you can do," and maintain accountability across complex environments.

**Core Concepts**:
- **Authentication**: Verifying the identity of a user, device, or service (the "who").
- **Authorization**: Determining what actions an authenticated entity is permitted to perform (the "what").
- **Access Control**: The overarching mechanisms that enforce both authentication and authorization.

For new professionals, think of this as the digital equivalent of a high-security building with badge readers, escort requirements, and detailed visitor logs. Advanced practitioners view it through the lens of Zero Trust: never trust, always verify, with continuous evaluation.

In corporate environments, strong IAM supports remote work, cloud adoption, and customer identity management while meeting standards like SOC 2 and GDPR. In DoD environments, these systems are mission-critical, supporting warfighter access under strict controls from RMF, NIST SP 800-53, and the DoD Zero Trust Reference Architecture.

**Strategic Importance**: Poorly designed systems lead to privilege creep, insider threats, and compliance failures. Masters-level designs incorporate automation, least privilege, and resilience against modern threats like credential stuffing and session hijacking.

---

## Provisioning and Deprovisioning

### Provisioning
**Definition**: The process of creating, configuring, and issuing identities and access rights to users, devices, or services. New professionals: This is onboarding someone into the system. Advanced users: It involves automated workflows, role mapping, and integration with HR or asset management systems.

**Credential Issuance**:
- Corporate: Automated account creation in Active Directory or Okta with temporary credentials and mandatory MFA enrollment.
- DoD: Issuance of Common Access Cards (CAC) or Derived Credentials with PKI certificates, tied to background investigations.

**Self-Provisioning**:
**Definition**: Allowing users to request and receive access through automated portals with approval workflows.
- Corporate Application: Service catalog tools like ServiceNow where developers self-onboard to cloud resources with automated approvals.
- DoD Application: Limited use due to strict controls; often requires ISSO review within eMASS for RMF compliance.

### Deprovisioning
**Definition**: The timely revocation of access when users depart, change roles, or devices are retired. This is critical for preventing orphaned accounts.

**Best Practices**:
- Automated triggers from HR systems.
- Just-in-time (JIT) access for privileged accounts.
- Comprehensive audit trails for all changes.

**Corporate Application**: Integration with offboarding workflows that disable accounts within hours.
**DoD Application**: Mandatory within 24-72 hours per policy, with verification during CCRI/CORA inspections.

---

## Federation and Single Sign-On (SSO)

### Federation
**Definition**: The sharing of identity information across security domains or organizations using standardized protocols. New professionals: It allows users from one company to access resources in another without creating new accounts. Advanced: It relies on trust relationships and assertions.

**Corporate Application**: SAML 2.0 or OpenID Connect for partner ecosystems and B2B collaborations.
**DoD Application**: Federated identity with coalition partners using DoD PKI and ICAM Reference Design. `https://dodcio.defense.gov/`

### Single Sign-On (SSO)
**Definition**: A mechanism that allows users to authenticate once and gain access to multiple applications without re-entering credentials.

**Implementation Considerations**:
- Reduced password fatigue and helpdesk load.
- Increased risk if the SSO provider is compromised (mitigated by strong MFA and session monitoring).

**Corporate Application**: Okta, Azure AD, or Ping Identity for enterprise SaaS integration.
**DoD Application**: Enterprise SSO supporting CAC/PKI authentication across DoDIN systems.

---

## Conditional Access and Policy Enforcement

### Conditional Access
**Definition**: Dynamic access decisions based on real-time context such as user location, device posture, time, and risk score.

**Corporate Application**: Microsoft Entra Conditional Access policies that block access from high-risk countries or non-compliant devices.
**DoD Application**: Context-aware controls in tactical environments, integrating with Zero Trust pillars.

### Identity Provider (IdP)
**Definition**: The system responsible for authenticating users and providing identity assertions to relying parties. New professionals: The "source of truth" for login. Advanced: Centralizes authentication logic and supports multiple protocols.

**Examples**: Azure AD, Okta, or DoD's Identity, Credential, and Access Management (ICAM) systems.

### Service Provider (SP)
**Definition**: The application or resource that relies on the IdP for authentication and receives authorization attributes.

### Attestations
**Definition**: Cryptographic proofs or claims about the state of a user, device, or system (e.g., "this device is patched and compliant").

**Corporate Application**: Device health attestations in Zero Trust Network Access (ZTNA).
**DoD Application**: Hardware Root of Trust using TPMs for platform attestations.

### Policy Decision Point (PDP) and Policy Enforcement Point (PEP)
**Definition**:
- **PDP**: Evaluates policies and makes allow/deny decisions.
- **PEP**: Enforces the decisions made by the PDP (e.g., at network gateways or application layers).

**Corporate Application**: Implemented in cloud access security brokers (CASB) and micro-segmentation tools.
**DoD Application**: Critical in SASE architectures and enclave boundary protection.

---

## Access Control Models

### Role-Based Access Control (RBAC)
**Definition**: Access granted based on predefined roles within the organization. New professionals: "If you are a manager, you get these permissions." Advanced: Supports role hierarchies and separation of duties (SoD).

**Corporate Application**: Standard in enterprise HR and financial systems.
**DoD Application**: Widely used but often combined with other models for finer control.

### Rule-Based Access Control
**Definition**: Decisions based on specific rules or conditions (e.g., time-based or location-based).

### Attribute-Based Access Control (ABAC)
**Definition**: Dynamic access based on attributes of users, resources, actions, and environment. Masters-level choice for complex, data-centric environments.

**Corporate Application**: Fine-grained policies in cloud platforms using tags and attributes.
**DoD Application**: Aligns with DoD Zero Trust and data-centric security.

### Mandatory Access Control (MAC)
**Definition**: System-enforced access based on security labels and clearances. Highly rigid.

**DoD Application**: Dominant in classified systems using Bell-LaPadula or Biba models.

### Discretionary Access Control (DAC)
**Definition**: Owners of resources decide who gets access (e.g., file permissions in Windows/Linux).

**Corporate Application**: Common in collaborative file shares.
**DoD Application**: Limited use due to need for centralized control.

---

## Logging and Auditing

**Definition**: Systematic recording of security-relevant events for accountability, forensics, and compliance.

**Corporate Application**: Centralized SIEM with immutable logs and AI-assisted review.
**DoD Application**: Required under CJCSM 6510.01B and RMF control AU family. Feeds into enterprise monitoring platforms.

**Best Practices**:
- Capture who, what, when, where, and how.
- Protect log integrity with hashing and WORM storage.
- Regular log review and correlation.

---

## Public Key Infrastructure (PKI) Architecture

**Definition**: The framework for managing digital certificates and public-key encryption to support authentication, integrity, and confidentiality.

### Certificate Extensions
**Definition**: Additional fields in X.509 certificates that define usage constraints and policies.

### Certificate Types
- Client certificates, server certificates, code-signing, etc.

### Online Certificate Status Protocol (OCSP) Stapling
**Definition**: A method to improve TLS performance by having servers provide real-time revocation status.

### Certificate Authority/Registration Authority (CA/RA)
**Definition**: CA issues certificates; RA verifies requester identity.

**Corporate Application**: Internal CAs with automated issuance via ACME protocol.
**DoD Application**: DoD PKI with External Certificate Authorities and strict chain of trust. `https://public.cyber.mil/pki-pke/`

### Templates
**Definition**: Predefined certificate profiles for consistency and compliance.

### Deployment/Integration Approach
- Integration with directory services, S/MIME, and VPNs.
- Considerations for certificate lifecycle management and revocation.

---

## Access Control Systems

### Physical Access Control
**Definition**: Controls over physical entry to facilities, including badges, biometrics, and mantraps.

**Corporate Application**: Integrated with logical systems for badge-based workstation login.
**DoD Application**: SCIF requirements and anti-tailgating measures.

### Logical Access Control
**Definition**: Controls over digital resources, including passwords, tokens, and biometrics.

**Integration**: Modern designs converge physical and logical controls through unified IAM platforms.

---

## Practical Application: Hybrid Enterprise-DoD Scenario

**Scenario**: A defense contractor needs secure access for employees working across commercial cloud tools and classified DoD systems.

**Design Solution**:
- Federation and SSO using SAML/OpenID Connect with CAC as primary credential.
- Conditional Access based on device attestation, location, and risk score.
- ABAC policies for CUI data access.
- PKI integration for mutual TLS and code signing.
- Comprehensive logging to a SIEM with automated auditing.

**Outcome**: Seamless yet secure access while maintaining strict compliance.

---

## Implementation in DoD Environments

DoD prioritizes **ICAM** (Identity, Credential, and Access Management) and integration with the DoD Zero Trust Reference Architecture. Key elements include CAC/PKI dominance, attribute-based controls, and continuous monitoring.

- DoD ICAM Reference Design
- NIST SP 800-63 Digital Identity Guidelines
- RMF control families (IA, AC, AU)

**RACI Integration**: ISSO responsible for implementation details, Authorizing Official accountable for overall risk.

---

## Comparison Tables and Decision Frameworks

**Access Control Models Comparison**:

| Model | Granularity | Administration | Use Case | Corporate Example | DoD Example |
|-------|-------------|----------------|----------|-------------------|-------------|
| RBAC | Medium | Low | Role-centric orgs | Enterprise HR systems | Basic command access |
| ABAC | High | Medium-High | Dynamic environments | Cloud data lakes | Data-centric CUI protection |
| MAC | Very High | High | High-security | Rare | Classified enclaves |
| DAC | Low | Low | Collaborative | File shares | Limited tactical use |

**Authentication Methods Trade-offs**:

| Method | Security | Usability | Scalability | Corporate | DoD |
|--------|----------|-----------|-------------|-----------|-----|
| Password + MFA | Medium | Medium | High | Standard | Baseline |
| PKI/CAC | High | Low-Medium | Medium | VPNs | Primary |
| Passwordless (FIDO2) | High | High | High | Modern apps | Emerging |

**PKI Component Responsibilities**:

| Component | Role | Corporate Focus | DoD Focus |
|-----------|------|-----------------|-----------|
| CA | Issuance | Internal trust | Rooted in DoD PKI hierarchy |
| RA | Verification | Automation | Background checks |
| OCSP | Revocation | Performance | High-assurance checks |

---

## Key Resources and Standards

- NIST SP 800-63-3: `https://pages.nist.gov/800-63-3/`
- DoD Zero Trust Reference Architecture: `https://dodcio.defense.gov/`
- NIST SP 800-53 AC/IA Controls: `https://csrc.nist.gov/publications/sp/800/53`
- OWASP Authentication Cheat Sheet
- DoD PKI: `https://public.cyber.mil/pki-pke/`
