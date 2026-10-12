# CompTIA Security+ SY0-701 — Day 1 Notes

**Study date:** 12 October 2026  
**Focus:** Security foundations, the CIA triad, threats, vulnerabilities, exploits, risk, attack surface, and attack vectors.

> These are personal study notes prepared for revision. They are not official CompTIA materials. Use them alongside the current SY0-701 exam objectives and your chosen learning resources.

## Learning objectives

By the end of Day 1, I should be able to:

- Explain the CIA triad and give a workplace example of each principle.
- Distinguish a threat, vulnerability, exploit, and risk.
- Explain attack surface and attack vector.
- Distinguish CVSS vulnerability severity from organisational risk.
- Apply these concepts to a basic security-operations scenario.

---

## 1. The CIA triad

The CIA triad is a foundational information-security model consisting of **Confidentiality, Integrity, and Availability**.

### 1.1 Confidentiality

**Definition:** Information should be accessible only to authorised people, systems, or processes.

**Examples**
- An employee cannot read another employee's salary records without permission.
- Customer information is encrypted so that unauthorised parties cannot readily read it.

**Common controls**
- Access controls and least privilege
- Authentication and authorisation
- Encryption
- Data classification and handling procedures

**Memory aid:** Confidentiality = keep information private.

### 1.2 Integrity

**Definition:** Information and systems should remain accurate, complete, and protected from unauthorised or improper modification.

**Examples**
- An attacker changes a bank-account number in a database.
- An administrator verifies that a downloaded file has not changed unexpectedly by checking its cryptographic hash against a trusted reference.

**Common controls**
- Hashes and file-integrity monitoring
- Digital signatures
- Change control and audit logs
- Access controls and database constraints

**Important distinction:** A hash can help detect changes when compared with a trusted value. A hash alone does not prove who created a file or guarantee that the file is trustworthy.

**Memory aid:** Integrity = keep information correct and unaltered.

### 1.3 Availability

**Definition:** Systems, services, and information should be accessible to authorised users when needed.

**Examples**
- A distributed denial-of-service (DDoS) attack makes a website unavailable.
- A server outage prevents employees from accessing a business application.

**Common controls**
- Redundancy and failover
- Backups and tested recovery procedures
- Capacity management
- DDoS protection and resilient architecture
- Monitoring and incident response

**Memory aid:** Availability = keep services accessible.

### CIA triad quick-reference table

| Principle | Main question | Example impact | Example controls |
|---|---|---|---|
| Confidentiality | Who can see the information? | Unauthorised disclosure | Encryption, access control |
| Integrity | Can information be changed improperly? | Unauthorised or incorrect modification | Hashing, signatures, change control |
| Availability | Can authorised users access it when needed? | Outage or service disruption | Redundancy, backups, failover |

An incident can affect more than one CIA principle.

---

## 2. Threats, vulnerabilities, exploits, and risk

These concepts are related but not interchangeable.

### 2.1 Threat

**Definition:** A potential cause of harm to an asset, system, organisation, or person.

**Examples**
- A cybercriminal attempting to steal credentials
- Ransomware
- A malicious insider
- Fire, flooding, or another environmental event

**Question to ask:** What could cause harm?

### 2.2 Vulnerability

**Definition:** A weakness in a system, application, configuration, process, or security control that could be exploited or otherwise lead to harm.

**Examples**
- An unpatched operating system
- A web application vulnerable to SQL injection
- Weak password practices
- A misconfigured cloud storage bucket
- Excessive user permissions

**Question to ask:** What weakness could be abused?

A vulnerability can exist even if nobody has exploited it.

### 2.3 Exploit

**Definition:** A technique, code, or sequence of actions that takes advantage of a vulnerability.

**Example:** An attacker sends crafted input to abuse a SQL injection vulnerability.

**Question to ask:** How is the weakness being used?

**Distinction:** The vulnerability is the weakness; the exploit is the method or means used to take advantage of it. An exploit may be a technique or a piece of code.

### 2.4 Risk

**Definition:** The potential for loss or harm when a threat affects an asset, considering factors such as likelihood and impact.

A useful high-level model is:

**Risk depends on likelihood and impact.**

This is a conceptual model, not a universal numerical formula. Organisations may use qualitative or quantitative risk methodologies.

**Example:** An internet-facing, unpatched production server containing sensitive customer data may present significant risk because it is exposed and the consequences of compromise could be severe.

**Question to ask:** How likely is harm, and how serious would it be?

### Put the concepts together

Scenario: A company has an internet-facing server running outdated software.

1. **Threat:** An attacker may target the server.
2. **Vulnerability:** The server has an unpatched software flaw.
3. **Exploit:** The attacker uses a technique that abuses the flaw.
4. **Potential impact:** Data exposure, unauthorised changes, or service disruption.
5. **Risk assessment:** The organisation considers likelihood, exposure, asset value, potential impact, and existing controls.

This is a learning model, not a mandatory sequence for every incident. Risk can exist before an attack occurs, and a vulnerability does not necessarily mean that exploitation has occurred.

---

## 3. Attack surface vs. attack vector

### Attack surface

**Definition:** The collection of points where an attacker might be able to interact with or attack a system.

**Examples**
- Internet-facing services and open ports
- Web applications and APIs
- Remote-access services
- User accounts and identity systems
- Cloud storage and exposed management interfaces

### Attack vector

**Definition:** The route, method, or means used to carry out an attack.

**Examples**
- Phishing email
- Stolen credentials
- Exploitation of an exposed vulnerable service
- Abuse of a misconfigured API

**Memory aid**
- **Attack surface:** Where the opportunities for attack exist.
- **Attack vector:** How an attack is carried out.

They are related, but they are not synonyms.

---

