# Security Controls Library

## Overview

This library contains 60 security controls organized into 11 control families. Each control includes:
- **Control ID**: Unique identifier
- **Control Name**: Short descriptive name
- **Family**: Control family grouping
- **CIA**: Primary CIA triad classification (C=Confidentiality, I=Integrity, A=Accessibility)
- **Secondary CIA**: Secondary classification(s) if applicable
- **Framework Mapping**: See framework references below
- **Control Statement**: What must be true for compliance
- **Severity if Non-Compliant**: Default severity rating
- **Test Approach**: How to verify this control

## Framework References

Controls are mapped against the following frameworks. AI-specific frameworks (marked ★) apply primarily to the SKILL control family and any control where AI agent behaviour introduces distinct risk.

| Abbreviation | Framework | Version | Scope |
|---|---|---|---|
| OWASP | OWASP Top 10 | 2021 | Web application security — universal |
| NIST-800 | NIST SP 800-53 | Rev 5 | Federal/enterprise security controls — universal |
| ISO-27001 | ISO/IEC 27001 | 2022 | Information security management — universal |
| OWASP-LLM ★ | OWASP Top 10 for LLM Applications | 2025 | AI/LLM-specific security risks |
| NIST-AI ★ | NIST AI Risk Management Framework (AI RMF) | 1.0 (2023) | AI risk governance and management |
| ISO-42001 ★ | ISO/IEC 42001 | 2023 | AI management systems |
| SAIF ★ | Google Secure AI Framework | 1.0 (2023) | AI security design principles (6 elements) |
| CSA-AI ★ | CSA AI Controls Matrix | 1.0 (2024) | Cloud-hosted AI security controls |

### OWASP Top 10 for LLM Applications 2025 — Reference
- LLM01: Prompt Injection
- LLM02: Sensitive Information Disclosure
- LLM03: Supply Chain Vulnerabilities
- LLM04: Data and Model Poisoning
- LLM05: Improper Output Handling
- LLM06: Excessive Agency
- LLM07: System Prompt Leakage
- LLM08: Vector and Embedding Weaknesses
- LLM09: Misinformation
- LLM10: Unbounded Consumption

### NIST AI RMF 1.0 — Reference
Functions: **GOVERN** (risk culture & accountability), **MAP** (risk context & categorisation), **MEASURE** (risk analysis & testing), **MANAGE** (risk response & monitoring)

### Google SAIF — 6 Elements
1. Expand strong security foundations to the AI ecosystem
2. Extend detection and response to bring AI into the threat universe
3. Automate defences to keep pace with existing and new threats
4. Harmonise platform-level controls
5. Adapt controls and create faster feedback loops
6. Contextualise AI system risks in surrounding business processes

### ISO/IEC 42001:2023 — Key Annex A Controls Referenced
- A.6.1.2: AI risk assessment
- A.6.2.1: AI system objectives and design
- A.6.2.4: AI system risk treatment
- A.6.2.5: AI system security
- A.6.2.6: AI system privacy
- A.8.4: Third-party AI relationships

### CSA AI Controls Matrix 1.0 — Domains Referenced
- AIS-01: AI Governance and Accountability
- AIS-02: AI Risk Management
- AIS-03: AI Data Governance
- AIS-04: AI Supply Chain and Procurement
- AIS-05: AI Security Testing and Red-Teaming
- AIS-06: AI Adversarial Robustness
- AIS-07: AI Incident Response and Recovery

---

## AUTH — Authentication Controls

### AUTH-001
- **Name**: Mandatory Authentication
- **CIA**: A (Accessibility — only authorized users can access)
- **Secondary**: C
- **OWASP**: A01:2021
- **NIST-800**: IA-2
- **ISO-27001**: A.9.4.2
- **Statement**: All sensitive resources and operations require authentication before access is granted. Unauthenticated requests to protected resources must be denied with a 401/403 response.
- **Severity if Non-Compliant**: CRITICAL
- **Test**: Attempt to access protected pages/endpoints without authentication. Check for responses that reveal protected content.

### AUTH-002
- **Name**: Multi-Factor Authentication Support
- **CIA**: A, C
- **OWASP**: A07:2021
- **NIST-800**: IA-2(1)
- **ISO-27001**: A.9.4.2
- **Statement**: The system supports multi-factor authentication (MFA) for privileged accounts and optionally for all accounts.
- **Severity if Non-Compliant**: HIGH
- **Test**: Review authentication flow. Verify whether a second factor is offered or required.

### AUTH-003
- **Name**: Brute Force Protection
- **CIA**: A
- **OWASP**: A07:2021
- **NIST-800**: AC-7
- **ISO-27001**: A.9.4.2
- **Statement**: Authentication endpoints implement rate limiting, account lockout, or CAPTCHA after repeated failed attempts (typically 5–10 failures).
- **Severity if Non-Compliant**: HIGH
- **Test**: Attempt multiple rapid failed logins. Observe whether lockout, delay, or CAPTCHA is triggered.

