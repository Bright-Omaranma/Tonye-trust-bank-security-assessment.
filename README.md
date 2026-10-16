---
title: "Security Assessment Plan for Tonye Trust Bank Ltd."
project_id: "CSF-001"
course: "Cybersecurity Fundamentals"
student: "Bright Madubuochi Omranma"
cohort: "February 2026"
---

CYBERSECURITY FUNDAMENTALS

SECURITY ASSESSMENT PLAN FOR
TONYE TRUST BANK LTD.

Project ID: CSF-001

Student Name: Bright Madubuochi Omranma

Student ID: [Add your student ID]

Cohort: February 2026

Instructor: Nyekwere TamunoTonye Tom

Submission Date: [Add submission date]

Individual Project | Introductory Cybersecurity

## Executive Summary

This assessment reviews the cybersecurity posture of Tonye Trust Bank Ltd., a fictional bank with approximately 60 employees and departments covering Customer Service, Finance, Human Resources, Administration and Information Technology. The assessment is based on the scenario supplied for the academic project; no live systems were tested and no exploitation is claimed. The review identifies weaknesses involving network separation, backup access, customer-data exports, shared administrative accounts, security-log protection and the submission of customer information to a public artificial-intelligence service.

The most significant risks are unauthorized exposure of customer information, compromise spreading from a public-facing service into internal systems, damage to transaction integrity, and loss or encryption of backups. The bank should adopt a risk-based programme consistent with the NIST Cybersecurity Framework 2.0, which organizes outcomes around Govern, Identify, Protect, Detect, Respond and Recover (Pascoe et al., 2024). Priority actions include segmenting the network, restricting privileged access, protecting backups, reducing unnecessary customer-data copies, strengthening monitoring, and establishing an approved-use policy for AI services. Controls should be proportionate to risk and should preserve legitimate banking activity. The bank should validate implementation through documented access reviews, restore tests, log reviews, staff training and follow-up assessment.

## 1. Scope and Assumptions

The scope is limited to the assets, services and observations described in the assignment scenario. The assessment is a desk-based review of a fictional organization, not a penetration test, vulnerability scan or confirmation of a real breach. The report identifies observed conditions, inferred risks and unknown facts separately. For example, the scenario confirms that customer information was submitted to a public AI service, but does not establish whether the service retained it, used it for training, or disclosed it to another party.

Risk levels are qualitative. High means a plausible event could seriously affect customers, money, critical services or sensitive data; Medium means meaningful harm is possible but may be limited by other controls; Low means expected impact or likelihood is comparatively limited. These ratings are preliminary and should be reviewed after the bank confirms system configurations, existing controls, data flows and business requirements. Recommendations are based on the scenario and general guidance from NIST, CISA and ISC2.

## 2. Security Principles and Objectives (Part A)

Confidentiality prevents unauthorized disclosure; integrity protects accuracy and completeness; and availability ensures authorized users can access systems and information when required. The relative importance varies by asset. For a customer database, confidentiality and integrity are especially important because disclosure or alteration can harm customers and undermine trust. For backups, availability and integrity are critical because unusable or altered backups may prevent recovery. Authentication verifies identity, authorization determines permitted actions, and accounting records activity. Privacy requires appropriate handling of personal information, while non-repudiation supports reliable attribution of actions.

