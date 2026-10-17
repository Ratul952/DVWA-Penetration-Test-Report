# DVWA Penetration Test Report

## 1. Executive Summary
*(Write this last, once all findings are complete — a 3-4 sentence overview of
what was tested, what was found, and overall risk level.)*

## 2. Scope and Methodology

**Target:** DVWA (Damn Vulnerable Web Application), deployed locally via Docker
**Security Level Tested:** Medium
**Testing Type:** Authenticated, white-box testing
**Testing Window:** October 2026

**Methodology:** Testing followed a standard black-box-to-grey-box web application
approach: reconnaissance, manual exploration, intercepting proxy analysis (Burp Suite),
and targeted exploitation of each vulnerability class, with evidence captured at each step.

## 3. Reconnaissance

- Confirmed target scope: `http://127.0.0.1:42001`
- Ran `nmap -sV -p- localhost` to confirm exposed services
- Confirmed application identity and version via DVWA's `About` page
- Confirmed security level setting prior to testing (Medium)

![Security level confirmation](screenshots/01-security-medium.png)

## 4. Findings

### Finding 1: Broken Brute-Force Protection
**Severity:** High | **CVSS 3.1:** 8.1

**Description:**
The login form at `/vulnerabilities/brute/` has no account lockout, rate limiting,
or CAPTCHA protection at Medium security level, allowing unlimited automated login attempts.

**Steps to Reproduce:**
1. Intercepted a login request in Burp Suite:
   `GET /vulnerabilities/brute/?username=abcd&password=abcd&Login=Login`
2. Sent the request to Intruder and configured a cluster bomb attack, with a
   username wordlist on position 1 and a password wordlist on position 2.
3. Ran the attack (408 total requests) and sorted results by response length.
4. One result stood out: `admin` / `password` returned length **4746**, while
   all failed attempts returned **4708**.
5. Manually confirmed by logging in with `admin` / `password` — successful login,
   displaying "Welcome to the password protected area admin."

**Evidence:**
![Burp Intruder results showing anomaly](screenshots/06-intruder-results-anomaly.png)
![Manual login confirmation](screenshots/07-manual-confirm-login.png)

**Impact:**
An attacker can brute-force weak credentials with no detection or blocking,
leading to full account compromise.

**Remediation:**
- Implement account lockout after a defined number of failed attempts
- Add rate limiting or progressive delays between login attempts
- Require CAPTCHA after repeated failures
- Enforce a strong password policy

---

