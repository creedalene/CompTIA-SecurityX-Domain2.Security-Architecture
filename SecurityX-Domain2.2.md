# SecurityX (CAS-005) Domain 2.2: Security in the Systems Life Cycle

**Given a scenario, implement security in the early stages of the systems life cycle and throughout subsequent stages.**

## 📋 Table of Contents

- [Introduction to Secure Systems Development Life Cycle (SDLC)](#introduction-to-secure-systems-development-life-cycle-sdlc)
- [Security Requirements Definition](#security-requirements-definition)
- [Software Assurance](#software-assurance)
- [Continuous Integration/Continuous Deployment (CI/CD)](#continuous-integrationcontinuous-deployment-cicd)
- [Supply Chain Risk Management](#supply-chain-risk-management)
- [Hardware Assurance](#hardware-assurance)
- [End-of-Life (EOL) Considerations](#end-of-life-eol-considerations)
- [Practical Application: Hybrid Development Scenario](#practical-application-hybrid-development-scenario)
- [Implementation in DoD Environments](#implementation-in-dod-environments)
- [Comparison Tables and Decision Frameworks](#comparison-tables-and-decision-frameworks)
- [Key Resources and Standards](#key-resources-and-standards)

---

## Introduction to Secure Systems Development Life Cycle (SDLC)

The Systems Development Life Cycle (SDLC) represents the structured process organizations use to plan, create, test, deploy, and maintain information systems. SecurityX (CAS-005) emphasizes integrating security from the very beginning—often called "shift left"—rather than bolting it on at the end. This approach reduces costs, minimizes vulnerabilities, and builds inherently resilient systems.

**Core Phases of SDLC (with Security Integration):**
- **Requirements** — Define security needs early.
- **Design** — Architect secure components.
- **Implementation** — Build with secure coding practices.
- **Testing** — Validate through multiple assurance methods.
- **Deployment** — Secure rollout via CI/CD.
- **Operations and Maintenance** — Continuous monitoring and updates.
- **Disposition** — Secure decommissioning.

In corporate environments, secure SDLC supports compliance with standards like SOC 2, ISO 27001, and customer contracts. In DoD environments, it aligns directly with the Risk Management Framework (RMF) per `DoDI 8510.01`, NIST SP 800-160, and program protection plans.

**Benefits of Early Security Integration:**
- Reduced remediation costs (up to 100x cheaper in requirements phase vs. production).
- Improved system trustworthiness.
- Better alignment between security, development, and business/mission objectives.

---

## Security Requirements Definition

Security requirements must be clearly defined and traceable throughout the entire life cycle. They fall into two main categories.

### Functional Requirements
**Definition**: These describe specific behaviors or features the system must perform, including security capabilities. For a new professional, think of them as "what the system does." Advanced users recognize them as verifiable, testable statements tied to use cases.

**Examples**:
- Corporate: "The system shall authenticate users via multi-factor authentication (MFA) before accessing customer data."
- DoD: "The system shall enforce Role-Based Access Control (RBAC) for all CUI-handling interfaces per NIST SP 800-53 control AC-3."

**Best Practices**: Use SMART criteria (Specific, Measurable, Achievable, Relevant, Traceable). Map to threat models and business/mission needs.

### Non-Functional Requirements
**Definition**: These define how the system performs (quality attributes) rather than what it does. New professionals: These are the "ilities" — reliability, scalability, security. Advanced: They often become architectural drivers and SLAs.

**Examples**:
- Corporate: "The system shall achieve 99.99% availability with recovery time objective (RTO) under 5 minutes."
- DoD: "The system shall maintain integrity of data at rest using FIPS 140-3 validated cryptography."

### Security vs. Usability Trade-off
**Definition**: Balancing robust security controls against user experience and operational efficiency. Overly strict controls can lead to shadow IT or reduced productivity.

**Corporate Application**: Implementing strict password policies might increase helpdesk calls. Solution: Adaptive authentication and passwordless options (e.g., passkeys).

**DoD Application**: Tactical environments require quick access during missions. Use context-aware controls and just-in-time permissions while maintaining `DoDI 8500.01` compliance.

**Decision Framework**:
| Factor | Security Priority | Usability Priority | Recommended Approach |
|--------|-------------------|--------------------|----------------------|
| High-Risk Data | Strong MFA, least privilege | Streamlined workflows | Risk-based authentication |
| Mission-Critical Ops | Strict controls | Minimal friction | Biometrics + conditional access |

---

## Software Assurance

Software assurance encompasses activities to ensure software is free of vulnerabilities, functions as intended, and resists tampering.

### Static Application Security Testing (SAST)
**Definition**: White-box testing that analyzes source code or binaries without execution. New professionals: Like a code reviewer looking for flaws statically. Advanced: Integrated into IDEs for real-time feedback.

**Corporate Application**: Tools like SonarQube or Checkmarx scan during development.

**DoD Application**: Required in RMF Step 3 (Implement) and continuous monitoring.

### Dynamic Application Security Testing (DAST)
**Definition**: Black-box testing that examines running applications by simulating attacks. New professionals: Treats the app like an external hacker would.

**Corporate Application**: OWASP ZAP or Burp Suite against staging environments.

**DoD Application**: Validates deployed configurations against STIGs.

### Interactive Application Security Testing (IAST)
**Definition**: Combines SAST and DAST by analyzing code while the application runs, providing precise vulnerability location and context.

**Corporate Application**: Ideal for microservices with tools like Contrast Security.

### Runtime Application Self-Protection (RASP)
**Definition**: Security tools embedded in the application runtime that detect and block attacks in real-time.

**Corporate Application**: Protects against zero-days in production.

**DoD Application**: Enhances resilience in contested environments.

### Vulnerability Analysis
**Definition**: Systematic identification, classification, and prioritization of weaknesses.

**Tools**: Nessus, OpenVAS, or dependency checkers.

### Software Composition Analysis (SCA)
**Definition**: Identifies open-source components and their known vulnerabilities/licensing issues.

**Corporate Application**: Black Duck or Snyk in pipelines.

**DoD Application**: Critical for SBOM compliance.

### Software Bill of Materials (SBOM)
**Definition**: A formal, machine-readable inventory of all components in a software product, including versions, suppliers, and licenses. New professionals: Like a detailed ingredients list for software. Advanced: Enables rapid vulnerability response per Executive Order 14028.

**Corporate Application**: Generated via Syft or CycloneDX formats.

**DoD Application**: Mandated for software supply chain visibility. `https://www.cisa.gov/sbom`

### Formal Methods
**Definition**: Mathematical techniques to prove correctness of algorithms and systems.

**Corporate Application**: Used in safety-critical software (e.g., aerospace).

**DoD Application**: Applied to high-assurance systems under `DoDI 5200.44`.

---

## Continuous Integration/Continuous Deployment (CI/CD)

CI/CD pipelines automate building, testing, and deploying code, with security gates embedded at every stage.

### Coding Standards and Linting
**Definition**: Enforced rules for code style and quality. Linting tools catch errors early.

**Corporate Application**: ESLint for JavaScript, pylint for Python.

**DoD Application**: Integrates with secure coding STIGs.

### Branch Protection
**Definition**: Git controls requiring reviews, status checks, and approvals before merging.

**Best Practices**: Require signed commits and multiple approvers.

### Continuous Improvement
**Definition**: Iterative refinement using metrics, feedback, and lessons learned.

### Testing Activities
- **Unit Testing**: Tests individual components.
- **Integration Testing**: Verifies interactions between components.
- **Regression Testing**: Ensures new changes don't break existing functionality.
- **Automated Test and Retest**: CI-triggered re-execution of test suites.
- **Canary Testing**: Gradual rollout to a subset of users to monitor impact.

**Corporate Application**: Jenkins, GitHub Actions, or GitLab CI with security scanning stages.

**DoD Application**: Supports DevSecOps initiatives under DoD Enterprise DevSecOps Reference Design.

---

## Supply Chain Risk Management

Supply chain risk management (SCRM) addresses threats from third-party components and suppliers.

### Software Supply Chain Risk Management
**Definition**: Processes to secure the software ecosystem from development to delivery.

**Corporate Application**: Vendor risk assessments and code signing.

**DoD Application**: `DoDI 5200.44` and NIST SP 800-161. Focus on provenance and counterfeit prevention.

### Hardware Supply Chain Risk Management
**Definition**: Mitigation of risks in physical components, including tampering and counterfeits.

**Corporate Application**: Supplier audits and hardware root of trust (TPM).

**DoD Application**: Program Protection Plans (PPP) and Trusted Systems and Networks (TSN) initiatives.

---

## Hardware Assurance

**Definition**: Processes ensuring hardware components are genuine, reliable, and free from malicious modifications.

**Certification and Validation Process**:
- FIPS 140-3 for cryptographic modules.
- Common Criteria (CC) evaluations.
- DoD-specific: Defense Microelectronics Activity (DMEA) trusted sources.

**Corporate Application**: Procurement policies requiring validated hardware.

**DoD Application**: Integrated into RMF and acquisition lifecycle.

---

## End-of-Life (EOL) Considerations

**Definition**: Secure handling of systems and components when they reach end of support.

**Key Activities**:
- Data sanitization (NIST SP 800-88).
- Secure disposal or recycling.
- Migration planning to new platforms.
- Archiving of configurations and SBOMs.

**Corporate Application**: Asset retirement processes to prevent data leaks.

**DoD Application**: Strict media sanitization per `DoD 5220.22-M` and CUI destruction requirements.

---

## Practical Application: Hybrid Development Scenario

**Scenario**: A defense contractor develops a cloud-native application handling both commercial data and CUI.

**Requirements**:
- Functional: API endpoints with OAuth2.
- Non-Functional: Zero-trust enforcement, SBOM generation.
- Assurance: SAST/DAST/SCA in CI/CD pipeline.
- Supply Chain: Vetted open-source components.
- EOL: Automated data wipe on decommission.

**Implementation Steps**:
1. Define requirements in Jira with security acceptance criteria.
2. Integrate security tools in GitHub Actions.
3. Generate SBOM at build time.
4. Conduct RMF tailoring for DoD portions.
5. Plan phased retirement with continuity measures.

---

## Implementation in DoD Environments

DoD emphasizes **DevSecOps**, RMF integration, and **cyber resilient systems engineering** per NIST SP 800-160. Key guidance includes:

- `https://software.af.mil/` (DoD Enterprise DevSecOps)
- DISA STIGs for development tools
- eMASS for documenting assurance activities

**RACI Integration**: Program Manager accountable, Security Engineer responsible for implementation.

---

## Comparison Tables and Decision Frameworks

**Assurance Testing Methods Comparison**:

| Method | Type | Speed | Accuracy | Best For | Corporate Example | DoD Example |
|--------|------|-------|----------|----------|-------------------|-------------|
| SAST | White-box | Fast | High (code-level) | Early development | SonarQube | Static analysis in DevSecOps pipeline |
| DAST | Black-box | Medium | Runtime behavior | Production-like | OWASP ZAP | Boundary testing |
| IAST | Hybrid | Real-time | Contextual | CI/CD | Contrast | High-assurance apps |
| RASP | Runtime | Ongoing | Low false positives | Live protection | Production shields | Contested environments |

**SDLC Security Integration Maturity**:

| Level | Description | Corporate Indicators | DoD Indicators |
|-------|-------------|----------------------|---------------|
| Initial | Ad-hoc security | Post-deployment fixes | Reactive patching |
| Managed | Basic gates | SCA + SAST | RMF Step 3 |
| Defined | Automated pipelines | Full CI/CD security | DevSecOps Reference Design |
| Optimized | Continuous assurance | AI-driven | JADC2 alignment |

---

## Key Resources and Standards

- NIST SP 800-160 Vol. 1 & 2: `https://csrc.nist.gov/publications/sp/800/160`
- NIST SP 800-218: Secure Software Development Framework
- DoD DevSecOps: `https://software.af.mil/`
- CISA SBOM Resources: `https://www.cisa.gov/sbom`
- OWASP SAMM: Software Assurance Maturity Model
