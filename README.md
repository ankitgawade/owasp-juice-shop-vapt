# owasp-juice-shop-vapt
Documented VAPT assessment of OWASP Juice Shop, including testing methodology, evidence, findings, and remediation recommendations.

This project documents six findings from a local OWASP Juice Shop 20.3.0 training lab at `http://localhost:3000`, using dummy accounts. The report uses saved HTTP captures and screenshots from 27 October 2026 (IST).

## Report and recommendations

- [PDF report](report/OWASP_Juice_Shop_VAPT_Report.pdf)
- [Markdown report](report/OWASP_Juice_Shop_VAPT_Report.md)
- [Remediation recommendations](remediation/recommendations.md)

## Findings

| ID | Finding | CVSS v3.1 | Severity | Status |
| --- | --- | --- | --- | --- |
| F-01 | [SQL Injection - Authentication Bypass](findings/01-sqli-auth-bypass.md) | 9.1 | Critical | Confirmed |
| F-02 | [Password Hash Disclosure in JWT Payload](findings/02-password-hash-disclosure.md) | 4.3 | Medium | Confirmed |
| F-03 | [Weak Password Hashing - Unsalted MD5](findings/03-weak-password-hashing.md) | 5.3 | Medium | Confirmed |
| F-04 | [IDOR - Unauthorized Shopping Basket Read](findings/04-basket-idor.md) | 4.3 | Medium | Confirmed |
| F-05 | [DOM-based XSS in Search](findings/05-dom-xss.md) | 6.1 | Medium | Confirmed |
| F-06 | [Reflected XSS in Order Tracking](findings/06-reflected-xss.md) | 6.1 | Medium | Confirmed |

Scores follow CVSS v3.1 with full vectors and metric assumptions in each finding and the report. F-03 explicitly models the documented hash-exposure/recovery scenario.

## Evidence

The [evidence directory](evidence/) contains paired request/response records and original screenshots. Each finding links to its supporting files. An additional [MD5 verification record](evidence/03%20-Weak_Password_Hashing/03-md5-known-password-verification.md) documents the comparison made during report preparation.

## Repository layout

The report contains scope, methodology, findings, recommendations, tools, and references. Individual finding files provide convenient GitHub navigation, and the evidence directory contains the supporting captures. The remediation file provides a consolidated action list.
