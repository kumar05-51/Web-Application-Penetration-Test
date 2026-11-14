# Web-Application-Penetration-Test
Manual penetration test of DVWA covering Brute Force, Command Injection, SQL Injection, XSS, and CSRF — methodology based on OWASP WSTG, tested with Burp Suite.
# DVWA Web Application Penetration Test

A hands-on penetration testing exercise against [DVWA (Damn Vulnerable Web Application)](https://github.com/digininja/DVWA), a deliberately vulnerable PHP/MySQL web app used for learning and practicing common web security flaws.

> ⚠️ **Disclaimer:** This project was conducted entirely against a local, isolated DVWA instance for educational purposes. None of the techniques here were used against systems without explicit authorization. Do not test any application you do not own or have written permission to test.

## Overview

This repo documents a manual security assessment of DVWA at the **Low** security level, following a methodology based on the [OWASP Web Security Testing Guide (WSTG)](https://owasp.org/www-project-web-security-testing-guide/). Testing was performed using [Burp Suite](https://portswigger.net/burp) as an intercepting proxy.

## Scope

- Brute Force Authentication Bypass
- OS Command Injection
- SQL Injection
- Cross-Site Scripting (Reflected and Stored)
- Cross-Site Request Forgery (CSRF)

## Setup

DVWA was run locally via Docker:

\`\`\`bash
git clone https://github.com/digininja/DVWA.git
cd DVWA
docker compose up -d
\`\`\`

Then:
1. Navigate to `setup.php` and click **Create / Reset Database**.
2. Log in with `admin` / `password`.
3. Set **DVWA Security** to **Low**.

## Tools Used

| Tool | Purpose |
| --- | --- |
| Burp Suite Community | Intercepting proxy, Repeater, Intruder |
| Browser DevTools | Network inspection, debugging |
| sqlmap | Automated SQL injection validation |

## Findings Summary

| # | Finding | Severity | Status |
| --- | --- | --- | --- |
| 1 | Brute Force Authentication Bypass | High | Confirmed |
| 2 | OS Command Injection | Critical | Confirmed |
| 3 | SQL Injection | Critical | Confirmed |
| 4 | Cross-Site Scripting (Reflected and Stored) | High | Confirmed |
| 5 | Cross-Site Request Forgery | Medium | Confirmed |

Full details — including reproduction steps, evidence, impact, and remediation for each finding — are in the [penetration test report](./report.pdf).

## Key Takeaways

- Lack of input validation and output encoding was the root cause of most findings (Command Injection, SQL Injection, XSS).
- Missing anti-CSRF tokens made state-changing requests forgeable at the Low security level.
- No rate limiting or lockout policy allowed unrestricted brute forcing of credentials.

## References

- [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [DVWA GitHub Repository](https://github.com/digininja/DVWA)

