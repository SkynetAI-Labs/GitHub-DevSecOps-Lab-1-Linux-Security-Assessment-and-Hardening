
![Lab 01 — Linux Security Assessment & Hardening](skynet-lab-01.png)

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

The saved follow-up package listing contains two available updates.
The published evidence does not establish why those updates remained
available or confirm their later installation.

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
| Password-quality module | Not recorded as enabled | Installed and enabled |
| UFW firewall | Initial Lynis audit detected an active firewall; UFW baseline not established | UFW active and configured |
| Automatic update configuration | Enabled | Enabled |

The follow-up Lynis audit recorded a hardening index of 69/100, a 3-point improvement from 66/100, with no reported warnings. This does not independently confirm that all vulnerable packages were patched.

## Evidence

### Security Assessment Report

- [Full Linux Security Vulnerability Assessment Report](VULNERABILITY_REPORT.md)

### Lynis Audit Results

- [Initial Lynis audit](evidence/lynis-before.dat)
- [Follow-up Lynis audit](evidence/lynis-after.dat)

### Package Management

- [Packages before remediation](evidence/packages-before.txt)
- [Packages after remediation](evidence/packages-after.txt)

### Authentication and Firewall

- [Password-quality configuration](evidence/password-policy.txt)
- [UFW firewall status](evidence/firewall-status.txt)

### Network and System Configuration

- [Network-service inspection](evidence/network-services.txt)
- [OpenSSH Server installation status](evidence/ssh-status.txt)
- [Automatic-update configuration](evidence/automatic-updates.txt)

Evidence should be reviewed and sanitised before publication to remove sensitive information.

## Audit and evidence status — 24 October 2026

Repository review confirmed the recorded Lynis 3.1.6 hardening indices:
66 before and 69 after. The reports record start times of 9 October 2026
17:34:06 and 10 October 2026 00:00:14; their timezone is not stated.
The package listings contain 133 and two upgradable entries respectively.
These are historical observations, not a current assessment of the machine.

The password-policy file records configured values and the follow-up Lynis
report detects pam_pwquality. End-to-end password-change enforcement was
not tested in the published evidence. UFW settings were recorded; external
traffic filtering was not connection-tested. Automatic-update configuration
does not prove later successful update installation.

No GitHub Actions workflow is present and no workflow runs were returned
at review time. This lab's evidence consists of saved local assessment
outputs; no new host scan or system changes were performed during this review.

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


## Repository audit — 24 October 2026

See the [dated security audit and prioritised recommendations](SECURITY_AUDIT.md) for the reviewed source commit, verification results, open findings and evidence limitations.

