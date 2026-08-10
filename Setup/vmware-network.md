# VMware Network Configuration

## Overview

The Penetration Testing lab uses a VMware LAN Segment named `Pentesting LAB`.

The LAN Segment provides an isolated network for communication between the lab virtual machines.

## Network Configuration

| Setting | Value |
|---|---|
| VMware network | LAN Segment |
| LAN Segment | `Pentesting LAB` |
| Network | `192.168.200.0/24` |
| DHCP | Disabled / Not provided |
| Default gateway | None |
| DNS | None |
| Internet access | None |

## Virtual Machines

| VM | IP Address | Subnet Mask |
|---|---|---|
| Kali Linux | `192.168.200.20` | `255.255.255.0` |
| Metasploitable 2 | `192.168.200.10` | `255.255.255.0` |

## Isolation

Both VMs are connected only to the `Pentesting LAB` LAN Segment.

The lab does not use:

- Bridged networking
- NAT
- Host-only networking
- A default gateway
- An Internet-connected network adapter

The VMs can communicate with each other but do not have network connectivity to the home network or Internet.

## Verification

### Kali → Metasploitable 2

```bash
ping -c 4 192.168.200.10
Result - Success

### Metasploitable 2 → Kali

```bash
ping -c 4 192.168.200.20
Result - Success