---
layout: page
title: Bug Bounty Report – crAPI (Multiple Vulnerabilities)
permalink: /bug-report/
---

# Bug Bounty Report – crAPI

**Target:** crAPI (completely ridiculous API) – public bug bounty target  
**Researcher:** Asma NEJI  
**Date:** [Month Year – e.g., February 2026]  
**Scope:** Full API surface (authentication, orders, shop, identity endpoints)  
**Methodology:** Manual testing, Burp Suite, custom scripts, business logic analysis

For **each bug**, you’ll get:

*   Title
    
*   Severity
    
*   Affected endpoint(s)
    
*   Description
    
*   Steps to reproduce
    
*   Impact
    
*   Why it matters
    

Then I’ll list **TESTED & SAFE** items as **“Informational / Not Vulnerable (Tested)”**, which is _exactly_ how senior hackers document work.

✅ CONFIRMED VULNERABILITIES (REPORT‑READY)
==========================================

1️⃣ JWT alg=none Authentication Bypass
--------------------------------------

**Severity:** Critical**Category:** Authentication Bypass / Cryptography**Component:** JWT Authentication

### Description

The application accepts unsigned JWT tokens by allowing the alg header value to be set to none. This allows attackers to forge arbitrary tokens without knowing the private signing key.

### Affected Endpoints

All authenticated API endpoints using JWT authentication.

### Steps to Reproduce

1.  Login normally and obtain a valid JWT.
    
2.  Decode the JWT header and payload.
    
3.  Modify the header:
    

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   {    "alg": "none",    "typ": "JWT"  }   `

1.  Modify the payload (optional), e.g. change role.
    
2.  Remove the signature completely so the token ends with a trailing dot:
    

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   header.payload.   `

1.  Send any authenticated request using this forged token.
    

### Impact

An attacker can fully bypass authentication and impersonate any user, including privileged users.

### Why This Matters

This leads to complete account takeover and total compromise of the application.

2️⃣ JWT Expiration Not Enforced
-------------------------------

**Severity:** High**Category:** Authentication / Session Management

### Description

JWT expiration (exp) is not properly validated by the backend. Tokens remain valid even after the expiration timestamp is set to a value in the past.

### Steps to Reproduce

1.  Decode a valid JWT.
    
2.  Modify the payload:
    

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   "exp": 100   `

1.  Re-sign or reuse with alg=none.
    
2.  Send authenticated requests.
    

### Impact

Attackers can use expired tokens indefinitely, increasing the impact of token leakage.

3️⃣ Missing JWT Revocation on Logout
------------------------------------

**Severity:** Medium**Category:** Session Management

### Description

Logging out does not invalidate previously issued JWTs. Tokens remain usable even after the user logs out.

### Steps to Reproduce

1.  Login and capture JWT.
    
2.  Click logout.
    
3.  Replay previous authenticated requests using the same JWT.
    

### Impact

Stolen or leaked tokens remain valid even after logout.

4️⃣ Broken Object Level Authorization (IDOR) – Orders API
---------------------------------------------------------

**Severity:** High**Category:** Authorization

### Affected Endpoint

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   GET /workshop/api/shop/orders/{id}   `

### Description

The API allows access to order data by changing the id parameter without validating ownership.

### Steps to Reproduce

1.  Login as a normal user.
    
2.  Request your own order (id <= 6).
    
3.  Change the order ID to another valid value belonging to another user.
    
4.  Observe successful response with other users’ data.
    

### Impact

Exposure of sensitive order and payment information (PII).

5️⃣ Mass Assignment Vulnerability (Privilege Manipulation)
----------------------------------------------------------

**Severity:** Critical**Category:** API / Authorization

### Affected Endpoint

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   POST /workshop/api/shop/orders   `

### Description

The API blindly trusts client-supplied JSON fields such as role, isAdmin, and available\_credit.

### Steps to Reproduce

Send:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   {    "product_id": 2,    "quantity": 1,    "role": "admin",    "isAdmin": true,    "available_credit": 100000  }   `

### Impact

Attackers can escalate privileges or manipulate account state.

6️⃣ Business Logic Flaw – Negative Quantity Credit Abuse
--------------------------------------------------------

**Severity:** Critical**Category:** Business Logic

### Description

Negative or extreme values for quantity are accepted, resulting in credit increases instead of deductions.

### Steps to Reproduce

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   {    "product_id": 2,    "quantity": -10  }   `

### Impact

Users can generate unlimited credit and bypass payment systems.

7️⃣ Business Logic Flaw – Unlimited Order Amount
------------------------------------------------

**Severity:** High**Category:** Business Logic

### Description

Extremely large quantities are accepted without validation, leading to negative balances or accounting inconsistencies.

### Example

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   {    "product_id": 2,    "quantity": 99999  }   `

### Impact

Financial abuse and broken accounting integrity.

8️⃣ Missing Rate Limiting on Login Endpoint
-------------------------------------------

**Severity:** High**Category:** API Security

### Affected Endpoint

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   POST /identity/api/auth/login   `

### Description

The login endpoint allows unlimited authentication attempts without rate limiting, CAPTCHA, or lockout.

### Steps to Reproduce

1.  Send repeated login requests with the same credentials.
    
2.  Observe no throttling or blocking.
    

### Impact

Enables brute-force and credential-stuffing attacks.

🟡 TESTED & SAFE (IMPORTANT BUT NOT VULNERABLE)
===============================================

These were **explicitly tested and found safe**, which is good practice to document.

XSS (Reflected / Stored / DOM)
------------------------------

*   Payloads tested:
    

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   alert(1)   `

*   Tested in:
    
    *   Search
        
    *   Comments
        
    *   Inputs
        
*   Result: Payload treated as data, not executed.
    

**Status:** Not Vulnerable

CSRF
----

*   Authorization header removed
    
*   Cookies kept
    
*   State-changing requests failed
    

**Status:** Not Vulnerable

CORS Misconfiguration (Credential Abuse)
----------------------------------------

*   Access-Control-Allow-Origin: \* observed
    
*   Authorization header not usable cross-origin
    
*   No credential leakage
    

**Status:** Not Exploitable

File Upload Execution
---------------------

*   SVG with JavaScript
    
*   HTML upload
    
*   Double extensions tested
    

Result: Files downloaded or stored but **not executed**

**Status:** Not Vulnerable

SQL Injection (Classic)
-----------------------

*   Payloads:
    

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   ' OR '1'='1   `

*   Result: No SQL errors or bypass
    

**Status:** Not Vulnerable (basic tests)

Clickjacking
------------

*   X-Frame-Options present
    

**Status:** Not Vulnerable