| Asset | Why It Matters | Confidentiality | Integrity | Availability | Other Principle | Justification |
| --- | --- | --- | --- | --- | --- | --- |
| Customer database | Contains identity, account and transaction information. | High | High | High | Privacy, authorization, accounting | Disclosure may enable fraud; unauthorized changes can corrupt records; service disruption can affect customer operations. |
| Online banking portal | Customer-facing banking service. | High | High | High | Authentication, non-repudiation | Customer sessions and transactions must be protected; inaccurate transactions and outages are both serious. |
| Internal file server | Stores departmental documents and reports. | High | Medium | Medium | Authorization, accounting | Confidential HR or finance documents need restricted access; temporary downtime may be manageable through alternatives. |
| Finance systems | Support financial operations and transaction processing. | High | High | High | Separation of duties, non-repudiation | Financial confidentiality and accurate processing are essential; disruption can stop important operations. |
| Backup server | Stores organizational backups. | High | High | High | Authorization, availability | Backups must remain confidential, unaltered and recoverable; compromise can undermine disaster recovery. |
| Staff workstations | Used for daily employee work. | Medium | Medium | Medium | Authentication, least privilege | Workstations may contain cached or downloaded data and can be entry points for malware. |
| Email system | Supports internal and external communication. | High | Medium | High | Authentication, privacy, accounting | Email may carry sensitive attachments and can be used for phishing or account takeover. |
| Security logs | Record activities on important systems. | High | High | Medium | Accounting, non-repudiation | Logs can reveal sensitive events and must be protected against unauthorized access or alteration. |
| Employee records | Contain HR and personal information. | High | High | Medium | Privacy, authorization | Disclosure may cause personal harm; accurate records are needed for employment administration. |
| CCTV/NVR system | Records physical-security video. | Medium | Medium | Medium | Privacy, authorization | Footage may reveal movements and must be restricted; loss can weaken physical investigations. |

### Professional Responsibility and Scope

If authorized to assess the internal file server and another server appears reachable, I would stop short of probing, logging in, scanning, copying files or testing its weaknesses. I would record only the minimum observation obtained within the authorized activity, avoid accessing its data, and report the finding to my supervisor for written clarification or an updated scope. Technical capability is not authorization: the fact that a system is reachable does not grant permission to test it. A cybersecurity analyst must act ethically, protect information encountered accidentally, preserve evidence appropriately and remain within the agreed rules of engagement. This approach reflects professional conduct and due care, concepts included in ISC2’s Certified in Cybersecurity knowledge areas (ISC2, 2026).

## 3. Threat, Vulnerability and Risk Analysis (Part B)

A threat is a potential cause of harm, such as a malicious actor, malware or human error. A vulnerability is a weakness that may be used or triggered. Exploitation is the actual use of a weakness; the scenario does not confirm that the listed weaknesses have been exploited. Risk is the possibility and consequence of a security event, while organizational impact describes the resulting business harm.

| Asset | Threat | Vulnerability | Possible Security Event | Objectives Affected | Organizational Impact | Risk | Justification / Evidence Status |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Online banking and internal systems | External attacker or malware | Public-facing and internal systems share a general network environment (Observed). | Compromise of portal followed by attempted lateral movement (Inferred). | C, I, A | Service disruption, customer-data exposure, financial and reputational loss. | High | Internet-facing systems are exposed to external threats; insufficient separation may increase the potential reach of a compromise. No compromise is confirmed. |
| Guest Wi-Fi | Visitor or compromised guest device | Guest network is not properly separated (Observed). | Guest device reaches internal resources if permitted by configuration (Inferred). | C, I, A | Unauthorized access, malware spread, operational disruption. | High | Visitors should not need access to bank systems. Actual reachability and firewall rules remain unknown. |
| Backup server | Ransomware operator or compromised employee account | Normal staff workstations can reach backups (Observed). | Malware or an account compromise affects backup files (Inferred). | I, A, C | Recovery failure, extended outage, recovery costs. | High | Backups reachable from ordinary endpoints may be exposed to the same incident as production systems. Actual write permissions are unknown. |
| Customer spreadsheets | Insider, malware, accidental disclosure | Customer information is exported and some files are over-shared (Observed). | Unauthorized employee views, copies or distributes data (Inferred). | C, Privacy | Fraud, customer harm, regulatory or contractual consequences, loss of trust. | High | Extra copies and broad access increase exposure. No specific unauthorized access is confirmed. |
| Shared administrator account | Malicious insider or external attacker using stolen credentials | IT staff sometimes share an administrative account (Observed). | Actions cannot be reliably attributed to one person; shared credentials may be misused (Inferred). | C, I, A | Delayed investigation, unauthorized changes, accountability gaps. | High | Shared accounts weaken individual accountability. Whether credentials have been compromised is unknown. |
| Security logs | Insider or attacker attempting to hide activity | Management is unsure whether access restrictions are suitable (Observed). | Unauthorized viewing, deletion or alteration of logs (Inferred). | I, C, Accounting | Reduced incident-detection capability and weaker evidence for investigations. | Medium | The weakness is uncertainty about controls, not proof that logs are accessible or altered. |
| Public AI submission | Employee error or unapproved data processing | Customer report was copied into a public AI service (Observed). | Data retained or processed beyond the bank’s control (Possible; details Unknown). | C, Privacy | Confidentiality and privacy exposure, trust damage, possible compliance impact. | High | The submission occurred, but retention, model-training use and onward disclosure are not established. |
| Online transactions | Fraudster, malware, insider error | Scenario emphasizes the need for accurate and traceable transaction records; specific transaction controls are Unknown. | Unauthorized or erroneous transaction modification (Possible). | I, A, Non-repudiation | Financial loss, reconciliation effort, customer disputes. | High | Transaction integrity is a critical business requirement. The scenario does not confirm a transaction alteration. |

