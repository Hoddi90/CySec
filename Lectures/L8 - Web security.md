---
tags:
  - Category/Lecture-Notes
aliases:
  - Lecture-Note
---
HTTP was invented to share static documents. It was designed to be **stateless** and **open by default**. Today we use this same protocol for banking, healthcare, and critical infrastructure. We are forcing a protocol designed for sharing to perform tasks requiring secrecy and rigid control.

**The golden rule of web security:** **“Never trust the client.”** The client is easily compromised. **All security validation must happen on the server.**

In modern web development, the attack surface is split between:

- **Server** (our backend)
- **Client** (the user’s browser)

## Server-Side Attack Surface

1. **Visible inputs** → Forms (login, search), file uploads (webshells)
2. **Hidden inputs** → URL/parameters (?id=5), HTTP headers (User-Agent, Referer), cookies
3. **API layer** → Exposed REST/GraphQL endpoints, Broken Object Level Authorization (BOLA/IDOR)
4. **Supply chain** → Insecure third-party libraries or dependencies

## Client-Side Attack Surface

The attacker targets the user within our application context:

1. **The DOM** → DOM-based XSS (tricking the browser into running attacker code)
2. **Client-side storage** → Tokens stolen via XSS from localStorage/sessionStorage
3. **Third-party scripts** → Magecart/formjacking via analytics, chatbots, ad networks

## OWASP Top 10

A standard awareness document listing the most critical security risks to web applications.

> Good news: Most malicious bots go for low-hanging fruit. Reasonable automated defenses keep the majority at bay.

**Risk = Likelihood × Impact**

## Key Vulnerabilities & Fixes