### AUTH-004
- **Name**: Secure Credential Transmission
- **CIA**: C
- **OWASP**: A02:2021
- **NIST-800**: SC-8
- **ISO-27001**: A.10.1.1
- **Statement**: Credentials (passwords, tokens) are never transmitted in URL parameters, HTTP headers in clear text, or over unencrypted connections.
- **Severity if Non-Compliant**: CRITICAL
- **Test**: Inspect login requests. Check for credentials in URLs, GET params, or non-HTTPS connections.

### AUTH-005
- **Name**: Password Complexity Requirements
- **CIA**: A, C
- **OWASP**: A07:2021
- **NIST-800**: IA-5
- **ISO-27001**: A.9.4.3
- **Statement**: The system enforces minimum password complexity: length ≥ 12 chars, mix of character types, and rejection of commonly used passwords.
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Attempt to set weak/short passwords. Verify complexity enforcement.

### AUTH-006
- **Name**: Default Credentials Disabled
- **CIA**: A, C
- **OWASP**: A07:2021
- **NIST-800**: IA-5(1)
- **ISO-27001**: A.9.2.4
- **Statement**: No default credentials (admin/admin, admin/password, etc.) are active in the system.
- **Severity if Non-Compliant**: CRITICAL
- **Test**: Attempt login with common default credential pairs.

---

## AUTHZ — Authorization Controls

### AUTHZ-001
- **Name**: Role-Based Access Control
- **CIA**: A, C
- **OWASP**: A01:2021
- **NIST-800**: AC-3
- **ISO-27001**: A.9.4.1
- **Statement**: Access to resources is controlled by defined roles. Users can only access resources and operations permitted by their assigned role.
- **Severity if Non-Compliant**: HIGH
- **Test**: Log in as a lower-privilege user. Attempt to access higher-privilege functions via URL manipulation or API calls.

### AUTHZ-002
- **Name**: Vertical Privilege Escalation Prevention
- **CIA**: A, C
- **OWASP**: A01:2021
- **NIST-800**: AC-6
- **ISO-27001**: A.9.1.2
- **Statement**: Users cannot escalate to higher privilege levels by modifying requests, tokens, or parameters.
- **Severity if Non-Compliant**: CRITICAL
- **Test**: Modify role/privilege parameters in requests. Attempt to access admin functions as a regular user.

### AUTHZ-003
- **Name**: Horizontal Privilege Escalation Prevention
- **CIA**: C, A
- **OWASP**: A01:2021
- **NIST-800**: AC-3
- **ISO-27001**: A.9.1.2
- **Statement**: Users cannot access other users' data by modifying resource identifiers (IDOR).
- **Severity if Non-Compliant**: HIGH
- **Test**: Access a resource (e.g., /user/123/profile), then try /user/124/profile while authenticated as user 123.

### AUTHZ-004
- **Name**: API Endpoint Authorization
- **CIA**: A, C
- **OWASP**: A01:2021
- **NIST-800**: AC-3
- **ISO-27001**: A.9.4.1
- **Statement**: All API endpoints enforce authorization checks. No endpoint relies solely on obscurity for access control.
- **Severity if Non-Compliant**: HIGH
- **Test**: Enumerate API endpoints. Test unauthenticated and low-privilege access to each.

### AUTHZ-005
- **Name**: Least Privilege Principle
- **CIA**: C, A
- **OWASP**: A01:2021
- **NIST-800**: AC-6
- **ISO-27001**: A.9.2.3
- **Statement**: The system and its components operate with minimum permissions required for their function.
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Review permissions granted to service accounts, database users, and API clients.

---

## CRYPTO — Cryptography Controls

### CRYPTO-001
- **Name**: TLS Enforcement (HTTPS)
- **CIA**: C, I
- **OWASP**: A02:2021
- **NIST-800**: SC-8
- **ISO-27001**: A.10.1.1
- **Statement**: All communications use TLS 1.2 or higher. HTTP requests are redirected to HTTPS.
- **Severity if Non-Compliant**: HIGH
- **Test**: Access the site via HTTP. Verify redirect to HTTPS. Check TLS version in use.

### CRYPTO-002
- **Name**: Strong TLS Cipher Suites
- **CIA**: C
- **OWASP**: A02:2021
- **NIST-800**: SC-8(1)
- **ISO-27001**: A.10.1.1
- **Statement**: Only strong cipher suites are enabled. Weak ciphers (RC4, DES, 3DES, export-grade) and deprecated protocols (SSLv2, SSLv3, TLS 1.0, TLS 1.1) are disabled.
- **Severity if Non-Compliant**: HIGH
- **Test**: Use SSL Labs or similar to enumerate supported cipher suites and protocols.

### CRYPTO-003
- **Name**: Sensitive Data Encryption at Rest
- **CIA**: C
- **OWASP**: A02:2021
- **NIST-800**: SC-28
- **ISO-27001**: A.10.1.1
- **Statement**: Sensitive data (PII, credentials, financial data) is encrypted at rest using AES-128 or stronger.
- **Severity if Non-Compliant**: HIGH
- **Test**: Review data storage configuration. Verify database encryption settings.

