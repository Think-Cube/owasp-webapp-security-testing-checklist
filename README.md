# 🧰 OWASP Web Application Security Testing Checklist
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Aligned with [OWASP Web Security Testing Guide (WSTG) v4.2](https://owasp.org/www-project-web-security-testing-guide/) and [OWASP API Security Top 10 (2023)](https://owasp.org/API-Security/editions/2023/en/0x00-header/). Covers web application, API, client-side, and AI/LLM security testing.

> **Last reviewed:** October 2026

---

## 🕵️ 1. Information Gathering
- [ ] 🔍 Explore the application manually and identify entry points.
- [ ] 🕸️ Perform automated crawling and hidden content discovery.
- [ ] 📄 Review `robots.txt`, `sitemap.xml`, backups, temp files.
- [ ] 🌐 Enumerate subdomains and related applications.
- [ ] 🧩 Identify technologies, frameworks, and versions used.
- [ ] 🖥️ Collect server and application fingerprints.
- [ ] 🪶 Inspect HTML, comments, and metadata for sensitive info.
- [ ] 👥 Identify all user roles and access levels.
- [ ] ⚙️ List all hostnames, ports, and third-party integrations.
- [ ] 🔗 Discover and analyze API endpoints (REST, GraphQL, gRPC).

---

## ⚙️ 2. Configuration & Deployment Management
- [ ] 🧭 Identify admin interfaces or exposed management panels.
- [ ] 🧹 Check for old, backup, or unreferenced files.
- [ ] 🧱 Verify restricted HTTP methods (e.g., disable `PUT`, `TRACE`).
- [ ] 🧾 Test for security headers (`CSP`, `HSTS`, `X-Frame-Options`, etc.).
- [ ] 🔒 Validate HTTPS / TLS configuration and certificate chain (TLS 1.2+ only; TLS 1.0 and 1.1 are deprecated).
- [ ] 🧮 Confirm correct file permissions and environment variables.
- [ ] 🚫 Ensure no production data in test systems (and vice versa).
- [ ] ☁️ Test for exposed cloud storage or misconfigured CDN.
- [ ] 🧩 Check for possible subdomain takeover or orphaned DNS entries.
- [ ] 🧑‍💻 Review CI/CD pipelines for secrets or hardcoded credentials.
- [ ] 🌍 Verify CORS policy is not overly permissive (`Access-Control-Allow-Origin: *` on sensitive endpoints).
- [ ] 🚀 If the application supports **HTTP/3 / QUIC**, verify that TLS is enforced, UDP port 443 is properly secured, and security headers apply equally to HTTP/3 responses.

---

## 👤 3. Identity Management
- [ ] 🆔 Review registration and provisioning flows.
- [ ] 🚷 Test for user enumeration (login, reset, signup).
- [ ] 👥 Verify unique username policies and predictable IDs.
- [ ] 🔄 Validate de-provisioning and role removal processes.
- [ ] ⚖️ Confirm least-privilege principles are applied.

---

## 🔑 4. Authentication Testing
- [ ] 🔐 Verify credentials transmitted only via HTTPS.
- [ ] 🚨 Test for default or weak passwords.
- [ ] 🧭 Test for authentication bypass and forced browsing.
- [ ] ⛔ Check brute-force protection and account lockout.
- [ ] 🧾 Validate password policies (length, complexity, reuse).
- [ ] 💾 Test "Remember Me" token security.
- [ ] 🔁 Review password reset/change flows.
- [ ] 🧠 Verify CAPTCHA / rate-limit on login endpoints.
- [ ] 🛡️ Test MFA / 2FA enforcement and bypass techniques.
- [ ] 🚪 Ensure logout properly invalidates sessions/tokens.
- [ ] 🧩 Test for session fixation and renewal upon login.
- [ ] 🚫 Disable browser autocomplete on password fields.
- [ ] 🧼 Verify sensitive data not cached or stored locally.
- [ ] 🔏 Test **WebAuthn / Passkey** implementation if present — verify origin binding, credential ID uniqueness, and replay protection.
- [ ] 🔄 Validate **OAuth 2.0 / PKCE** flows — verify `code_verifier`, `state` parameter, and redirect URI restrictions.
- [ ] 🔐 If the application uses **OAuth 2.1**, verify that implicit grant and Resource Owner Password Credentials grant are not supported, and that PKCE is enforced for all clients.
- [ ] 🪪 Test federated / social login for account linking and identity confusion attacks.

---

## 🛂 5. Authorization Testing
- [ ] 📁 Test for path traversal and file access control.
- [ ] 🧍 Test for insecure direct object references (IDOR).
- [ ] 🔝 Check for privilege escalation (vertical/horizontal).
- [ ] 🕳️ Test for missing or broken access control.
- [ ] 🧱 Validate access control consistency across APIs.
- [ ] 🪙 Review OAuth / OIDC implementations.

---

## 🧩 6. Session Management
- [ ] 🍪 Identify how sessions are handled (cookies, tokens, JWT).
- [ ] ⚙️ Verify cookie flags (`Secure`, `HttpOnly`, `SameSite`).
- [ ] ⏰ Check session timeout and absolute expiration.
- [ ] 🚪 Confirm session invalidation after logout or inactivity.
- [ ] 🔁 Regenerate session IDs on login / privilege changes.
- [ ] 🔒 Test session ID randomness and predictability.
- [ ] 🧱 Validate HTTPS-only transmission of tokens.
- [ ] 🧿 Test for CSRF and clickjacking protection.
- [ ] 🪪 Review JWT signature algorithm (`alg: none` bypass, RS256 vs HS256 confusion), expiration, and claim integrity.

---

## 🧮 7. Input Validation & Injection
- [ ] 💬 Test for Reflected, Stored, and DOM-based XSS.
- [ ] 🧠 Test for SQL, NoSQL, and ORM Injection.
- [ ] 🧾 Test for XML / XXE and XPath Injection.
- [ ] 🧑‍💻 Test for Command, Code, and Template Injection (SSTI).
- [ ] 🌐 Test for SSRF and HTTP Request Smuggling.
- [ ] ⚙️ Test for HTTP Header and Host Header Injection.
- [ ] 🚏 Test for Open Redirects.
- [ ] 📂 Test for LFI / RFI (File Inclusion).
- [ ] 🧱 Test for Expression Language Injection and Mass Assignment.
- [ ] 🔄 Compare client-side vs. server-side validation rules.
- [ ] 🧬 Test for **Prototype Pollution** in JavaScript/Node.js applications — verify that `__proto__`, `constructor`, and `prototype` properties are sanitized in object merges and deep clones.
- [ ] 🔀 Test for **HTTP Parameter Pollution (HPP)** — send duplicate parameters and verify server-side behavior.
- [ ] 🤖 Test for **Prompt Injection** if the application passes user input to an LLM — verify that system prompts cannot be overridden or leaked (see also Section 13).

---

## 🚨 8. Error Handling & Logging
- [ ] 🧱 Test for verbose error messages and stack traces.
- [ ] 🚫 Validate no sensitive data is leaked in errors or logs.
- [ ] 📋 Confirm security events are logged and monitored.
- [ ] 📡 Verify alerting for critical events (auth failures, privilege changes).

---

## 🔐 9. Cryptography
- [ ] 🔑 Verify encryption of sensitive data (in transit + at rest).
- [ ] 🧮 Test for weak / deprecated algorithms (MD5, SHA-1, RC4, DES).
- [ ] 🧂 Check proper salting and key derivation (PBKDF2, bcrypt, Argon2).
- [ ] 🧰 Validate secure random number generation.
- [ ] 🚫 Detect hardcoded keys or secrets.
- [ ] 🪪 Validate certificate chain and expiry.
- [ ] 🔏 Verify TLS 1.0 and TLS 1.1 are disabled — TLS 1.2 minimum, TLS 1.3 preferred.
- [ ] 🔮 Assess **Post-Quantum Cryptography (PQC) readiness** — verify whether long-lived secrets and certificates are protected against harvest-now-decrypt-later attacks; check if the application roadmap includes migration to NIST-standardized PQC algorithms (ML-KEM, ML-DSA, SLH-DSA).

---

## 🧠 10. Business Logic Testing
- [ ] ⚙️ Test for logic bypasses and workflow manipulation.
- [ ] ⏳ Test for race conditions and timing attacks.
- [ ] 📈 Validate business rule enforcement (limits, quotas).
- [ ] 🧾 Test for missing non-repudiation controls.
- [ ] 🧍‍♂️ Verify separation of duties and privilege boundaries.
- [ ] 📂 Test for unsafe file uploads (type, size, path, scanning).
- [ ] 🧨 Test for malicious file execution after upload.

---

## 🧭 11. Client-Side Security
- [ ] 🧠 Test for DOM-based XSS and client-side injection.
- [ ] 🪶 Test for HTML and CSS Injection.
- [ ] 🌐 Check CORS configuration.
- [ ] 🖼️ Test for clickjacking via frames/iframes.
- [ ] 📬 Verify Web Messaging (`postMessage`) origins and targets.
- [ ] 💬 Test WebSockets for authentication and origin checks.
- [ ] 💾 Check browser storage (LocalStorage, IndexedDB) for secrets.
- [ ] 🔁 Test for Reverse Tabnabbing and open redirects.
- [ ] 🔐 Verify PWA / Service Worker caching security.

---

## 🔗 12. API Security Testing

> Aligned with [OWASP API Security Top 10 – 2023](https://owasp.org/API-Security/editions/2023/en/0x11-t10/).

- [ ] 🌍 Enumerate API endpoints and parameters (including versioned and deprecated endpoints).
- [ ] 🧱 **API1:2023** – Test for Broken Object Level Authorization (BOLA / IDOR).
- [ ] 🔐 **API2:2023** – Test for Broken Authentication (weak tokens, missing expiry, credential stuffing).
- [ ] 🏷️ **API3:2023** – Test for Broken Object Property Level Authorization — excessive data exposure in responses AND mass assignment via writable fields.
- [ ] ⏱️ **API4:2023** – Test for Unrestricted Resource Consumption — verify rate limiting, payload size limits, and query complexity limits (GraphQL).
- [ ] 🔝 **API5:2023** – Test for Broken Function Level Authorization — verify HTTP method restrictions and admin-only endpoint access.
- [ ] 🚦 **API6:2023** – Test for Unrestricted Access to Sensitive Business Flows — verify bot protection and abuse prevention on high-value flows (checkout, login, account creation).
- [ ] 🌐 **API7:2023** – Test for Server Side Request Forgery (SSRF) in API parameters that fetch URLs or resources.
- [ ] ⚙️ **API8:2023** – Test for Security Misconfiguration — CORS, missing security headers, debug endpoints, default credentials.
- [ ] 🗂️ **API9:2023** – Test for Improper Inventory Management — identify shadow APIs, unversioned endpoints, and undocumented paths.
- [ ] 🤝 **API10:2023** – Test for Unsafe Consumption of APIs — verify that the application validates and sanitizes data received from third-party APIs before use.
- [ ] 🪶 Test GraphQL queries and mutations for injection, introspection exposure, and query depth/complexity abuse.

---

## 🤖 13. AI / LLM Security Testing

> Aligned with [OWASP Top 10 for Large Language Model Applications (2025)](https://genai.owasp.org/).

- [ ] 💉 **LLM01** – Test for **Prompt Injection** — attempt to override system prompts via user input, indirect injection through retrieved documents or tool outputs.
- [ ] 🔓 **LLM02** – Test for **Sensitive Information Disclosure** — verify the model does not leak training data, system prompts, PII, or internal API keys in responses.
- [ ] 🔗 **LLM03** – Test for **Supply Chain vulnerabilities** — review third-party model providers, fine-tuning datasets, and plugin/tool integrations.
- [ ] 📊 **LLM04** – Test for **Data and Model Poisoning** — verify controls on fine-tuning pipelines and retrieval-augmented generation (RAG) data sources.
- [ ] 🧰 **LLM05** – Test for **Improper Output Handling** — verify that LLM output is treated as untrusted input; test for XSS, SQLi, and command injection via model responses.
- [ ] ⚡ **LLM06** – Test for **Excessive Agency** — verify that LLM-powered agents have minimum required permissions and confirm high-impact actions with the user.
- [ ] 🛡️ **LLM07** – Test for **System Prompt Leakage** — attempt to extract the system prompt via direct or indirect techniques.
- [ ] 🗃️ **LLM08** – Test for **Vector and Embedding Weaknesses** — test RAG pipelines for poisoned or adversarial documents that manipulate retrieval results.
- [ ] 🔌 **LLM09** – Test for **Misinformation** — verify outputs are grounded and the application includes appropriate disclaimers and human oversight.
- [ ] 🌐 **LLM10** – Test for **Unbounded Consumption** — verify rate limiting and cost controls on LLM API calls to prevent denial-of-wallet attacks.

---

## 🧨 14. Denial of Service
- [ ] 🕳️ Test for resource exhaustion (CPU, memory, I/O).
- [ ] ⏱️ Verify rate limiting and throttling mechanisms.
- [ ] 🧮 Test for regex or SQL wildcard DoS (ReDoS).
- [ ] 📦 Test oversized payload and file upload handling.

---

## 🧾 15. Reporting & Documentation
- [ ] 🧭 Document all findings with WSTG IDs, risk level, and PoC.
- [ ] 🗂️ Map findings to OWASP Top 10 and OWASP API Security Top 10 (2023) categories.
- [ ] 🧰 Provide clear remediation steps and references.
- [ ] 🔐 Store test results securely and restrict access.

---

## License

MIT © [Think-Cube](https://github.com/Think-Cube)

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.
