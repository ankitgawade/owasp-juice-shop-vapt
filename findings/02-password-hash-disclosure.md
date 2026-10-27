# F-02 - Password Hash Disclosure in JWT Payload

| Field | Assessment |
| --- | --- |
| Severity | Medium |
| CVSS v3.1 score | 4.3 |
| CVSS v3.1 vector | `CVSS:3.1/AV:N/AC:L/PR:L/UI:N/S:U/C:L/I:N/A:N` |
| Status | Confirmed |
| Weakness | CWE-201 |
| Affected feature | `POST /rest/user/login; authentication.token -> data.password` |

## Description

A normal login response includes a signed JWT whose readable payload contains the test account password hash. The token serializes password-related data that is unnecessary for client authentication.

## Prerequisites

A successful login to a dummy customer account. Decoding the payload does not require the signing key.

## Steps to reproduce

1. Log in with the dummy account using the normal POST /rest/user/login request.
2. Copy authentication.token from the HTTP 200 response.
3. Decode the middle Base64url segment of the JWT locally as JSON.
4. Observe data.password alongside user ID 25, role customer, and basket ID 6.

```text
{
  "data": {
    "id": 25,
    "password": "5de52ea9d787966e8b598720255a37a7",
    "role": "customer"
  },
  "bid": 6
}
```

## Observed result

The normal login response and decoded-token screenshot expose the same password hash: 5de52ea9d787966e8b598720255a37a7. The hash is present in data.password within the readable JWT payload.

## Impact

A holder of the token can extract the test account hash and attempt password guesses offline. The observed MD5 representation increases the consequence of disclosure and is assessed separately in F-03.

## Severity rationale

AV:N/AC:L: a normal HTTP login response discloses the value without a special race or configuration. PR:L: the assessed access path uses a valid customer account. UI:N: no separate user action is needed. S:U: exposure remains within the application. C:L: the response exposes the logged-in account password verifier. I:N/A:N: direct disclosure alone does not alter data or disrupt service.

**Scoring assumptions:** This score covers the verified disclosure of the authenticated account hash. Password recovery and administrator bypass are separate findings, so their impacts are not added to this score.

## Technical note

The JWT uses RS256 for signing. The password-hashing algorithm is assessed independently in F-03. Base64url decoding makes the signed token payload readable.

## Remediation

Build JWT claims from an explicit allowlist of necessary identifiers and authorization claims. Exclude password hashes and other authentication secrets from token payloads and API serializers. JWT signing protects integrity and does not hide payload contents.

## Suggested remediation verification

Perform a normal login and decode the returned token. Verify that no password or password hash is present, while required authentication and authorization features still function.

## Evidence

- [02 — Password-Hash-Disclosure_request_response.md](../evidence/02%20-Password-Hash-Disclosure/02%20%E2%80%94%20Password-Hash-Disclosure_request_response.md)

![Normal login response containing the JWT.](../evidence/02%20-Password-Hash-Disclosure/screenshots/02%20%E2%80%94%20Password_Hash_Disclosure_request_response.png)

Normal login response containing the JWT.

![Decoded JWT contains data.password; the hash is readable without a signing key.](../evidence/02%20-Password-Hash-Disclosure/screenshots/02%20-Password_Hash_Disclosure_JWT_TOKEN_Decoded.png)

Decoded JWT contains data.password; the hash is readable without a signing key.

**References:** [RFC 7519 - JSON Web Token](https://www.rfc-editor.org/rfc/rfc7519)

**CVSS reference:** [FIRST CVSS v3.1 specification](https://www.first.org/cvss/v3.1/specification-document).
