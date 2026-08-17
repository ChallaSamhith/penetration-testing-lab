# Hydra

## Overview

Hydra is a network authentication auditing tool used to test login credentials against supported network services.

In this lab, Hydra is used from Kali Linux to perform controlled authentication testing against services running on the intentionally vulnerable Metasploitable 2 target.

## Installation and Verification

Kali Linux normally includes Hydra.

Verify the installation:

```bash id="z7m2k4"
hydra -h
```

Check the executable location:

```bash id="q8n5r1"
which hydra
```

Check the installed version:

```bash id="p4x9v6"
hydra -V
```

If Hydra is not installed:

```bash id="k2w7d3"
sudo apt update
sudo apt install hydra
```

## Lab Network

Hydra is used from Kali Linux against Metasploitable 2.

```text id="m6v1q8"
Network: CYBERLAB
Subnet: 192.168.200.0/24

Kali Linux:       192.168.200.20
Metasploitable 2: 192.168.200.10
```

The lab network is isolated from the home network and Internet.

## Basic Syntax

The general Hydra syntax is:

```bash id="r8n3t5"
hydra [options] target service
```

Hydra can test authentication services such as SSH, FTP, HTTP authentication, and other supported protocols.

## Username and Password Testing

A basic username/password test can use:

```bash id="w5k2p9"
hydra -l <username> -p <password> <target> <service>
```

Example structure:

```bash id="c7m4x2"
hydra -l <username> -p <password> 192.168.200.10 ssh
```

This tests the specified credentials against the SSH service on the lab target.

## Username and Password Lists

Hydra can use lists of usernames and passwords:

```bash id="n9v6r3"
hydra -L users.txt -P passwords.txt 192.168.200.10 ssh
```

Where:

* `-L` specifies a username list.
* `-P` specifies a password list.
* `192.168.200.10` is the Metasploitable 2 target.
* `ssh` specifies the service.

Only use credential lists created or authorized for the lab.

## Common Options

| Option | Purpose                                       |
| ------ | --------------------------------------------- |
| `-l`   | Specify a single username                     |
| `-L`   | Specify a username list                       |
| `-p`   | Specify a single password                     |
| `-P`   | Specify a password list                       |
| `-s`   | Specify a non-default port                    |
| `-t`   | Number of parallel tasks                      |
| `-v`   | Verbose output                                |
| `-V`   | Show each login/password attempt              |
| `-f`   | Stop after finding the first valid credential |
| `-o`   | Save results to a file                        |
| `-h`   | Display help                                  |

## Service Examples

Hydra supports multiple network services.

Examples include:

```bash id="d6q2w8"
hydra -l <username> -p <password> 192.168.200.10 ssh
```

```bash id="x4m8s1"
hydra -l <username> -p <password> 192.168.200.10 ftp
```

The target service must be running and accessible before authentication testing begins.

Use Nmap to identify available services:

```bash id="p5r9k3"
nmap -sV 192.168.200.10
```

## Lab Workflow

The recommended authentication-testing workflow is:

```text id="v2k7m4"
Nmap
  ↓
Identify authentication services
  ↓
Identify service and version
  ↓
Confirm service is in scope
  ↓
Prepare authorized test credentials
  ↓
Run controlled Hydra test
  ↓
Analyze result
  ↓
Document findings
```

Hydra should not be used blindly against every open port. First identify the service and determine whether authentication testing is appropriate.

## Rate and Resource Considerations

Authentication testing can generate significant network traffic and service load.

For controlled lab exercises:

* Use small credential lists initially.
* Use conservative task counts.
* Monitor the target service.
* Stop the test if the service becomes unstable.
* Record the parameters used during the exercise.

Example with a limited number of parallel tasks:

```bash id="q8v5n2"
hydra -t 2 -l <username> -P passwords.txt 192.168.200.10 ssh
```

## Saving Results

Hydra results can be saved to a file:

```bash id="m3x7c9"
hydra -l <username> -P passwords.txt 192.168.200.10 ssh -o hydra-results.txt
```

Store lab-specific results under the appropriate `labs/` directory.

Avoid committing sensitive credentials or unnecessarily large output files to the repository.

## Documentation

General Hydra usage is documented in this file.

Individual authentication-testing exercises should be documented under:

```text id="a6v3r8"
labs/
```

Lab documentation should record:

* Target
* Service
* Port
* Test account
* Credential source
* Hydra command
* Result
* Observations
* Lessons learned

Do not document or commit credentials that are not intended for the lab.

## Security Considerations

Hydra should only be used against systems and accounts that are authorized for testing.

For this project, the authorized target is the intentionally vulnerable Metasploitable 2 VM:

```text id="w9k2p5"
192.168.200.10
```

The attacking system is:

```text id="c4m7x1"
Kali Linux
192.168.200.20
```

All Hydra exercises are restricted to the isolated `CYBERLAB` VMware LAN Segment.

Do not use Hydra against external systems, production infrastructure, or accounts without explicit authorization.

## Lab Scope

```text id="s5v8n3"
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