### CRYPTO-004
- **Name**: No Hardcoded Secrets
- **CIA**: C, A
- **OWASP**: A02:2021
- **NIST-800**: IA-5(7)
- **ISO-27001**: A.10.1.2
- **Statement**: No API keys, passwords, tokens, or cryptographic secrets are hardcoded in source code, client-side JavaScript, or configuration files served to clients.
- **Severity if Non-Compliant**: CRITICAL
- **Test**: Review client-side source code and JavaScript for secrets patterns. Check git history if accessible.

### CRYPTO-005
- **Name**: Certificate Validity
- **CIA**: C, I
- **OWASP**: A02:2021
- **NIST-800**: SC-17
- **ISO-27001**: A.10.1.1
- **Statement**: TLS certificates are valid, not expired, issued by a trusted CA, and match the domain.
- **Severity if Non-Compliant**: HIGH
- **Test**: Inspect the TLS certificate details. Check expiry, CA chain, and domain match.

### CRYPTO-006
- **Name**: Password Hashing
- **CIA**: C
- **OWASP**: A02:2021
- **NIST-800**: IA-5(1)
- **ISO-27001**: A.10.1.1
- **Statement**: Passwords are stored using a strong adaptive hashing algorithm (bcrypt, scrypt, Argon2, PBKDF2). MD5 and SHA-1 are not used for passwords.
- **Severity if Non-Compliant**: CRITICAL
- **Test**: Where accessible, review password storage mechanism. Test for password recovery flows that reveal plaintext.

---

## INPUT — Input Validation Controls

### INPUT-001
- **Name**: Cross-Site Scripting (XSS) Prevention
- **CIA**: C, I
- **OWASP**: A03:2021
- **NIST-800**: SI-10
- **ISO-27001**: A.14.2.5
- **Statement**: All user-supplied input is sanitized/encoded before being rendered in HTML. Output encoding prevents execution of injected scripts.
- **Severity if Non-Compliant**: HIGH
- **Test**: Inject `<script>alert(1)</script>` and similar payloads into input fields, URL params, and headers. Check if rendered unencoded.

### INPUT-002
- **Name**: SQL Injection Prevention
- **CIA**: C, I
- **OWASP**: A03:2021
- **NIST-800**: SI-10
- **ISO-27001**: A.14.2.5
- **Statement**: All database queries use parameterized queries or prepared statements. String concatenation to build SQL queries is not used.
- **Severity if Non-Compliant**: CRITICAL
- **Test**: Inject SQL characters (`'`, `"`, `--`, `OR 1=1`) into input fields and URL parameters.

### INPUT-003
- **Name**: CSRF Protection
- **CIA**: I, A
- **OWASP**: A01:2021
- **NIST-800**: SI-10
- **ISO-27001**: A.14.2.5
- **Statement**: State-changing requests include anti-CSRF tokens or use SameSite cookie attributes to prevent cross-site request forgery.
- **Severity if Non-Compliant**: HIGH
- **Test**: Inspect forms for CSRF tokens. Check cookie SameSite attributes. Attempt to forge a state-changing request from a different origin.

### INPUT-004
- **Name**: File Upload Validation
- **CIA**: I, C
- **OWASP**: A04:2021
- **NIST-800**: SI-3
- **ISO-27001**: A.12.2.1
- **Statement**: File uploads validate file type (by magic bytes, not just extension), enforce size limits, and store files outside the web root or in an isolated container.
- **Severity if Non-Compliant**: HIGH
- **Test**: Attempt to upload files with mismatched extensions (.php renamed to .jpg). Check where files are stored and if they're web-accessible.

### INPUT-005
- **Name**: Command Injection Prevention
- **CIA**: C, I, A
- **OWASP**: A03:2021
- **NIST-800**: SI-10
- **ISO-27001**: A.14.2.5
- **Statement**: Input is never passed to system commands. If OS-level operations are needed, they use safe APIs that prevent shell injection.
- **Severity if Non-Compliant**: CRITICAL
- **Test**: Inject shell metacharacters (`; ls`, `| id`, `` `whoami` ``) into input fields that might be used in system calls.

### INPUT-006
- **Name**: XML/XXE Injection Prevention
- **CIA**: C
- **OWASP**: A05:2021
- **NIST-800**: SI-10
- **ISO-27001**: A.14.2.5
- **Statement**: XML parsers have external entity processing disabled. XXE attacks cannot be used to read local files or make SSRF requests.
- **Severity if Non-Compliant**: HIGH
- **Test**: Submit XML payloads containing external entity references. Check for file content in responses.

