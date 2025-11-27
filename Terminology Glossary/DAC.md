---
tags:
  - Category/Terminology
aliases:
  - Terminoligy
---


**Definition:**  
Discretionary Access Control (DAC) is an access control model where the _owner_ of a resource (file, directory, object) can decide who is allowed to access it and with what permissions.

**Context / Example:**  
- **How/where it’s used:**  
	Common in [[Unix]]-like systems and Windows, where each file has an owner who can grant or revoke read/write/execute permissions for users and groups. Access decisions are “discretionary” because they’re up to the resource owner.
- **Concrete example:**  
	On Linux, a user creates a file and uses `chmod 640 secret.txt` and `chgrp staff secret.txt` to allow the `staff` group to read it but only the owner to read/write. That user effectively controls (at their discretion) who can access the file.

**Related Concepts:**  
Links to other terms.
- [[MAC]]
- [Related term 2]