| Vulnerability                                | Description                                                              | Main Mitigation                                                                                                                                                             |
| -------------------------------------------- | ------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **SQL Injection (SQLi)**                     | Untrusted data sent to database interpreter as part of a command         | Use prepared statements / parameterized queries (never concatenate strings, use the database's drive built-in placeholder system make the database treat the input as data) |
| **Insecure Direct Object References (IDOR)** | Direct access to objects via user input without authorization check      | Always verify ownership/authorisation on the server before returning data                                                                                                   |
| **Broken Authentication**                    | Weak passwords, no lockout, session IDs in URLs, poor session management | Use Multi-Factor Authentication and standard, battle-tested authentication libraries                                                                                        |
| **Cross-Site Scripting (XSS)**               | Attacker injects script that runs in other users’ browsers               | Convert “<” to “&lt;” so the comment will be rendered as text, not code.                                                                                                    |
| **Reflected XSS**                            | Input immediately echoed back (search results, error messages)           | Same as XSS above                                                                                                                                                           |
| **Attribute Injection**                      | Breaking out of HTML to add event handlers                               | Same as above.                                                                                                                                                              |
| **Session Stealing**                         | Stealing cookies/JWTs via XSS to impersonate user                        | Use HttpOnly, if XSS succeeds, the attacker can't steal the session.  Use an HTTP header that tells the browser which scripts are allowed to run.                           |

### Core XSS Defenses

1. Convert special characters to HTML entities before rendering
2. Flag session cookies as **HttpOnly** (JS can’t read them)
3. Use **Content-Security-Policy (CSP)** headers to restrict allowed scripts

### Authentication & Authorization Best Practices

1. Do not implement authentication all by yourself
2. Use external well-tested libraries or delegate (OAuth 2.0, etc.)

## The Hacker’s Toolbox

### 1. Reconnaissance

- Browser DevTools (F12) → Network & Storage tabs to find the target's API requests, headers and hidden parameters and sensitive data in LocalStorage or Cookies.
- Wappalyzer → identify the technology stack & whether any software versions is outdated.
- DNSDumpster → find subdomains and map the organization's attack service without touching the target

### 2. Directory/Path Brute-Forcing

- **Use Nmap** (Network mapper) for network discovery. Pair it with the Nmap Scripting Engine (NSE) to deteck know vulnerabilites automatically.
- **Use Gobuster/Dirb** to find hidden paths like /admin, /backup, /.git, or /config.php. It tests thousands of common filenames against the web server.

### 3. Interception Proxies

- **Use Burp Suite** to act as a “Man-in-the-Middle” between your browser and the server. It captures a request, modifies one parameter and sends it back. You can observe the result and repeat the process as many times as you like or need.
- **Use OWASP ZAP** (Zed attack proxy), the open-source alternative to burp. The same but offers automated scanning

### 4. Specialized Scanners

- **Use SQLMap** to automate the detection and exploitation of SQL Injection flaws. It can dump entire databases with a single command.
- **Use Nikto** to check for outdated server version (Apache/Nginx), default files and insecure configurations. Find the low hanging fruit.

## Specific Vulnerabilities Deep-Dive

### CSRF (Cross-Site Request Forgery)

**What is it?** Cross site request forgery is an attack that forces an end user to execute unwanted actions on a web application in which they are currently authenticated. Often done by sending a malware link via email or chat.

**Differs from XSS?** XSS runs script in the victim’s browser; CSRF tricks the victim’s browser into making legitimate-looking requests using existing credentials.

**Mitigation**

- Synchronizer Token Pattern (anti-CSRF tokens) where tokens are generated on the server side and only once per user session or request. Because the time range for an attacker to exploit the stolen tokens is minimal for per-request tokens, they are more secure than per-session tokens.

**OWASP Top 10 (2025)** → Part of **A01:2025 – Broken Access Control**

### SSRF (Server-Side Request Forgery)

**What is it?** Server-Side request forgery is an attack where the attacker can abuse functionality on the server to read or update internal resources. The attacker can supply or modify a URL which the code running on the server will read or submit data to.

**Potential impact**

- Read various server configurations such as AWS metadata
- Connect to internal services e.g. http enabled databases
- POST requests to internal services which are not intended to be exposed

**Primary defense**: A **strict allow-list validation** at the application layer. Applications should permit only a predefined set of trusted domains, IP ranges, or URL patterns. Strong validation should

- Use secure, well-tested parsing libraries
- Reject redirects or re-validate redirect targets
- Block private and link-local IP ranges (e.g., 127.0.0.1, 10.0.0.0/8, 169.254.169.254).
- Avoid performing DNS resolution during initial validation to prevent information exposure and DNS rebinding issues

When an application must legitimately access arbitrary public URLs—such as for webhook callbacks or URL preview, a more permissive design requires additional safeguards such as:

- Strict block-lists for private/internal IP ranges
- Validating URL format and resolving the hostname at request time
- Ensuring the resolved IP is public and re-checking after any redirect
- Disabling automatic redirects entirely where possible

**OWASP Top 10 (2025)** → Part of **A01:2025 – Broken Access Control**

### Insecure Deserialization → Remote code execution (RCE)

**Serialization** → converting objects to byte stream (e.g., for cookies, session files). **Deserialization** → reconstructing the object from the byte stream.

**How it becomes RCE**: Many frameworks (Java, PHP, .NET, Python pickle, etc.) execute certain methods automatically during deserialization (magic methods, gadget chains). If the server blindly deserializes untrusted data (e.g., a tampered cookie), the attacker can craft a serialized object that triggers malicious code execution when deserialized.

**Example (Java)** Attacker replaces a normal serialized session object with one containing a malicious gadget chain → server runs Runtime.exec() or similar upon deserialization → full RCE.

**OWASP Category** → **A08:2025 – Software and Data Integrity Failures**

**Mitigations**

- Never deserialize untrusted input
- Use safe formats (JSON instead of Java serialization/pickle)
- Integrity checks (signing/HMAC) on serialized data
- Run deserialization in sandboxed/low-privilege context if unavoidable

Lecture Title

**Date:** {{26.11.2025}}
**Created:** {{02.12.2025}}

---

## Key Concepts & Takeaways

- [Placeholder]
- [Placeholder]
- [Placeholder]

---

## Connections to Earlier Material

- [New topic] → relates to [old topic] because…
- [ ]

---

## Questions for Discussion / Research

- [Placeholder]
- [Placeholder]
- [Placeholder]

---

## Diagrams / Examples / Code

### Diagram / Example
- [Short description]

```python
[ASCII sketch or notes about diagram]
# paste code example
Code Snippet
lang
Copy code
# paste code example
```
