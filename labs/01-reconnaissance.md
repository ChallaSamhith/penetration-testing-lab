# Phase 1 — Reconnaissance

## Objective

Identify and establish the presence of the authorized target within the assessment network.

## Methodology

This phase follows the reconnaissance/intelligence-gathering principles of the **Penetration Testing Execution Standard (PTES)**.

## Target

| Item                | Details          |
| ------------------- | ---------------- |
| Asset               | QTL-SRV-01       |
| IP Address          | 192.168.200.10   |
| Network             | 192.168.200.0/24 |
| Testing Workstation | 192.168.200.20   |

## 1. Host Discovery

### Objective

Determine whether the authorized target is reachable from the Kali testing workstation.

### Commands

```bash
ping 192.168.200.10
nmap -sn 192.168.200.10
```

### Results

The target responded successfully to ICMP requests.

Nmap host discovery confirmed that `192.168.200.10` is up and reachable.

Nmap also identified the following MAC address:

```text
00:0C:29:FA:DD:2A
```

The MAC address was identified as VMware.

### Evidence

* ICMP connectivity confirmed.
* Target confirmed active through Nmap host discovery.
* VMware MAC address identified.

### Observation

The authorized target is active and reachable from the Kali testing workstation.

No vulnerability conclusion is made at this stage.

---

## Evidence

### Evidence 1 — Host Discovery

**Evidence:** Terminal output from ICMP connectivity test and Nmap host discovery.

**Target:** 192.168.200.10

**Result:** Host confirmed active.

---

## Phase Status

**Status:** In Progress

The target has been confirmed as reachable. Further reconnaissance is required to identify the externally exposed attack surface.