## 4. CVE, CVSS severity, and organisational risk

### CVE

**Common Vulnerabilities and Exposures (CVE)** identifiers are used to identify publicly documented cybersecurity vulnerabilities. A CVE identifier points to a particular vulnerability record; it is not, by itself, a complete risk assessment.

### CVSS

**Common Vulnerability Scoring System (CVSS)** provides a standardised way to represent vulnerability severity using defined metrics. A CVSS score helps compare technical severity, but it does not automatically tell an organisation exactly how urgently it must remediate a finding.

### Organisational risk

Risk depends on the organisation's context, which can include:
- Whether the asset is internet-facing or internally isolated
- Whether the vulnerable component is present and affected
- Exploitability and credible threat activity
- Asset criticality and sensitivity of the data
- Potential business and operational impact
- Existing mitigations and compensating controls

**Example:** Two systems may have vulnerabilities with the same CVSS severity, but the internet-facing production server holding sensitive customer data may create greater organisational risk than an isolated test system. The actual priority should be determined through the organisation's risk process and available evidence.

**Exam takeaway:** CVSS severity is an input to risk-based prioritisation, not a substitute for it.

---

## 5. Applying the concepts in security operations

### Scenario: Wazuh reports a critical CVE on a Windows endpoint

A vulnerability alert indicates that installed software may be affected by a known CVE.

A security analyst should not assume from the alert alone that an attacker has exploited it. A sensible workflow is:

1. **Validate the finding:** Confirm the affected asset, software, version, and relevant vulnerability details.
2. **Assess exposure:** Determine whether the system is internet-facing, reachable from relevant network segments, or otherwise exposed.
3. **Assess risk:** Consider severity, exploitability, asset criticality, business impact, and available mitigations.
4. **Look for evidence of exploitation:** Review relevant endpoint, authentication, network, and security alerts where appropriate.
5. **Prioritise remediation:** Coordinate patching or other approved mitigations according to the organisation's process.
6. **Verify remediation:** Confirm that the patch or mitigation was applied and that the finding is resolved.
7. **Document the outcome:** Record evidence, decisions, exceptions, and residual risk as required.

A vulnerability alert is evidence of a potential weakness; it is not, by itself, proof of a successful compromise.

---

## 6. Common exam traps and distinctions

- **Threat vs. vulnerability:** A threat could cause harm; a vulnerability is a weakness.
- **Vulnerability vs. exploit:** The vulnerability is the weakness; the exploit is the method or code that takes advantage of it.
- **Threat vs. risk:** A threat is a potential cause of harm; risk considers the likelihood and impact of harm in context.
- **Attack surface vs. attack vector:** The surface is the set of possible attack points; the vector is the route or method used.
- **CVSS vs. risk:** CVSS communicates vulnerability severity; organisational risk also depends on business context, exposure, likelihood, impact, and controls.
- **Vulnerability vs. compromise:** A vulnerable system has a weakness; compromise requires evidence that an unauthorised action or impact actually occurred.
- **CIA triad:** Disclosure primarily affects confidentiality, unauthorised modification primarily affects integrity, and service disruption primarily affects availability. A single incident can affect multiple principles.

---

## 7. Quick revision sheet

| Term | One-line meaning |
|---|---|
| Confidentiality | Prevent unauthorised disclosure |
| Integrity | Protect accuracy and prevent unauthorised modification |
| Availability | Ensure authorised access when needed |
| Threat | Potential cause of harm |
| Vulnerability | A weakness that could be exploited |
| Exploit | Technique or code that takes advantage of a vulnerability |
| Risk | Potential loss or harm assessed in context, including likelihood and impact |
| Attack surface | Potential points of interaction or attack |
| Attack vector | Route or method used to carry out an attack |
| CVE | Identifier for a publicly documented vulnerability |
| CVSS | Standardised vulnerability-severity scoring system |

## 8. Self-test

Try to answer from memory before checking the notes.

1. An unauthorised employee reads confidential salary data. Which CIA principle is primarily affected?
2. An attacker changes a customer's bank-account number in a database. Which CIA principle is primarily affected?
3. A DDoS attack prevents customers from accessing an online service. Which CIA principle is primarily affected?
4. A web application contains a SQL injection flaw. Identify the vulnerability.
5. An attacker sends crafted input to exploit that flaw. What does the attack technique represent?
6. What is the difference between an attack surface and an attack vector?
7. Why might two vulnerabilities with the same CVSS score have different organisational risk?
8. Does a Wazuh vulnerability alert alone prove that the endpoint has been compromised?

### Answer key

1. Confidentiality.
2. Integrity.
3. Availability.
4. The SQL injection weakness in the application.
5. An exploit technique.
6. The attack surface is the set of potential attack points; the attack vector is the route or method used.
7. Exposure, exploitability, asset criticality, business impact, and mitigations may differ.
8. No. The alert indicates a potential vulnerability; compromise requires separate supporting evidence.

---

## 9. Day 1 completion checklist

- [ ] Explain confidentiality, integrity, and availability without notes.
- [ ] Give one example and one control for each CIA principle.
- [ ] Distinguish threat, vulnerability, exploit, and risk.
- [ ] Explain attack surface vs. attack vector.
- [ ] Explain why CVSS severity is not the same as organisational risk.
- [ ] Describe how an analyst should validate and prioritise a vulnerability alert.
- [ ] Complete the self-test and revisit incorrect answers during revision.

## Day 1 summary

Today established the vocabulary needed to understand security controls, vulnerability management, incident analysis, and risk-based decision-making. The key skill is not merely memorising definitions; it is identifying which concept applies to a real scenario and explaining why.

**Next study session:** Continue the Security+ learning sequence with the next foundational topic, using short explanations, workplace examples, and exam-style practice.
