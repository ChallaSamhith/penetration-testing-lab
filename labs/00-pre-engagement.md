# Penetration Test — Pre-Engagement

**Client:** Qelvaris Technologies Private Limited
**Status:** Fictional Company — Cybersecurity Laboratory
**Engagement:** Internal Network Penetration Test
**Assessment Type:** Black-Box
**Target:** QTL-SRV-01
**Target IP:** `192.168.200.10`
**Tester:** Authorized Security Tester
**Testing IP:** `192.168.200.20`
**Network:** `192.168.200.0/24`

---

## 1. Fictional Company Disclaimer

**Qelvaris Technologies Private Limited is a fictional company created exclusively for this cybersecurity laboratory.**

It does not represent a real client, organization, or production environment. All systems, personnel, business information, and engagement details are simulated.

Testing is authorized only against the laboratory target defined in this document.

---

## 2. Scenario

Qelvaris Technologies Private Limited has requested an internal network penetration test against one of its Linux servers.

The objective is to determine whether an attacker with access to the internal network could:

* Discover exposed services.
* Identify security vulnerabilities.
* Gain unauthorized access.
* Escalate privileges.
* Demonstrate the potential impact of a successful compromise.

The assessment is conducted as a **black-box penetration test**.

The tester is given the target IP address but is not provided with credentials, service information, vulnerability information, or system configuration.

The target is implemented using **Metasploitable 2** for laboratory purposes.

---

## 3. Scope

### In Scope

| Asset      | IP               |
| ---------- | ---------------- |
| QTL-SRV-01 | `192.168.200.10` |

### Out of Scope

* Kali Linux
* VMware host
* Home network
* Internet
* Other virtual machines
* Any system other than `192.168.200.10`

---

## 4. Rules of Engagement

The following activities are permitted against the target:

* Network reconnaissance
* Port and service enumeration
* Vulnerability assessment
* Controlled authentication testing
* Controlled exploitation
* Post-exploitation
* Privilege-escalation testing
* Evidence collection
* Network traffic analysis

The following activities are prohibited:

* Denial-of-service attacks
* Destruction or modification of data
* Persistent backdoors
* Malware deployment
* Lateral movement to other systems
* Testing systems outside the defined scope

Testing must stop if the target becomes unstable or activity begins affecting an out-of-scope system.

---

## 5. Methodology

The engagement follows:

**Primary methodology:** Penetration Testing Execution Standard (PTES)

**Supporting guidance:** NIST SP 800-115 — Technical Guide to Information Security Testing and Assessment

**Severity scoring:** CVSS v4.0 where applicable

The practical assessment is divided into:

1. Reconnaissance
2. Enumeration
3. Vulnerability Assessment
4. Exploitation
5. Post-Exploitation
6. Privilege Escalation
7. Reporting

Wireshark is used as a supporting traffic-analysis and evidence-collection tool throughout the engagement.

---

## 6. Five-Vulnerability Laboratory Objective

The Metasploitable 2 target contains many intentionally vulnerable services.

For this laboratory, the assessment will focus on **five significant vulnerabilities** representing different attack techniques.

The five vulnerabilities are **not disclosed to the tester before testing**.

They must be discovered through the normal black-box methodology.

The five findings will demonstrate:

* Service-based exploitation
* Remote command execution
* Authentication weakness
* Vulnerability validation
* Initial compromise
* Post-exploitation
* Privilege escalation

Only vulnerabilities actually discovered and validated during the engagement will be reported as findings.

---

## 7. Evidence and Documentation

Each phase will document:

* Actions performed
* Commands/tools used
* Results
* Relevant screenshots
* Findings
* Decisions and observations

Screenshots will be captured only when they provide useful evidence.

No phase will contain fabricated results.

Documentation will be created as the engagement progresses.

---

## 8. Engagement Workflow

```text
Pre-Engagement
      ↓
Reconnaissance
      ↓
Enumeration
      ↓
Vulnerability Assessment
      ↓
Exploitation
      ↓
Post-Exploitation
      ↓
Privilege Escalation
      ↓
Final Report
```

The final report will summarize the attack path, confirmed vulnerabilities, evidence, impact, severity, and remediation recommendations.

---

## 9. Authorization

For this laboratory exercise, the tester is authorized to perform the activities defined above against:

**QTL-SRV-01 — `192.168.200.10`**

No authorization is granted for any other system.

**Engagement Status:** Authorized for Laboratory Execution

---

**End of Pre-Engagement Document**