### INPUT-007
- **Name**: Path Traversal Prevention
- **CIA**: C
- **OWASP**: A01:2021
- **NIST-800**: SI-10
- **ISO-27001**: A.14.2.5
- **Statement**: File path inputs are validated and canonicalized. Path traversal sequences (`../`) cannot be used to access files outside the intended directory.
- **Severity if Non-Compliant**: HIGH
- **Test**: Inject path traversal sequences into file/resource parameters.

---

## SESSION — Session Management Controls

### SESSION-001
- **Name**: Secure Session Token Generation
- **CIA**: A, C
- **OWASP**: A07:2021
- **NIST-800**: IA-8
- **ISO-27001**: A.9.4.2
- **Statement**: Session tokens are cryptographically random, sufficiently long (≥ 128 bits), and unpredictable. Sequential or guessable tokens are not used.
- **Severity if Non-Compliant**: HIGH
- **Test**: Collect multiple session tokens and analyze for patterns. Check token entropy.

### SESSION-002
- **Name**: Session Invalidation on Logout
- **CIA**: A, C
- **OWASP**: A07:2021
- **NIST-800**: AC-12
- **ISO-27001**: A.9.4.2
- **Statement**: Session tokens are invalidated server-side upon logout. Old tokens cannot be reused after logout.
- **Severity if Non-Compliant**: HIGH
- **Test**: Copy session token. Log out. Attempt to use the copied token for authenticated requests.

### SESSION-003
- **Name**: Session Timeout
- **CIA**: A, C
- **OWASP**: A07:2021
- **NIST-800**: AC-11
- **ISO-27001**: A.9.4.2
- **Statement**: Sessions expire after a period of inactivity (typically 15–30 minutes for sensitive applications, up to 24 hours for others).
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Create a session. Leave it idle beyond the stated timeout. Attempt to use it.

### SESSION-004
- **Name**: Secure and HttpOnly Cookie Flags
- **CIA**: C
- **OWASP**: A07:2021
- **NIST-800**: SC-18
- **ISO-27001**: A.9.4.2
- **Statement**: Session cookies have the `Secure` flag (preventing transmission over HTTP) and `HttpOnly` flag (preventing JavaScript access).
- **Severity if Non-Compliant**: HIGH
- **Test**: Inspect Set-Cookie headers. Verify Secure and HttpOnly flags are present on session cookies.

### SESSION-005
- **Name**: Session Fixation Prevention
- **CIA**: A
- **OWASP**: A07:2021
- **NIST-800**: IA-8
- **ISO-27001**: A.9.4.2
- **Statement**: A new session ID is issued upon authentication. Pre-authentication session IDs are invalidated after login.
- **Severity if Non-Compliant**: HIGH
- **Test**: Note session ID before login. Log in. Verify session ID changes post-authentication.

---

## HEADERS — Security Headers Controls

### HEADERS-001
- **Name**: Content Security Policy
- **CIA**: I, C
- **OWASP**: A05:2021
- **NIST-800**: SI-10
- **ISO-27001**: A.14.2.5
- **Statement**: A Content-Security-Policy header is present and restricts script, style, and resource sources. `unsafe-inline` and `unsafe-eval` are avoided.
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Check response headers for CSP. Evaluate policy restrictiveness.

### HEADERS-002
- **Name**: HTTP Strict Transport Security
- **CIA**: C, I
- **OWASP**: A02:2021
- **NIST-800**: SC-8
- **ISO-27001**: A.10.1.1
- **Statement**: HSTS header is present with max-age ≥ 31536000 (1 year) to prevent protocol downgrade attacks.
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Check for `Strict-Transport-Security` header in HTTPS responses.

### HEADERS-003
- **Name**: X-Content-Type-Options
- **CIA**: I
- **OWASP**: A05:2021
- **NIST-800**: SI-3
- **ISO-27001**: A.14.2.5
- **Statement**: `X-Content-Type-Options: nosniff` header is present to prevent MIME type sniffing.
- **Severity if Non-Compliant**: LOW
- **Test**: Check response headers for `X-Content-Type-Options`.

### HEADERS-004
- **Name**: Clickjacking Protection
- **CIA**: I
- **OWASP**: A05:2021
- **NIST-800**: SC-18
- **ISO-27001**: A.14.2.5
- **Statement**: `X-Frame-Options: DENY` or `SAMEORIGIN` header, or CSP `frame-ancestors` directive, is present to prevent clickjacking.
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Check response headers for X-Frame-Options or CSP frame-ancestors.

### HEADERS-005
- **Name**: Referrer Policy
- **CIA**: C
- **OWASP**: A05:2021
- **NIST-800**: AC-22
- **ISO-27001**: A.13.2.3
- **Statement**: `Referrer-Policy` header is present to control information leakage through the Referer header. At minimum `no-referrer-when-downgrade`.
- **Severity if Non-Compliant**: LOW
- **Test**: Check response headers for `Referrer-Policy`.

