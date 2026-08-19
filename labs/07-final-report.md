# Penetration Testing Final Report

## 1. Executive Summary

This penetration test was conducted against an intentionally vulnerable Linux system in an isolated VMware laboratory environment.

The assessment simulated a black-box penetration test against **Qelvaris Technologies Private Limited**.

> **Disclaimer:** Qelvaris Technologies Private Limited is used as a fictional client name for this cybersecurity laboratory project. No real production systems were tested.

The assessment identified multiple critical vulnerabilities that allowed remote code execution, unauthorized access, and ultimately complete root-level compromise of the target system.

---

## 2. Engagement Overview

| Item | Details |
|---|---|
| Client | Qelvaris Technologies Private Limited |
| Assessment Type | Black-Box Penetration Test |
| Target | Metasploitable 2 |
| Attacker System | Kali Linux |
| Platform | VMware Workstation Pro |
| Network | Isolated VMware LAN Segment |
| Target IP | `192.168.200.10` |
| Attacker IP | `192.168.200.20` |
| Testing Period | August 2026 |

---

## 3. Scope

The assessment was limited to the intentionally vulnerable Metasploitable 2 host:

```text
192.168.200.10
```

Only the following five vulnerabilities were included in the exploitation scope:

1. vsftpd 2.3.4 Backdoor
2. distccd Command Execution
3. UnrealIRCd Backdoor
4. Java RMI Server Vulnerability
5. PostgreSQL 8.3.x Vulnerability

Other vulnerabilities identified during reconnaissance and enumeration were outside the defined exploitation scope.

---

## 4. Rules of Engagement

The following rules were applied during the assessment:

- Testing was performed only against the designated laboratory target.
- The environment was isolated from the home network and Internet.
- Testing was limited to the five vulnerabilities defined in scope.
- Exploitation was performed using controlled techniques.
- Evidence was collected through terminal output and screenshots.
- No real-world systems or data were targeted.

---

## 5. Methodology

The assessment followed the following penetration-testing methodology:

```text
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

Each phase was documented separately in the project repository.

---

## 6. Findings Summary

| # | Vulnerability | Impact | Severity |
|---|---|---|---|
| 1 | vsftpd 2.3.4 Backdoor | Remote root access | Critical |
| 2 | distccd Command Execution | Remote command execution | High |
| 3 | UnrealIRCd Backdoor | Remote command execution | Critical |
| 4 | Java RMI Server Vulnerability | Remote code execution | Critical |
| 5 | PostgreSQL 8.3.x Vulnerability | Unauthorized database/service access | High |
| 6 | SUID Nmap 4.53 | Local privilege escalation to root | Critical |

> **Note:** The SUID Nmap issue was identified during post-exploitation/privilege-escalation activities and is reported separately from the five initial exploitation targets.

---

## 7. Detailed Findings

### 7.1 vsftpd 2.3.4 Backdoor

**Severity:** Critical

The target exposed vsftpd 2.3.4 on TCP port 21.

The service was confirmed vulnerable and successfully exploited using the Metasploit Framework.

The exploitation resulted in a Meterpreter session running as:

```text
Server username: root
```

**Impact:**

- Remote access to the target
- Root-level privileges
- Complete system compromise

**Recommendation:**

- Remove vsftpd 2.3.4.
- Upgrade to a supported version.
- Disable unnecessary FTP services.
- Restrict FTP access using firewall rules.

---

### 7.2 distccd Command Execution

**Severity:** High

The target exposed distccd on TCP port 3632.

The service was successfully exploited to obtain a command shell.

The resulting shell was running as:

```text
uid=1(daemon) gid=1(daemon)
```

This access was subsequently used as the starting point for privilege escalation.

**Impact:**

- Remote command execution
- Unauthorized system access
- Potential privilege escalation

**Recommendation:**

- Disable distccd if not required.
- Restrict access to trusted hosts.
- Upgrade or remove obsolete services.

---

### 7.3 UnrealIRCd Backdoor

**Severity:** Critical

UnrealIRCd was identified during service enumeration and included in the defined exploitation scope.

The presence of a backdoored version of the service represents a serious remote command-execution risk.

**Impact:**

- Remote command execution
- Potential unauthorized system access
- Potential complete system compromise

**Recommendation:**

- Remove the compromised version.
- Install software only from trusted sources.
- Upgrade to a supported release.
- Restrict unnecessary IRC services.

---

### 7.4 Java RMI Server Vulnerability

**Severity:** Critical

A Java RMI service was identified during enumeration and included in the exploitation scope.

The exposed RMI service represented a potential remote code-execution attack surface.

**Impact:**

- Remote code execution
- Unauthorized access to the host
- Potential system compromise

**Recommendation:**

- Disable unnecessary RMI services.
- Restrict RMI access to trusted systems.
- Apply current security updates.
- Avoid exposing Java management interfaces directly to untrusted networks.

---

### 7.5 PostgreSQL 8.3.x Vulnerability

**Severity:** High

An outdated PostgreSQL 8.3.x service was identified on TCP port 5432.

The service was included in the defined exploitation scope because of its obsolete software version and associated security risks.

**Impact:**

- Increased attack surface
- Potential unauthorized database access
- Potential compromise through outdated software

**Recommendation:**

- Upgrade PostgreSQL to a supported release.
- Restrict database access to trusted hosts.
- Enforce strong authentication.
- Remove unnecessary database exposure.

---

## 8. Privilege Escalation Finding

### SUID Nmap 4.53

**Severity:** Critical

During privilege-escalation testing, SUID binaries were enumerated from the `daemon` shell.

The following binary was identified:

```text
-rwsr-xr-x 1 root root 780676 Apr  8  2008 /usr/bin/nmap
```

Nmap version 4.53 supported interactive functionality.

The SUID-root binary was used to obtain a root shell:

```text
nmap>
!sh