## 4. Security Controls and Gap Analysis (Part C)

The recommended controls are selected to address the risks rather than to introduce technology without a clear purpose. The Security+ categories below follow the assignment’s model (technical, managerial, operational and physical); the ISC2 CC column uses technical, administrative and physical. The primary category is selected for each control, although some controls also depend on management and staff processes.

| Current Situation | Security Gap | Control Objective | Recommended Control | Security+ Category | ISC2 CC Category | Expected Improvement |
| --- | --- | --- | --- | --- | --- | --- |
| Public-facing and internal systems share a general network. | Insufficient separation between exposed services and internal resources. | Limit paths from a compromised public service to internal assets. | Technical | Technical | Place online banking-facing components in a DMZ or equivalent isolated segment; use firewalls and explicit allow rules between segments. | Reduces lateral movement and limits the systems reachable after compromise. |
| Guest Wi-Fi not properly separated. | Guest devices may have an unnecessary route to internal systems. | Keep visitor access separate from bank resources. | Technical | Technical | Use a separate guest VLAN and firewall policy that permits internet access only; block private/internal ranges. | Reduces exposure from visitor devices. |
| Staff workstations can reach backup server. | Backups are not sufficiently isolated from ordinary endpoints. | Protect backup integrity and recoverability. | Technical | Technical | Restrict backup access to designated backup servers and authorized administrators; use immutable/offline copies and separate credentials. | Makes it harder for endpoint malware to delete or encrypt recovery copies. |
| Customer data exported to spreadsheets and shared too broadly. | Excessive data copies and broad access. | Reduce disclosure and unauthorized processing. | Technical | Administrative | Apply role-based access, data minimization, approved storage locations, encryption and DLP alerts for sensitive data movement. | Limits access to staff with a business need and improves detection of risky transfers. |
| Shared administrative account used by IT. | Poor individual attribution and privilege accountability. | Identify each administrator and limit privileged activity. | Technical | Administrative | Create unique named admin accounts, require MFA, use least privilege and log privileged actions; review access regularly. | Improves accountability and reduces credential-sharing risk. |
| Log access controls are uncertain. | Log confidentiality and integrity may not be assured. | Protect evidence and support detection/investigation. | Technical | Technical | Restrict log access by role, forward logs to a protected central repository, synchronize time and alert on changes or gaps. | Improves detection and preserves more reliable investigation evidence. |
| Customer data submitted to public AI. | No demonstrated approved-use guardrail or data-handling process. | Prevent sensitive information being submitted to unapproved services. | Managerial | Administrative | Publish an AI-use policy, train staff, require approved tools, prohibit sensitive data entry unless formally approved, and provide a safe redaction workflow. | Reduces accidental disclosure while allowing approved, privacy-preserving productivity. |
| Transaction records must remain accurate and traceable. | Specific integrity safeguards are not described in the scenario. | Prevent and detect unauthorized transaction changes. | Technical | Technical | Use role-based transaction permissions, separation of duties, strong authentication, audit trails, reconciliation and integrity monitoring. | Improves control over transaction changes and accountability. |

## 5. Security Control Functions (Part D)

A control’s function depends on its purpose and implementation, not only on the technology used. A firewall rule that blocks unauthorized traffic is preventive; a firewall alert that reports a denied connection is detective. A policy is directive because it tells employees what they must do. The table identifies the primary function and any additional function.