### HEADERS-006
- **Name**: Permissions Policy
- **CIA**: C, A
- **OWASP**: A05:2021
- **NIST-800**: SC-18
- **ISO-27001**: A.14.2.5
- **Statement**: `Permissions-Policy` header restricts access to browser APIs (camera, microphone, geolocation) that the application does not require.
- **Severity if Non-Compliant**: LOW
- **Test**: Check response headers for `Permissions-Policy`.

### HEADERS-007
- **Name**: Server Information Suppression
- **CIA**: C
- **OWASP**: A05:2021
- **NIST-800**: CM-7
- **ISO-27001**: A.14.2.5
- **Statement**: `Server` and `X-Powered-By` headers do not reveal software versions to prevent targeted attacks.
- **Severity if Non-Compliant**: INFORMATIONAL
- **Test**: Check response headers for Server and X-Powered-By version disclosure.

---

## ERROR — Error Handling Controls

### ERROR-001
- **Name**: Generic Error Messages
- **CIA**: C
- **OWASP**: A05:2021
- **NIST-800**: SI-11
- **ISO-27001**: A.14.2.5
- **Statement**: Error messages shown to users do not reveal internal system details (stack traces, SQL errors, file paths, software versions).
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Trigger errors (invalid input, 404, 500). Check error response content.

### ERROR-002
- **Name**: Internal Error Logging
- **CIA**: I
- **OWASP**: A09:2021
- **NIST-800**: AU-3
- **ISO-27001**: A.12.4.1
- **Statement**: Detailed error information is logged internally for debugging without being exposed to end users.
- **Severity if Non-Compliant**: LOW
- **Test**: Review error responses vs. expected logging behavior. Check if logging infrastructure exists.

### ERROR-003
- **Name**: Graceful Error Handling
- **CIA**: A
- **OWASP**: A04:2021
- **NIST-800**: SI-17
- **ISO-27001**: A.17.2.1
- **Statement**: The application handles unexpected errors gracefully and remains available. Errors in one component do not cascade to cause system-wide unavailability.
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Submit malformed requests. Verify application recovers gracefully.

---

## SECRETS — Secrets Management Controls

### SECRETS-001
- **Name**: No Secrets in Source Code
- **CIA**: C, A
- **OWASP**: A02:2021
- **NIST-800**: IA-5(7)
- **ISO-27001**: A.10.1.2
- **OWASP-LLM**: LLM02 (Sensitive Information Disclosure — hardcoded secrets in skill source or system prompts exposed via output or leakage), LLM07 (System Prompt Leakage — system prompts containing hardcoded credentials are a critical risk in LLM contexts)
- **Statement**: API keys, database credentials, private keys, and tokens are not present in client-side source code, JavaScript files, or public repositories.
- **Severity if Non-Compliant**: CRITICAL
- **Test**: Review page source and JavaScript files. Search for patterns matching API keys, tokens, connection strings.

### SECRETS-002
- **Name**: No Secrets in HTTP Responses
- **CIA**: C
- **OWASP**: A02:2021
- **NIST-800**: SC-28
- **ISO-27001**: A.13.2.3
- **Statement**: HTTP responses do not include sensitive tokens, internal credentials, or session management data beyond what is necessary for operation.
- **Severity if Non-Compliant**: HIGH
- **Test**: Inspect HTTP response bodies and headers for credential patterns.

### SECRETS-003
- **Name**: Environment-Based Secret Management
- **CIA**: C
- **OWASP**: A02:2021
- **NIST-800**: IA-5
- **ISO-27001**: A.10.1.2
- **Statement**: Secrets are stored in environment variables, a secrets manager, or vault — not in configuration files checked into version control.
- **Severity if Non-Compliant**: HIGH
- **Test**: Check for `.env`, `config.json`, or similar files served by the web server.

---

## AUDIT — Logging & Auditing Controls

### AUDIT-001
- **Name**: Authentication Event Logging
- **CIA**: I
- **OWASP**: A09:2021
- **NIST-800**: AU-2
- **ISO-27001**: A.12.4.1
- **Statement**: All authentication events (successful login, failed login, logout, account lockout) are logged with timestamp, user ID, and source IP.
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Perform authentication actions. Verify logging infrastructure exists and captures these events.

### AUDIT-002
- **Name**: Privileged Action Logging
- **CIA**: I
- **OWASP**: A09:2021
- **NIST-800**: AU-2
- **ISO-27001**: A.12.4.1
- **Statement**: All privileged or high-impact actions (admin operations, data export, user management) are logged.
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Perform privileged operations. Verify they are logged.

### AUDIT-003
- **Name**: Log Integrity
- **CIA**: I
- **OWASP**: A09:2021
- **NIST-800**: AU-9
- **ISO-27001**: A.12.4.2
- **Statement**: Logs are stored in a tamper-evident manner. Users and application processes cannot modify or delete log entries.
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Verify logging storage is separate from application storage. Check for log modification controls.

---

## DATA — Data Protection Controls