whoami
root
```

**Attack Path:**

```text
distccd
   ↓
daemon shell
   ↓
SUID-root Nmap 4.53
   ↓
Interactive shell
   ↓
root
```

**Impact:**

An attacker who obtains a low-privileged local shell can escalate to complete root-level control.

**Recommendation:**

- Remove the SUID permission from Nmap.
- Remove Nmap from production systems where unnecessary.
- Review all SUID binaries regularly.
- Apply the principle of least privilege.
- Upgrade obsolete software.

---

## 9. Attack Chain

The assessment demonstrated multiple independent paths to compromise.

The primary demonstrated privilege-escalation chain was:

```text
Target Discovery
      ↓
Service Enumeration
      ↓
distccd Exploitation
      ↓
daemon Shell
      ↓
SUID Enumeration
      ↓
SUID Nmap 4.53
      ↓
Root Shell
```

A separate exploitation path through vsftpd resulted directly in root-level Meterpreter access:

```text
vsftpd 2.3.4
      ↓
Backdoor Exploitation
      ↓
Meterpreter Session
      ↓
root
```

---

## 10. Risk Summary

The target presented a **critical overall security risk**.

The combination of:

- Outdated software
- Backdoored services
- Unnecessary exposed services
- Weak service configuration
- SUID-root binaries

allowed an attacker to obtain unauthorized access and ultimately achieve root-level control.

---

## 11. Recommendations

The following remediation actions are recommended:

1. Remove or upgrade all obsolete software.
2. Remove known backdoored software versions.
3. Disable unnecessary network services.
4. Restrict exposed services using firewall rules.
5. Remove unnecessary SUID permissions.
6. Apply the principle of least privilege.
7. Maintain regular security patching.
8. Regularly review exposed services and SUID binaries.
9. Monitor authentication and system activity for suspicious behavior.
10. Perform periodic vulnerability assessments and penetration tests.

---

## 12. Conclusion

The penetration test demonstrated that the target could be compromised through multiple outdated and vulnerable services.

The most significant result was the ability to obtain **root-level access** through both the vsftpd 2.3.4 backdoor and the privilege-escalation path involving SUID-enabled Nmap 4.53.

The findings demonstrate the security impact of running obsolete software and allowing unnecessary privileged functionality on a system.

Remediation should prioritize removal of backdoored software, upgrading unsupported services, reducing the exposed attack surface, and eliminating unnecessary SUID privileges.
