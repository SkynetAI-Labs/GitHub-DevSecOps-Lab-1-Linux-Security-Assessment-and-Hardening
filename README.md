# GitHub DevSecOps Lab 1: Linux Security Assessment and Hardening

## Project Overview

A hands-on cybersecurity and DevSecOps project assessing the security posture of an Ubuntu Linux environment running on Windows Subsystem for Linux (WSL2).

The project demonstrates security auditing, vulnerability investigation, system hardening, remediation and evidence collection.

## Tools & Technologies

- Ubuntu Linux / WSL2
- Lynis Security Auditor
- APT Package Manager
- PAM / libpam-pwquality
- UFW Firewall
- Git & GitHub
- Bash

## Initial Security Assessment

**Security auditing tool:** Lynis 3.1.6

**Initial hardening index:** 66/100

The assessment identified security-hardening opportunities involving:

- Outdated software packages
- Password quality enforcement
- Firewall configuration
- System auditing and logging
- File permissions and kernel security settings

These findings represent configuration and maintenance concerns, not necessarily confirmed exploitable vulnerabilities.

## Remediation Activities

### 1. Package Security Updates

The initial assessment identified 133 packages with available updates.

Following package upgrades, two updates were deferred due to Ubuntu's phased rollout; their installation was not confirmed.

### 2. Password Policy Hardening

Installed and enabled `libpam-pwquality`.

Configured the following password requirements:

- Minimum password length: 14 characters
- Minimum character classes: 3
- Maximum consecutive repeated characters: 3

### 3. Firewall Configuration

Installed and enabled UFW with the following configuration:

- Incoming traffic: Deny
- Outgoing traffic: Allow
- Firewall logging: Enabled

Firewall behaviour within WSL2 may differ from a standalone Linux server and does not replace Windows host firewall controls.

### 4. Network Exposure Assessment

Inspected listening network services using `ss`.

Confirmed that OpenSSH Server was not installed. Reviewed the network listeners visible inside the Linux environment.

### 5. Automatic Security Updates

Verified that Ubuntu's automatic update configuration was enabled.

## Validation Results

| Assessment | Before | After |
|---|---|---|
| Lynis hardening index | 66/100 | 69/100 |
| Packages awaiting updates | 133 | 2 |
| Password-quality module | Not installed | Installed and enabled |
| UFW firewall | Not installed | Active |
| Automatic update configuration | Enabled | Enabled |

The follow-up Lynis audit recorded a hardening index of 69/100, a 3-point improvement from 66/100, with no reported warnings. This does not independently confirm that all vulnerable packages were patched.

## Evidence

The `evidence/` directory contains supporting audit outputs, package information and security configuration records.

Evidence should be reviewed and sanitised before publication to remove sensitive information.

## Limitations

This assessment was performed on Ubuntu running under WSL2, not a production Linux server.

WSL2 has different kernel, networking and service-management characteristics from conventional Linux deployments.

The project does not claim that outdated packages are exploitable without further vulnerability verification.

## Future Improvements

- Investigate specific CVEs affecting installed packages
- Implement automated security scans
- Assess Linux file permissions
- Expand system logging and monitoring
- Build CI/CD security controls
- Reproduce findings in an isolated Linux virtual machine

## Skills Demonstrated

Linux Security | Vulnerability Assessment | Security Hardening | Package Management | Firewall Configuration | Authentication Security | Security Documentation | Git