| Recommended Control | Primary Function | Additional Function, If Any | Justification |
| --- | --- | --- | --- |
| Network segmentation and firewall allow rules | Preventive | Detective | Blocking unapproved traffic prevents access; logging denied connections may also reveal suspicious attempts. |
| Separate guest Wi-Fi VLAN | Preventive | — | Isolation blocks guest devices from reaching internal networks when enforced by routing and firewall rules. |
| Immutable/offline backups and restricted backup access | Preventive | Corrective | Access restrictions help prevent tampering; restoration from clean backups helps recover after an incident. |
| Role-based access and least privilege for spreadsheets | Preventive | Directive | Permissions block unauthorized access; the access policy directs staff to use approved repositories. |
| Unique admin accounts and MFA | Preventive | Detective | MFA makes account takeover harder; individual account logs help identify suspicious or inappropriate actions. |
| Centralized protected logging and alerts | Detective | Corrective | Alerts detect suspicious activity; logs support investigation and remediation after an event. |
| AI acceptable-use policy and staff training | Directive | Preventive | The policy states required behavior; training and enforcement help prevent sensitive data from being submitted. |
| Transaction authorization, separation of duties and audit trail | Preventive | Detective | Approval and role restrictions prevent unauthorized changes; audit trails and reconciliation can reveal irregularities. |

### Controls With Multiple Functions

First, network firewalls can be preventive and detective. A rule that denies traffic between guest Wi-Fi and internal systems prevents unauthorized communication. If the firewall also records and alerts on repeated denied connections, it provides detective value. Second, backup controls can be preventive and corrective. Restricted credentials and immutable storage reduce the chance that an attacker can change backups, while verified restoration procedures help the bank recover after data loss or ransomware. These examples show why classification depends on the control’s configured purpose and operating process.

## 6. Data Protection (Part E)

Data protection should be based on the information’s sensitivity, where it is stored or transmitted, and the business purpose for which it is used. Encryption is useful for confidentiality but does not replace access controls, secure handling or data minimization. Hashing can help verify integrity when an appropriate secure hash and trusted comparison process are used; it is not a general method for hiding readable customer records.

| Information Type | Relevant Data State | Main Security Concern | Appropriate Protection Method | Reason |
| --- | --- | --- | --- | --- |
| Customer identity and account information | At rest in database; in transit to approved services; possibly copied into spreadsheets. | Disclosure, identity misuse and unauthorized access. | Encrypt at rest and in transit; role-based access; data minimization; DLP; mask fields in test or routine views. | Encryption protects stored and transmitted information; limiting copies and masking reduce exposure. |
| Transaction records | At rest in transaction systems and backups; in transit during processing. | Unauthorized changes, deletion or inability to prove what happened. | Strong transaction authorization, separation of duties, access logging, reconciliation and integrity checks; hash exported evidence where suitable. | Transactions require high integrity and traceability; audit trails support investigation and non-repudiation. |
| Employee/HR records | At rest in HR repositories and in approved transfers. | Exposure of personal and employment details. | Role-based access, encryption, retention limits, redaction before sharing and audit logging. | Only HR and other authorized roles should access relevant fields. |
| Departmental documents and reports | At rest on file server and shared folders; in transit to authorized colleagues. | Over-sharing or accidental external disclosure. | Access reviews, approved shared locations, encryption, data classification and watermarking for sensitive reports when useful. | Permissions and labels reduce inappropriate distribution and help trace document handling. |
| Security logs | At rest in logging platform; transmitted from systems to repository. | Alteration, deletion, unauthorized viewing or disclosure of technical details. | Centralized restricted storage, protected transmission, access logging, time synchronization and retention rules. | Protects investigative evidence and supports reliable event reconstruction. |
| CCTV footage | At rest on NVR or storage; viewed by authorized security staff. | Privacy intrusion, unauthorized viewing or deletion. | Restrict viewing/export permissions, secure storage, retention limits and audit access to footage. | Video should be available for legitimate security needs without unnecessary exposure. |

### Analysis of the Public AI Incident

