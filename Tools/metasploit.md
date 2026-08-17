# Metasploit

## Overview

Metasploit Framework is a penetration testing platform used to discover, validate, and demonstrate security vulnerabilities.

In this lab, Metasploit is used from Kali Linux against the intentionally vulnerable Metasploitable 2 target within the isolated `CYBERLAB` VMware LAN Segment.

## Installation and Verification

Kali Linux normally includes Metasploit Framework.

Verify the installation:

```bash id="z8e6qv"
msfconsole --version
```

Find the executable:

```bash id="0c0g5x"
which msfconsole
```

Start the Metasploit console:

```bash id="g7g2c4"
msfconsole
```

Exit the console with:

```text id="j1q3vb"
exit
```

If Metasploit is not installed:

```bash id="qhz4b8"
sudo apt update
sudo apt install metasploit-framework
```

## Lab Network

Metasploit is used from Kali Linux against Metasploitable 2.

```text id="brw6b7"
Network: CYBERLAB
Subnet: 192.168.200.0/24

Kali Linux:       192.168.200.20
Metasploitable 2: 192.168.200.10
```

The lab network is isolated from the home network and Internet.

## Basic Metasploit Workflow

The general workflow is:

```text id="l8e3dn"
Reconnaissance
      ↓
Service identification
      ↓
Vulnerability research
      ↓
Module selection
      ↓
Module configuration
      ↓
Controlled exploitation
      ↓
Verification
      ↓
Documentation
```

Nmap should normally be used before Metasploit to identify the services and versions exposed by the target.

## Starting Metasploit

Start the console with:

```bash id="xq8e2d"
msfconsole
```

The Metasploit console provides access to modules and commands used during penetration testing.

## Useful Console Commands

Display general help:

```text id="9zv8wb"
help
```

Search for modules:

```text id="2fk2ai"
search <keyword>
```

Display information about a module:

```text id="k3l1a7"
info <module>
```

Select a module:

```text id="z8cv3m"
use <module>
```

Display module options:

```text id="2cb9jh"
show options
```

Display compatible payloads:

```text id="e2x1st"
show payloads
```

Display module targets:

```text id="y5y9uw"
show targets
```

Return to the previous module context:

```text id="c9k4lm"
back
```

Display the current module:

```text id="1v3x2d"
show
```

Clear the console:

```text id="0f3s9k"
clear
```

Exit Metasploit:

```text id="l5b7zq"
exit
```

## Target Configuration

Metasploit modules generally require the target address to be specified.

For this lab, the target is:

```text id="w2x4p8"
RHOSTS = 192.168.200.10
```

Kali's address is:

```text id="u8k4n6"
192.168.200.20
```

[Certain] The exact module options vary by module. Always inspect the module with:

```text id="e4g6v2"
show options
```

before running it.

## Payloads

A payload defines the action performed after successful exploitation.

Common payload categories include:

* Command shell
* Meterpreter
* Reverse connections
* Bind connections

Payload selection depends on the target, exploit module, operating system, architecture, and network configuration.

## Sessions

After successful exploitation, Metasploit may create a session.

Useful session commands include:

```text id="f6k9m2"
sessions
```

List active sessions.

```text id="s3d7x1"
sessions -i <session_id>
```

Interact with a specific session.

```text id="j8p2w5"
background
```

Background the current session.

[Certain] Session behavior depends on the selected exploit and payload.

## Lab Workflow with Nmap

A typical exercise should follow:

```text id="n7q4w1"
Nmap
  ↓
Identify open ports
  ↓
Identify services and versions
  ↓
Research vulnerability
  ↓
Metasploit search
  ↓
Review module information
  ↓
Configure target
  ↓
Run controlled test
  ↓
Verify result
  ↓
Document findings
```

Example reconnaissance:

```bash id="c4v7p2"
nmap -sV 192.168.200.10
```

Then use the discovered service information to research appropriate Metasploit modules.

## Documentation

Metasploit commands and general usage are documented in this file.

Individual exploitation exercises should be documented under:

```text id="x1z5r8"
labs/
```

Lab documentation should record:

* Target
* Target service
* Vulnerability
* Metasploit module
* Configuration
* Result
* Evidence
* Lessons learned

## Security Considerations

Metasploit should only be used against systems that are authorized for testing.

In this project, the authorized target is the intentionally vulnerable Metasploitable 2 VM:

```text id="k7m3q9"
192.168.200.10
```

The lab is isolated using the VMware `CYBERLAB` LAN Segment.

Do not connect Metasploitable 2 to a production network, home network, or public Internet.

## Lab Scope

```text id="v9c2m6"
Attacker:
Kali Linux
192.168.200.20

Target:
Metasploitable 2
192.168.200.10

Network:
CYBERLAB
192.168.200.0/24
```

All Metasploit exercises in this project are restricted to the isolated lab environment.