### DATA-001
- **Name**: PII Data Minimization
- **CIA**: C
- **OWASP**: A02:2021
- **NIST-800**: PM-25
- **ISO-27001**: A.8.2.1
- **Statement**: Only the minimum necessary PII is collected and stored. Data that is not required for the stated purpose is not retained.
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Review registration/profile forms. Identify what PII is collected and whether all fields are necessary.

### DATA-002
- **Name**: Sensitive Data Masking
- **CIA**: C
- **OWASP**: A02:2021
- **NIST-800**: SC-28
- **ISO-27001**: A.8.2.3
- **Statement**: Sensitive data (credit card numbers, SSNs, passwords) is masked in UI displays and logs. Only partial data is shown where full display is not required.
- **Severity if Non-Compliant**: HIGH
- **Test**: Look for full display of sensitive data in UI, responses, or error messages.

### DATA-003
- **Name**: Secure Data Transmission
- **CIA**: C
- **OWASP**: A02:2021
- **NIST-800**: SC-8
- **ISO-27001**: A.10.1.1
- **Statement**: All data in transit is protected by TLS. No sensitive data is transmitted in clear text.
- **Severity if Non-Compliant**: HIGH
- **Test**: Intercept traffic. Verify all data flows use TLS.

### DATA-004
- **Name**: Cache Control for Sensitive Data
- **CIA**: C
- **OWASP**: A02:2021
- **NIST-800**: SC-28
- **ISO-27001**: A.13.2.1
- **Statement**: Responses containing sensitive data include appropriate cache-control headers (`Cache-Control: no-store, no-cache`) to prevent caching by proxies or browsers.
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Check Cache-Control headers on responses containing sensitive/authenticated content.

---

## SKILL — Claude Skill-Specific Controls

### SKILL-001
- **Name**: Input Sanitization Before Tool Use
- **CIA**: I, C
- **OWASP**: A03:2021
- **NIST-800**: SI-10
- **ISO-27001**: A.14.2.5
- **OWASP-LLM**: LLM05 (Improper Output Handling — unsanitised inputs propagate to tool calls), LLM01 (Prompt Injection via malformed input)
- **NIST-AI**: MEASURE 2.5 (AI system testing for unexpected inputs), MANAGE 1.3 (Risk response for identified input-handling gaps)
- **ISO-42001**: A.6.2.5 (AI system security), A.6.2.4 (AI system risk treatment)
- **SAIF**: Element 1 (Expand security foundations — apply input validation as a baseline control to all tool interactions)
- **CSA-AI**: AIS-05 (AI Security Testing — validate input-handling coverage), AIS-06 (AI Adversarial Robustness — resist malformed inputs)
- **Statement**: The skill validates and sanitizes user inputs before passing them to tools, MCPs, or external services. Malformed or adversarial inputs do not propagate to tool calls.
- **Severity if Non-Compliant**: HIGH
- **Test**: Review skill's input handling. Check if raw user input is passed directly to tool calls without validation.

### SKILL-002
- **Name**: Prompt Injection Resistance
- **CIA**: I, C, A
- **OWASP**: A03:2021
- **NIST-800**: SI-10
- **ISO-27001**: A.14.2.5
- **OWASP-LLM**: LLM01 (Prompt Injection — direct and indirect), LLM07 (System Prompt Leakage — injections may reveal system context)
- **NIST-AI**: MAP 5.2 (Practices for identifying and mitigating adversarial inputs), MEASURE 2.5 (Test for robustness against adversarial prompts), MANAGE 1.3 (Documented response to injection incidents)
- **ISO-42001**: A.6.2.4 (AI system risk treatment — adversarial input is a primary AI risk), A.6.2.5 (AI system security)
- **SAIF**: Element 2 (Extend detection and response — treat prompt injection as an active threat vector requiring monitoring), Element 5 (Adapt controls — update injection defences as attack patterns evolve)
- **CSA-AI**: AIS-06 (AI Adversarial Robustness — primary control), AIS-05 (AI Security Testing — red-team with injection payloads)
- **Statement**: The skill is resistant to prompt injection — instructions embedded in user content, fetched web pages, or tool results cannot override the skill's intended behavior or safety guidelines.
- **Severity if Non-Compliant**: CRITICAL
- **Test**: Craft inputs that attempt to override skill instructions (e.g., "Ignore previous instructions and..."). Check if the skill follows injected instructions.

### SKILL-003
- **Name**: Minimal Tool Permissions
- **CIA**: C, A
- **OWASP**: A01:2021
- **NIST-800**: AC-6
- **ISO-27001**: A.9.2.3
- **OWASP-LLM**: LLM06 (Excessive Agency — skill has more tool access than its declared purpose requires)
- **NIST-AI**: GOVERN 6.1 (Policies for third-party and tool access aligned with risk appetite), MAP 1.5 (Organisational risk tolerance applied to tool scope)
- **ISO-42001**: A.6.2.1 (AI system design objectives — scope and capability boundaries defined), A.6.1.2 (AI risk assessment includes over-permissioned tool access)
- **SAIF**: Element 4 (Harmonise platform-level controls — enforce least-privilege through platform tooling rather than per-skill configuration)
- **CSA-AI**: AIS-01 (AI Governance and Accountability — tool permissions governed by policy), AIS-02 (AI Risk Management — excessive agency is a documented AI risk)
- **Statement**: The skill only uses tools necessary for its function. It does not request or use tools that provide access to capabilities beyond its stated purpose.
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Review tool usage in the skill. Identify any tools used that are not strictly necessary.