The information exposed is the customer report or part of it, which may include personally identifiable information, account details or transaction information; the exact fields are unknown. Confidentiality and privacy are directly involved, and the bank’s governance and data-handling obligations may also be relevant. The employee should have asked: “Is this service approved by the bank for this information, and am I authorized to submit these data to it under our data-handling policy?” The fact that an AI service is publicly available does not mean it is approved for confidential business data. Its retention, access, training and processing terms may not meet the bank’s requirements.

The bank should promptly follow its incident-reporting process, document what was submitted and when, and consult the responsible security, privacy, legal or compliance personnel. It should not assume either that the data was retained or that no harm occurred. The bank should review the service’s terms and available deletion or incident-reporting options, assess the sensitivity of the submitted fields, and determine whether customer or regulatory notification is required. Preventive steps include an AI acceptable-use policy, staff training, approved enterprise tools, data-loss prevention where practical, and a redaction or de-identification workflow. Employees should use fictional or properly de-identified data for unapproved experiments.

## 7. Access Restrictions, Segmentation and Isolation (Part F)

The bank should adopt a segmented network in which systems are grouped by purpose and sensitivity. VLANs can provide logical separation, but separation is effective only when routing, firewall rules, identity controls and monitoring enforce it. This supports defense in depth: if one layer fails, other layers can still restrict access. CISA guidance recommends strong segmentation, placing externally facing services in a DMZ, and using explicit controls to limit communication between device groups (Cybersecurity and Infrastructure Security Agency [CISA], n.d.).

| Network Group | Proposed Separation | Allowed Communication | Why It Matters |
| --- | --- | --- | --- |
| Guest Wi-Fi | Separate guest VLAN/subnet with internet-only access. | Allow DNS and internet traffic through controlled egress; block access to all bank private networks. | Visitor devices should not reach employee or server resources. |
| Normal staff workstations | Staff VLANs, with further separation by department where useful. | Allow only approved business applications, file shares and services required for each role. | Reduces unnecessary access and limits lateral movement from a compromised workstation. |
| Sensitive business systems (Finance and HR) | Dedicated sensitive-system segments or tightly controlled application tiers. | Permit access only from approved staff roles and application servers; restrict direct workstation access where possible. | Financial and employee records require stronger confidentiality and integrity protections. |
| Server environment | Server VLANs separated by application/service role. | Allow only required application-to-database and management flows; deny unnecessary inbound and outbound traffic. | Reduces the number of systems that can communicate with a compromised server. |
| Online banking/public-facing systems | DMZ or equivalent isolated public-service segment. | Allow required customer-facing traffic to the web tier; permit only specifically required connections to backend services. | Internet-facing systems should not have broad access to internal networks. |
| Backup systems | Separate backup segment with tightly controlled backup paths. | Allow backup traffic from designated systems and management from approved admin hosts only; deny ordinary workstation access. | Reduces risk that endpoint malware can reach and destroy backups. |
| Security and administrative systems | Restricted management network or privileged access workstation segment. | Allow administration only through approved jump hosts or management tools with MFA and logging. | Separates powerful accounts and tools from everyday user activity. |
| Logging/monitoring systems | Protected monitoring segment or dedicated service environment. | Receive logs from systems; restrict log changes and console access to authorized security roles. | Helps preserve evidence and detect abnormal activity. |

The bank should use a default-deny approach between segments and then allow only documented business-required flows. For example, an approved online-banking application component may need to communicate with a specific backend service, but the public-facing server should not have unrestricted access to employee workstations, HR files or backup storage. Guest devices should not communicate directly with any internal segment. Ordinary staff workstations should not administer network equipment or write to backup repositories. Security administrators should use named accounts, MFA and a controlled management path.

Micro-segmentation may be considered for especially sensitive application workloads if the bank’s infrastructure supports it, but the first priority is a manageable, documented VLAN and firewall design. The IT team should maintain a network diagram, owner for each segment, approved communication rules and a change process. Rules should be tested in an authorized lab or controlled change window, with rollback plans and business-owner approval. Segmentation should not be treated as a substitute for endpoint protection, patching, strong authentication, secure configuration and staff awareness.

## 8. Major Recommendations

