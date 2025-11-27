---
tags:
  - Category/Terminology
aliases:
  - Terminoligy
---


**Definition:**  
Salting is the practice of adding a random value (a _salt_) to a password _before_ [[hashing]] it, so that identical passwords produce different hashes and precomputed attacks (like [[rainbow tables]]) become ineffective.

**Context / Example:**  
- **How/where it’s used:**  
	Used in secure password storage. Each user gets a unique random salt stored alongside their hash. This prevents attackers from using one hash lookup to crack many users with the same password.
- **Concrete example:**  
	A user chooses the password `P@ssw0rd`. The system generates a random salt `r9X2…` and hashes `r9X2…P@ssw0rd` with bcrypt. Another user with the _same_ password gets a different salt, so their stored hash is completely different. A stolen database with salts + hashes is much harder to crack than unsalted hashes.

**Related Concepts:**  
Links to other terms.
- [[Hashing]]
- [[Rainbow Tables]]