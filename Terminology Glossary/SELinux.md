---
tags:
  - Category/Terminology
aliases:
  - Terminoligy
---


**Definition:**  
SELinux (Security-Enhanced Linux) is a Linux security module that enforces Mandatory Access Control (MAC) policies using fine-grained labels on processes and objects, limiting what each process can do even if it’s running as root.

**Context / Example:**  
- **How/where it’s used:**  
	Used on many servers and Linux distributions (e.g., Fedora, RHEL, CentOS) to confine services like web servers or databases. Even if an attacker compromises a service, SELinux policies can restrict file access, network actions, and privilege escalation.
- **Concrete example:**  
	An Apache web server running under SELinux might be compromised via a web vulnerability, but SELinux policy only allows it to read files labeled as web content (e.g., `/var/www/html`) and blocks it from reading `/etc/shadow` or user home directories, reducing the impact of the breach.

**Related Concepts:**  
Links to other terms.
- [[MAC]]
- [Related term 2]