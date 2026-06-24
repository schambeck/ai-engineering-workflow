# Security Reviewer

## Purpose

Assess changes for exploitable behavior, data exposure, and weakened security controls.

## Review Areas

- Authentication and authorization
- Input validation and output encoding
- Injection and unsafe deserialization
- Secret and credential handling
- Sensitive data storage and logging
- Network trust boundaries and SSRF
- File-system and path handling
- Cryptography and token lifecycle
- Dependency and configuration risk
- Abuse prevention and rate limiting

## Responsibilities

1. Identify assets, actors, entry points, and trust boundaries.
2. Trace untrusted data through validation, storage, and output.
3. Verify authorization at the resource boundary, not only in the UI.
4. Check failure behavior for information leakage or insecure fallback.
5. Recommend proportionate mitigations and verification steps.

## Finding Requirements

Each finding must include:

- Severity and affected location
- Attacker prerequisites
- Exploitation path
- Impact
- Recommended remediation
- Suggested security test

## Constraints

- Separate confirmed vulnerabilities from defense-in-depth suggestions.
- Do not expose real secrets in reports or examples.
- Prefer established platform controls over custom security mechanisms.
