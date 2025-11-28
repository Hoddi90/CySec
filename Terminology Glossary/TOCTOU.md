---
tags:
  - Category/Terminology
aliases:
  - Terminoligy
---


**Definition:**  
TOCTOU (Time-of-Check to Time-of-Use) is a [[race condition]] where a program checks a condition (e.g., permissions, file state) and then later _uses_ the result, but the system changes in between, breaking the original assumption.

**Context / Example:**  
- **How/where it’s used:**  
	Classic OS/security bug: a program checks that an operation is safe (like “is this file writable and owned by this user?”), then performs the operation later. An attacker changes the file or environment between those two moments.
- **Concrete example:**  
	A setuid-root program checks that `/tmp/config` is a regular file owned by the user. After the check but before opening it, the attacker quickly swaps `/tmp/config` for a symlink to `/etc/shadow`. The program then opens `/etc/shadow` with elevated privileges, leaking or modifying sensitive data.

**Related Concepts:**  
Links to other terms.
- [[Race condition]]
- [Related term 2]