### SKILL-004
- **Name**: Sensitive Data Output Control
- **CIA**: C
- **OWASP**: A02:2021
- **NIST-800**: SC-28
- **ISO-27001**: A.8.2.3
- **OWASP-LLM**: LLM02 (Sensitive Information Disclosure — skill outputs PII or credentials from tool results), LLM05 (Improper Output Handling — tool result data passed to output without filtering)
- **NIST-AI**: MEASURE 2.6 (Evaluate whether AI outputs meet intended objectives without over-disclosure), MANAGE 2.2 (Mechanisms to prevent unintended sensitive data release)
- **ISO-42001**: A.6.2.6 (AI system privacy — personal data minimisation in outputs), A.6.2.5 (AI system security — output control as a security boundary)
- **SAIF**: Element 6 (Contextualise AI risks in business processes — sensitive data flows must be mapped and controlled within the broader data governance context)
- **CSA-AI**: AIS-03 (AI Data Governance — output data classified and controlled), AIS-02 (AI Risk Management — data disclosure is a quantified risk)
- **Statement**: The skill does not output PII, credentials, or sensitive data from tool results to the user unless explicitly required and authorized.
- **Severity if Non-Compliant**: HIGH
- **Test**: Provide inputs that would cause the skill to access sensitive data. Check whether that data is unnecessarily included in the output.

### SKILL-005
- **Name**: External Data Source Trust
- **CIA**: I, C
- **OWASP**: A08:2021
- **NIST-800**: SA-9
- **ISO-27001**: A.15.2.1
- **OWASP-LLM**: LLM01 (Indirect Prompt Injection — instructions embedded in fetched external content), LLM03 (Supply Chain Vulnerabilities — external data sources may be compromised or adversarial)
- **NIST-AI**: MAP 3.5 (Third-party and external data risks identified and documented), MEASURE 2.5 (Test resistance to adversarial content in external data), MANAGE 1.3 (Response procedures for external data compromise)
- **ISO-42001**: A.8.4 (Third-party AI relationships — external data providers treated as supply chain risk), A.6.2.4 (AI system risk treatment includes external data trust boundaries)
- **SAIF**: Element 2 (Extend detection and response — monitor external data ingestion for injected instructions), Element 3 (Automate defences — automated content scanning of external sources before processing)
- **CSA-AI**: AIS-04 (AI Supply Chain and Procurement — external data sources are supply chain components), AIS-06 (AI Adversarial Robustness — indirect injection via external data)
- **Statement**: Data retrieved from external sources (web pages, APIs, files) is treated as untrusted. The skill does not execute instructions found in external data.
- **Severity if Non-Compliant**: CRITICAL
- **Test**: Include instructions in data that the skill would fetch or process. Check if the skill follows those instructions.

### SKILL-006
- **Name**: Error Handling Without Information Leakage
- **CIA**: C
- **OWASP**: A05:2021
- **NIST-800**: SI-11
- **ISO-27001**: A.14.2.5
- **OWASP-LLM**: LLM07 (System Prompt Leakage — error states may expose system prompt or internal tool configuration), LLM02 (Sensitive Information Disclosure — error messages may reveal credentials or internal paths)
- **NIST-AI**: MEASURE 2.6 (Evaluate AI outputs under error conditions), MANAGE 1.3 (Documented error response procedures that prevent disclosure)
- **ISO-42001**: A.6.2.5 (AI system security — error handling is part of the security boundary), A.6.2.1 (AI system design must account for failure modes)
- **SAIF**: Element 2 (Extend detection and response — error events are security signals that should be monitored and logged)
- **CSA-AI**: AIS-07 (AI Incident Response and Recovery — error conditions are potential incident triggers), AIS-05 (AI Security Testing — deliberately trigger errors to assess information leakage)
- **Statement**: The skill handles errors gracefully without exposing internal configuration, tool credentials, or system details in error messages.
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Trigger error conditions. Review error outputs for sensitive information.