1. 1. Segment the network and isolate public-facing services. This is a top priority because a shared network environment and poorly separated guest Wi-Fi can expand the reach of a compromise. Implement a DMZ or equivalent, separate VLANs, and explicit firewall allow rules.
1. 2. Protect backups from ordinary endpoints. Restrict backup access, use separate credentials and administrative paths, maintain immutable or offline copies, and perform scheduled restore tests. Backups are valuable only if they can be restored reliably.
1. 3. Replace shared administrator accounts. Issue named administrator accounts, require MFA, apply least privilege and separation of duties, and review privileged access periodically. This improves accountability and reduces the impact of stolen credentials.
1. 4. Reduce customer-data copies and control AI use. Limit spreadsheet exports to legitimate needs, store them in approved restricted locations, apply masking or redaction where possible, and publish an AI-use policy that prohibits unapproved submission of sensitive data.
1. 5. Strengthen monitoring and incident response. Centralize and restrict security logs, alert on suspicious activity and log gaps, document incident escalation, and rehearse response and recovery. Use the results to refine risk ratings and controls.

## 9. Conclusion

The assessment identifies important risks at Tonye Trust Bank Ltd. that can be reduced through practical, layered controls. The most urgent concerns are weak separation between network environments, backup reachability from staff workstations, excessive copies of customer information, shared privileged accounts, uncertain log restrictions and unapproved use of public AI services. These observations do not prove that a cyberattack or data breach has occurred, but they justify action because the possible consequences are significant.

The bank should prioritize network segmentation, protected backups, individual privileged identities, controlled data handling and reliable monitoring. Management should assign control owners, establish completion dates and measure progress through access reviews, backup restoration tests, log reviews, staff training and follow-up assessments. A risk-based approach consistent with NIST’s Cybersecurity Framework can help the bank govern cybersecurity, protect critical assets, detect events, respond effectively and recover from disruption (Pascoe et al., 2024). The aim is not to block legitimate banking activity, but to ensure that employees and customers can use systems safely and reliably.

## References

Cybersecurity and Infrastructure Security Agency. (n.d.). *Enhanced visibility and hardening guidance for communications infrastructure*. https://www.cisa.gov/resources-tools/resources/enhanced-visibility-and-hardening-guidance-communications-infrastructure

Cybersecurity and Infrastructure Security Agency. (n.d.). *Require multifactor authentication*. https://www.cisa.gov/audiences/small-and-medium-businesses/secure-your-business/require-multifactor-authentication

ISC2. (2026). *Certified in Cybersecurity exam outline*. https://www.isc2.org/certifications/cc/cc-certification-exam-outline

Joint Task Force. (2020). *Security and privacy controls for information systems and organizations* (NIST Special Publication 800-53, Rev. 5). National Institute of Standards and Technology. https://doi.org/10.6028/NIST.SP.800-53r5

Pascoe, C., Quinn, S., & Scarfone, K. (2024). *The NIST Cybersecurity Framework (CSF) 2.0* (NIST Cybersecurity White Paper 29). National Institute of Standards and Technology. https://doi.org/10.6028/NIST.CSWP.29

## Appendix A: Evidence and Follow-up Checklist

Because this is a scenario-based assessment, no screenshots or live-system evidence have been created. If the instructor later provides an approved lab, evidence may include a labelled network-segmentation diagram, an access-control review, a sample redacted-data workflow, a backup restoration test record, or a sample log review. Each item should include a figure number, a title and an explanation of what it demonstrates. Do not scan, probe or test real systems without explicit written authorization.

| Follow-up Item | Evidence to Collect in an Authorized Environment | Purpose |
| --- | --- | --- |
| Network separation | Approved network diagram and firewall-rule review. | Confirm only required inter-segment flows are allowed. |
| Privileged access | List of named admin accounts, MFA status and access review record. | Confirm shared accounts have been replaced and access is appropriate. |
| Backup resilience | Documented restore-test result and backup-access list. | Confirm backups can be recovered and are isolated from ordinary endpoints. |
| Customer-data handling | Approved storage locations, access permissions and staff training record. | Confirm customer data is minimized and access is limited. |
| Security logging | Log access policy, alert examples and retention settings. | Confirm logs are protected, available and monitored. |
