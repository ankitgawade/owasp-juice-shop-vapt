# F-03 - Weak Password Hashing - Unsalted MD5

| Field | Assessment |
| --- | --- |
| Severity | Medium |
| CVSS v3.1 score | 5.3 |
| CVSS v3.1 vector | `CVSS:3.1/AV:N/AC:H/PR:L/UI:N/S:U/C:H/I:N/A:N` |
| Status | Confirmed for the tested account |
| Weakness | CWE-916 |
| Affected feature | `Password representation in the tested customer account; disclosed JWT data.password` |

## Description

The disclosed hash exactly matches MD5 of the known dummy password, calculated without a salt. This supports the weak-hashing finding for the tested account beyond a hash-format guess.

## Prerequisites

The known dummy password from the normal login capture and the corresponding hash disclosed in F-02.

## Steps to reproduce

1. Extract data.password from the normal login token documented in F-02.
2. Review the hash-identifier screenshot, which lists MD5 among multiple possible formats.
3. Independently calculate MD5 over the UTF-8 bytes of the known dummy password from the same request.
4. Compare the calculated digest with the disclosed hash; the values match exactly. The added verification record documents this report-preparation check.

```text
MD5(UTF-8 dummy password) = 5de52ea9d787966e8b598720255a37a7
Disclosed JWT password   = 5de52ea9d787966e8b598720255a37a7
Exact match             = True
```

## Observed result

An exact known-password comparison confirms that the observed value is the unsalted MD5 digest of the tested password. This check was performed during report preparation; the original terminal screenshot alone only suggested possible algorithms.

## Impact

An attacker who obtains this password representation can make rapid offline guesses and reuse precomputed values. The matched digest is a direct MD5 value without an adaptive work factor or per-password salt. F-02 provides an observed exposure route.

## Severity rationale

AV:N/PR:L: the assessment uses the observed authenticated network path to obtain verifier material. AC:H: successful password recovery depends on possessing a target verifier and a recoverable password, conditions beyond a guaranteed MD5 comparison. UI:N/S:U: no separate user action or authority change is required in the modeled scenario. C:H: recovery exposes a password secret. I:N/A:N: this score ends at password disclosure.

**Scoring assumptions:** This is an explicit F-02-to-F-03 exposure-and-recovery scenario score, not a universal standalone score for the MD5 algorithm. The tested known-password match proves the representation; recovery of an unknown password is a potential consequence. The two findings describe separate controls and their scores are not additive.

## Validation scope

The known-password comparison confirms the unsalted MD5 representation for the tested account.

## Remediation

Replace direct MD5 password hashing with a maintained Argon2id implementation using unique random salts and an appropriate cost. Migrate legacy hashes by rehashing after successful login or requiring a password reset. Do not replace MD5 with another fast general-purpose hash.

## Suggested remediation verification

Verify that the stored representation uses a modern password-hashing format. Two test accounts with the same password should have different salted hashes, and the raw MD5 digest should no longer match the stored value. Confirm valid login still succeeds.

## Evidence

- [02 — Password-Hash-Disclosure_request_response.md](../evidence/02%20-Password-Hash-Disclosure/02%20%E2%80%94%20Password-Hash-Disclosure_request_response.md)
- [03-md5-known-password-verification.md](../evidence/03%20-Weak_Password_Hashing/03-md5-known-password-verification.md)

![hash-identifier v1.2 proposes MD5 and other formats. The known-password comparison supplies the stronger algorithm check.](../evidence/03%20-Weak_Password_Hashing/screenshots/03%20-Weak_Password_Hashing_MD5.png)

hash-identifier v1.2 proposes MD5 and other formats. The known-password comparison supplies the stronger algorithm check.

**References:** [OWASP Password Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html)

**CVSS reference:** [FIRST CVSS v3.1 specification](https://www.first.org/cvss/v3.1/specification-document).