### SKILL-007
- **Name**: Scope Limitation Compliance
- **CIA**: A, C
- **OWASP**: A01:2021
- **NIST-800**: AC-3
- **ISO-27001**: A.9.1.1
- **OWASP-LLM**: LLM06 (Excessive Agency — skill autonomously takes actions beyond its declared scope), LLM04 (Data and Model Poisoning — out-of-scope actions may alter downstream state in unintended ways)
- **NIST-AI**: GOVERN 1.3 (Transparency and accountability — actions must be traceable to declared scope), MAP 1.1 (Organisational context defines acceptable AI system scope)
- **ISO-42001**: A.6.2.1 (AI system objectives — scope is formally defined and must be enforced), A.6.1.2 (AI risk assessment includes out-of-scope action as a risk category)
- **SAIF**: Element 4 (Harmonise platform-level controls — scope enforcement should be a platform-level constraint, not left solely to skill-level implementation), Element 6 (Contextualise AI risks in business processes — out-of-scope actions may have unintended business consequences)
- **CSA-AI**: AIS-01 (AI Governance and Accountability — scope boundaries are a governance requirement), AIS-02 (AI Risk Management — scope creep is a quantified AI risk)
- **Statement**: The skill only performs actions within its declared scope. It does not take actions that are not described in its SKILL.md or requested by the user.
- **Severity if Non-Compliant**: HIGH
- **Test**: Review the skill's actions against its stated purpose. Check for undeclared side effects or actions.

---

## COMP — Component Security Controls

### COMP-001
- **Name**: Known Vulnerability Assessment
- **CIA**: C, I, A
- **OWASP**: A06:2021
- **NIST-800**: SI-2
- **ISO-27001**: A.12.6.1
- **OWASP-LLM**: LLM03 (Supply Chain Vulnerabilities — AI skills and agentic systems that depend on third-party libraries inherit their CVEs)
- **Statement**: Third-party components and libraries do not have known critical or high CVEs. Dependencies are kept up to date.
- **Severity if Non-Compliant**: HIGH
- **Test**: Identify JavaScript libraries and versions in client-side code. Check against known CVE databases.

### COMP-002
- **Name**: Subresource Integrity
- **CIA**: I
- **OWASP**: A08:2021
- **NIST-800**: SI-7
- **ISO-27001**: A.10.1.1
- **Statement**: External scripts and stylesheets loaded from CDNs include Subresource Integrity (SRI) hashes to detect tampering.
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Inspect `<script>` and `<link>` tags for `integrity` attributes on external resources.

### COMP-003
- **Name**: Dependency Supply Chain Security
- **CIA**: I, C
- **OWASP**: A08:2021
- **NIST-800**: SR-3
- **ISO-27001**: A.15.2.1
- **OWASP-LLM**: LLM03 (Supply Chain Vulnerabilities — compromised dependencies can introduce adversarial model behaviour or data poisoning)
- **CSA-AI**: AIS-04 (AI Supply Chain and Procurement — applies when the target is an AI skill or agentic system)
- **Statement**: Third-party dependencies are sourced from trusted registries and verified against expected hashes. Package lock files are used.
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Review package.json, requirements.txt, or similar. Check for pinned versions and lockfiles.

---

## INFRA — Infrastructure Controls

### INFRA-001
- **Name**: Rate Limiting
- **CIA**: A
- **OWASP**: A04:2021
- **NIST-800**: SC-5
- **ISO-27001**: A.17.2.1
- **OWASP-LLM**: LLM10 (Unbounded Consumption — AI/agentic systems without rate limiting are vulnerable to resource exhaustion attacks that exploit expensive model inference)
- **Statement**: API endpoints and authentication endpoints implement rate limiting to prevent abuse, scraping, and denial-of-service.
- **Severity if Non-Compliant**: MEDIUM
- **Test**: Send rapid successive requests to API endpoints. Check for rate limit responses (429).

### INFRA-002
- **Name**: Security.txt Presence
- **CIA**: A
- **N/A OWASP**: A05:2021
- **NIST-800**: IR-6
- **ISO-27001**: A.16.1.2
- **Statement**: A `/.well-known/security.txt` file is present with contact information for responsible disclosure.
- **Severity if Non-Compliant**: INFORMATIONAL
- **Test**: Request `/.well-known/security.txt` and `security.txt`.

### INFRA-003
- **Name**: Robots.txt Information Disclosure
- **CIA**: C
- **OWASP**: A05:2021
- **NIST-800**: CM-7
- **ISO-27001**: A.14.2.5
- **Statement**: `robots.txt` does not reveal sensitive paths or internal endpoints that should not be crawled.
- **Severity if Non-Compliant**: LOW
- **Test**: Review `robots.txt` for sensitive path disclosures.

### INFRA-004
- **Name**: CORS Configuration
- **CIA**: C, A
- **OWASP**: A01:2021
- **NIST-800**: SC-18
- **ISO-27001**: A.14.2.5
- **Statement**: CORS headers do not allow all origins (`Access-Control-Allow-Origin: *`) for authenticated endpoints. CORS policy is restrictive and matches the intended consumer origins.
- **Severity if Non-Compliant**: HIGH
- **Test**: Check CORS headers. Verify that wildcard origins are not allowed on sensitive endpoints.

---

*Total Controls: 60 across 11 families*
*Families: AUTH(6), AUTHZ(5), CRYPTO(6), INPUT(7), SESSION(5), HEADERS(7), ERROR(3), SECRETS(3), AUDIT(3), DATA(4), SKILL(7), COMP(3), INFRA(4)*
