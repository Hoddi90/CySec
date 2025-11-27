---
tags:
  - Category/Terminology
aliases:
  - Terminoligy
---


**Definition:**  
Mandatory Access Control (MAC) is an access control model where a central authority defines strict policies about who can access which resources, and users cannot override or change these rules.

**Context / Example:**  
- **How/where it’s used:**  
	Used in high-security environments (military, government, some servers) where data is labeled with security levels (e.g., “confidential,” “secret”) and users have clearances. The system enforces rules like “no read up, no write down,” regardless of file ownership.
- **Concrete example:**  
	On a Linux system with [[SELinux]] enabled, even if a process “owns” a file, [[SELinux]] policies can prevent it from reading or writing that file if the security labels and policy rules don’t allow it, blocking potential malware or privilege abuse.

**Related Concepts:**  
Links to other terms.
- [[DAC]]
- [[SELinux]]