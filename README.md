# DVWA Penetration Test Report

A simulated penetration testing engagement against DVWA (Damn Vulnerable Web Application),
performed to practice real-world methodology: reconnaissance, exploitation, evidence
collection, severity scoring, and remediation guidance.

This is not a list of isolated lab exercises — it's written and structured the way a
professional pentest report would be delivered to a client.

## 📄 Full Report

👉 **[Read the full report here](report.md)**

The report includes:
- Scope and methodology
- Reconnaissance
- Detailed findings with evidence, CVSS scoring, and remediation
- An executive summary

## Target Environment

- **Application:** DVWA (Damn Vulnerable Web Application)
- **Deployment:** Local Docker instance
- **Security Level Tested:** Medium
- **Testing Type:** Authenticated, white-box (source-available) web application testing

## Tools Used

Burp Suite (Proxy, Repeater, Intruder), Nmap, Docker

## Findings Summary

| # | Finding | Severity | CVSS |
|---|---------|----------|------|
| 1 | Broken brute-force protection | High | 8.1 |
| 2 | *(in progress)* | | |

## About Me

Learning web application security and building hands-on penetration testing experience.
[GitHub profile](https://github.com/Ratul952) · [PortSwigger Writeups](https://github.com/Ratul952/Portswigger-Writeups)
