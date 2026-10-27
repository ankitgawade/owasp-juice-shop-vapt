# Remediation Recommendations

Remediation priorities address the demonstrated lab behaviors. CVSS v3.1 describes technical severity; the action order also considers related controls.

## Severity summary

| Finding | CVSS v3.1 | Severity |
| --- | --- | --- |
| F-01 | 9.1 | Critical |
| F-02 | 4.3 | Medium |
| F-03 | 5.3 | Medium |
| F-04 | 4.3 | Medium |
| F-05 | 6.1 | Medium |
| F-06 | 6.1 | Medium |

## Action priorities

| Priority | Finding | Action | Completion criterion |
| --- | --- | --- | --- |
| 1 - Immediate | F-01 | Parameterize login queries and verify passwords through a maintained library. | The injected request issues no session; valid login remains functional. |
| 2 - High priority | F-04 | Enforce server-side basket ownership for reads and related operations. | The same user cannot read the other account basket. |
| 2 - High priority | F-02 / F-03 | Remove password hashes from JWT claims and migrate MD5 representations to salted Argon2id. | Tokens contain no password data; password hashes use an adaptive salted format. |
| 2 - High priority | F-05 / F-06 | Render untrusted input as text; validate tracking IDs and review HTML/URL sinks. | Both route payloads are inert and valid search and tracking inputs remain functional. |
| 3 - Defense in depth | F-01 / F-05 / F-06 | Add least privilege, safe error handling, and a restrictive CSP after fixing primary causes. | The primary security controls remain effective without relying solely on extra layers. |

## F-01 - SQL Injection - Authentication Bypass (9.1 Critical)

Use parameterized queries or safe ORM query methods for all login data. Look up the account using bound values and verify its password with a password-hashing library. Apply least database privilege and keep database errors out of client responses.

**Suggested verification:** Replay the captured payload and verify that no authentication token is issued. Confirm that valid dummy credentials still work and that ordinary invalid credentials fail. Review the query implementation for parameter binding.

## F-02 - Password Hash Disclosure in JWT Payload (4.3 Medium)

Build JWT claims from an explicit allowlist of necessary identifiers and authorization claims. Exclude password hashes and other authentication secrets from token payloads and API serializers. JWT signing protects integrity and does not hide payload contents.

**Suggested verification:** Perform a normal login and decode the returned token. Verify that no password or password hash is present, while required authentication and authorization features still function.

## F-03 - Weak Password Hashing - Unsalted MD5 (5.3 Medium)

Replace direct MD5 password hashing with a maintained Argon2id implementation using unique random salts and an appropriate cost. Migrate legacy hashes by rehashing after successful login or requiring a password reset. Do not replace MD5 with another fast general-purpose hash.

**Suggested verification:** Verify that the stored representation uses a modern password-hashing format. Two test accounts with the same password should have different salted hashes, and the raw MD5 digest should no longer match the stored value. Confirm valid login still succeeds.

## F-04 - IDOR - Unauthorized Shopping Basket Read (4.3 Medium)

Enforce ownership on the server for each basket request. Scope lookups to the authenticated principal and requested basket, deny access to other users unless an explicit authorized role permits it, and apply the same checks to related read and write endpoints.

**Suggested verification:** User 26 should retain access to basket 7 and receive a consistent 403 or non-disclosing 404 for basket 6. Repeat in the opposite direction using user 25, and check related basket operations under the same authorization policy.

## F-05 - DOM-based XSS in Search (6.1 Medium)

Render search terms as text through framework interpolation or textContent. Avoid inserting user input into raw HTML and avoid sanitizer-bypass APIs. Where rich HTML is required, use a maintained sanitizer and enforce safe element, attribute, and URL-scheme policies.

**Suggested verification:** Replay the captured search payload and confirm that no iframe is created and no script runs. The input should appear as inert text or be safely rejected, while ordinary searches continue to work.

## F-06 - Reflected XSS in Order Tracking (6.1 Medium)

Validate tracking identifiers against the expected identifier format on the server. Return untrusted values as data and render them with safe text bindings. Apply context-appropriate encoding at rendering boundaries. Use a restrictive Content Security Policy as defense in depth.

**Suggested verification:** After remediation, open the captured tracking payload URL in a fresh tab or after a full reload. Confirm that the input is rejected or rendered as inert text, no script executes, and valid tracking identifiers continue to work.

## Related findings

F-02 and F-03 have separate causes and fixes: token data minimization removes the exposure, while an adaptive salted password hash reduces offline guessing efficiency. Both controls are needed. F-05 and F-06 affect separate input points. Safe rendering and input handling should be applied consistently to both search and order tracking.

## References

- [OWASP SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
- [RFC 7519 - JSON Web Token](https://www.rfc-editor.org/rfc/rfc7519)
- [OWASP Password Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html)
- [OWASP Insecure Direct Object Reference Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html)
- [OWASP DOM based XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/DOM_based_XSS_Prevention_Cheat_Sheet.html)
- [OWASP Cross Site Scripting Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
- [Pwning OWASP Juice Shop - Cross Site Scripting](https://pwning.owasp-juice.shop/companion-guide/latest/part2/xss.html)

CVSS score vectors and assessment assumptions are documented in the [report](../report/OWASP_Juice_Shop_VAPT_Report.md) and individual findings.
