---
tags:
  - Category/Terminology
aliases:
  - Terminoligy
---


**Definition:**  
A flight recorder is a continuously running logging mechanism (a “black box”) that records recent system events so that, after a failure or security incident, you can reconstruct what happened just before it.

**Context / Example:**  
- **How/where it’s used:**  
	Used in operating systems and security monitoring to keep a rolling history of important events (syscalls, network connections, privilege changes, crashes) without storing infinite logs. When something goes wrong, investigators dump or inspect the recorder’s buffer.
- **Concrete example:**  
	A server keeps the last 10 minutes of kernel and process activity in a circular buffer. When the system crashes or detects an intrusion, the buffer is saved to disk. Later, the admin can review which process opened `/etc/shadow`, what network connections were made, and which syscalls ran right before the crash.

**Related Concepts:**  
Links to other terms.
- [Related term 1]
- [Related term 2]