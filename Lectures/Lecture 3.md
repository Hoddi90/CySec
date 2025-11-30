---
tags:
  - Category/Lecture-Notes
aliases:
  - Lecture-Note
---


Further research

1. How can you prevent wildcard injection attacks, such as the one with rm * shown in the slides?

A wildcard injection attack is a cyber attack where the hacker(s) use wildcard characters e.g. "*" and put them into command(s) to force the user to do something he did not intend to do, for example, deleting all his files in the system instead of those in his folder. If a hacker created a file naemd -rf and an admin would run rm * in the folder containing that file, the shell would expand the command to also contain -rf which would  force the system to remove all files recursively.

2. The ”Curl — Bash” Problem: Find a recent example of a supply-chain attack where a remote script was compromised. If you must install software this way, what specific steps should you take to verify the script’s integrity before running it?

A supply chain attack is a cyber attack where some hacker(s) manage to hack into your software by initally attacking someone in the supply chain that has weaker cyber defences. An example of this are the 2020 cyberattacks on the United States by Russia where they successfully penetrated U.S. Treasury Department and the U.S. department of Commerce. 

The hackers managed to attack the U.S. by targeting the sofware company SolarWinds, which sold an IT monitoring platform called "Orion" for the government. By inserting their own code into Orion's software updates, the Russians gained access all users in the U.S government who had installed the trojan horse software updates.

In general, if you must install software via curl-bash, you should do several things. 
1. You should check the source. 
2. Download it without piping it directly to bash. 
3. Actually read the script and verify the checksum if it has one.


2. Principle of Least Privilege: Why is sudo safer than logging in as root directly? Research the concept of the ”Audit Trail” in system logs. How does sudo help track who did what?
Sudo is safer for several reasons. Sudo forces you to enter your password whenever it is used, which gives the user a moment to reflect on what he does. Furthermore it only gives the user 5 minutes to make those changes (a single command) and logs every command that you do. It can log every command because you are logged in as a regular user, just with temporary privileges. Therefore, sudo can log which user used which command, what command was used, when it was used and from where.

Logging as a root user directly means that you can make any change you can in sudo, but without any restrictions. That means you have no safeguards to protect you from your own mistakes or ignorance. Furthermore, there is no way to track who executed a command, thus it is functionally impossible to maintain any real accountability. Additionally, if a root user receives malware, it can easily take over the whole system and cause great damage. 

4. Path Hijacking: Create a safe experiment on your own machine (or a VM): Create a script named ’ls’ in a local folder, modify your $PATH, and see if you can trick your shell into running it. How do modern OSs (Windows/Linux) try to prevent this by default?

5. The Un-deletable File: You have a file named ’-i’. Every time you try to delete it (rm -i), the system asks you for confirmation, but even if you say yes, it doesn’t delete. Why? How do you fix it?

-i is an option in linux that prompts the user and asks if it is really what he wants to do. In this case, (rm -i) asks the user whether we is sure if he want to delet this file. If -i was created as a file then the shell expands to include it and waits for the user to write a file that is to be deleted.
You can fix this in two ways. 

The first is to stop option parsing by inserting -- after rm which creates the command "rm -- -i" which tells linux that everything after "--" is a filename. 

The second way is to prefix the filename with a path insert "./" after rm but connected to -i (rm ./-i), forcing the file to start with a "." and not a "-" which tells the computer that the file the user wishes to be deleted is located at the path ./-i

# Lecture Title

**Date:** {{26.11.2025}}
**Created:** {{30.11.2025}}

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

