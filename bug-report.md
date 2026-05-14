---
layout: page
title: Bug Bounty Report – crAPI (Multiple Critical Vulnerabilities)
permalink: /bug-report/
---

# Bug Bounty Report – crAPI

**Target:** crAPI (Public Bug Bounty Target)  
**Researcher:** Asma NEJI  
**Date:** September 2025  
**Scope:** Full API surface (Authentication, Orders, Shop, Identity endpoints)  
**Methodology:** Manual testing, Burp Suite, custom scripts, business logic analysis

---

## Executive Summary

During the assessment of the crAPI platform, **8 vulnerabilities** were identified, including **3 Critical** and **3 High** severity issues. The findings primarily revolve around severe authentication weaknesses, authorization flaws, and business logic bypasses that could lead to full account takeover, privilege escalation, and financial abuse.

---

## Confirmed Vulnerabilities

### 1. JWT `alg=none` Authentication Bypass
**Severity:** Critical  
**Category:** Authentication Bypass / Cryptography  
**Component:** JWT Authentication

**Description**  
The application accepts unsigned JWT tokens by allowing the `alg` header to be set to `none`. This flaw allows attackers to forge arbitrary tokens without knowledge of the private signing key.

**Affected Endpoints**  
All authenticated API endpoints using JWT.

**Steps to Reproduce**
1. Login normally and capture a valid JWT.
2. Decode the token and change the header to `{"alg": "none", "typ": "JWT"}`.
3. Modify the payload (e.g., change user role or ID).
4. Remove the signature (end the token with a trailing `.`).
5. Send the forged token in authenticated requests.

**Impact**  
Complete authentication bypass. An attacker can impersonate any user, including administrators, leading to full account takeover and total application compromise.

---

### 2. JWT Expiration Not Enforced
**Severity:** High  
**Category:** Authentication / Session Management

**Description**  
The backend does not properly validate the `exp` (expiration) claim. Tokens remain valid even when the expiration time is set in the past.

**Impact**  
Expired or stolen tokens can be used indefinitely, significantly increasing the impact of any token leakage.

---

### 3. Missing JWT Revocation on Logout
**Severity:** Medium  
**Category:** Session Management

**Description**  
Logging out does not invalidate previously issued JWTs. Tokens continue to work even after logout.

**Impact**  
Stolen or leaked tokens remain active, allowing persistent unauthorized access.

---

### 4. Broken Object Level Authorization (IDOR) – Orders API
**Severity:** High  
**Category:** Authorization

**Affected Endpoint**  
`GET /workshop/api/shop/orders/{id}`

**Description**  
The API does not validate order ownership. Any authenticated user can view other users’ orders by modifying the order ID.

**Impact**  
Exposure of sensitive order details and payment information (PII) belonging to other users.

---

### 5. Mass Assignment Vulnerability (Privilege Manipulation)
**Severity:** Critical  
**Category:** API / Authorization

**Affected Endpoint**  
`POST /workshop/api/shop/orders`

**Description**  
The API blindly trusts client-supplied JSON fields, including `role`, `isAdmin`, and `available_credit`.

**Impact**  
Attackers can escalate privileges to admin level or manipulate account balances and states.

---

### 6. Business Logic Flaw – Negative Quantity Credit Abuse
**Severity:** Critical  
**Category:** Business Logic

**Description**  
The system accepts negative quantities, resulting in credit increases instead of deductions.

**Impact**  
Unlimited credit generation and complete bypass of the payment system.

---

### 7. Business Logic Flaw – Unlimited Order Amount
**Severity:** High  
**Category:** Business Logic

**Description**  
Extremely large quantity values are accepted without proper validation, leading to negative balances and accounting inconsistencies.

**Impact**  
Financial abuse and broken accounting integrity.

---

### 8. Missing Rate Limiting on Login Endpoint
**Severity:** High  
**Category:** API Security

**Affected Endpoint**  
`POST /identity/api/auth/login`

**Description**  
The login endpoint has no rate limiting, CAPTCHA, or account lockout mechanism.

**Impact**  
Enables brute-force and credential-stuffing attacks.

---

## Tested & Safe (Not Vulnerable)

The following issues were explicitly tested and found to be secure:

- **XSS (Reflected, Stored, DOM)**: All payloads treated as data, not executed.
- **CSRF**: State-changing requests properly protected.
- **CORS Misconfiguration**: No credential leakage possible despite `*` origin.
- **File Upload Execution**: Uploaded files (including SVG/HTML) are not executed.
- **SQL Injection (basic)**: No bypass or errors observed.
- **Clickjacking**: Protected by `X-Frame-Options`.
