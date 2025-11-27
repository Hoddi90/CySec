---
tags:
  - Category/Lecture-Notes
aliases:
  - Lecture-Note
Keywords:
  - Process
  - Program
  - address space
  - virtual memory
---


# Lecture Title

**Date:** {{date}}
**Created:** {{time}}

---

## Key Concepts & Takeaways

# <Operating-System-Basics—Lecture-Notes>

**Category:** Operating Systems / Security / Cybersecurity  
**Operating System(s):** Linux / Windows / macOS / Android / Embedded

---

## 1. What is an Operating System?

- Kernel = Core program running in **privileged mode (Ring 0)**  
- Manages **hardware state**, CPU, memory, devices, interrupts  
- Bridge between **applications** (User Space) and **hardware**  
- User applications run in **user mode (Ring 3)** with restricted privileges  
- OS exposes hardware via **system calls (APIs)**

---

## 2. Abstraction & Arbitration

### Abstraction
- Hardware is complex → OS provides simple APIs  
- Examples: `open()`, `read()`, `write()`, `printf()`  
- System call = program asks kernel to perform hardware action  
- Kernel switches modes, performs task, returns result

### Arbitration (Resource Management)
- Multiple processes compete for limited resources  
- OS performs:
  - **Time multiplexing** (CPU scheduling)
  - **Space multiplexing** (RAM/disk allocation)
  - **Isolation** (process protection)

---

## 3. Key OS Functionalities

### Process Management
- **Program** = code on disk  
- **Process** = code in execution (PC, registers, stack, memory state)  
- **Context switching** saves/restores process state (PCB)  
- Creates illusion of parallelism

### Memory Management (Virtualization)
- Virtual memory → each process sees own address space  
- MMU translates virtual → physical addresses  
- Protection prevents cross-process memory access  
- Segfault = invalid address access

### I/O & Interrupts
- I/O is extremely slow vs CPU  
- OS uses sleep/wake + interrupts instead of busy waiting  
- **ISR** (Interrupt Service Routine) handles hardware events  

### File Systems
- Physical storage = blocks/sectors  
- OS provides files/directories/permissions  
- Responsible for metadata & consistency (journaling)

### Protection (Privilege Modes)
- **Ring 0 (kernel)**: full hardware access  
- **Ring 3 (user)**: restricted  
- Privilege violations cause **traps** handled by kernel

---

## 4. Common Operating Systems

### Unix / Linux
- "Everything is a file"  
- Modular tools + pipes  
- Linux = monolithic kernel  
- macOS = hybrid XNU (Mach + BSD)

### Windows (NT Architecture)
- Hybrid kernel  
- Uses **Registry** for configuration  
- Resources represented as **Objects** accessed via **Handles**

### Android
- Uses Linux kernel, but unique user-space  
- ART runtime (bytecode), HAL layer, Binder IPC  
- Strong sandboxing

### RTOS (Real-Time Systems)
- Goal: **determinism**, not throughput  
- Used in safety-critical devices  
- Tiny kernels, fast interrupt handling

---

## 5. POSIX Standard

- Defines **API contract** for Unix compatibility  
- Standardizes system calls, shell behavior, CLI utilities  
- Ensures source code portability across Unix-like OS  
- macOS = fully POSIX compliant  
- Linux = mostly compliant  
- Windows = non-POSIX (uses Win32 API)

---

## 6. Operating Systems & Security

### Trusted Computing Base (TCB)
- Hardware + firmware + software enforcing security policy  
- If any TCB component fails → whole system is compromised

### Reference Monitor
- OS checks:
  1. Authentication (AuthN)
  2. Authorization (Access control)

---

## 7. Authentication & Access Control

### Authentication (Who are you?)
- Identification (username)
- Verification (password, biometrics, key)

### Secure Password Storage
- Hashing only (no plain passwords)
- Salt prevents rainbow table attacks

### Access Control
- **DAC** (Owner controlled) → flexible, but less secure  
- **MAC** (System controlled) → used in SELinux, iOS, Android  
- Enforces mandatory policies

### Principle of Least Privilege
- Processes get minimum permissions needed  
- Limits damage if compromised

---

## 8. Logs, Auditing & Integrity

### Logs
- High-level tracking of system events  
- Linux: `/var/log/syslog`, `/var/log/auth.log`  
- Windows: Event Viewer

### System Auditing
- Tracks system calls  
- Required for compliance (PCI-DSS, HIPAA)

### File Integrity Monitoring (FIM)
- Detects unauthorized changes to critical files  
- Compares file hashes

---

## 9. Common Vulnerabilities

### Buffer Overflows
- Writing beyond buffer limits → overwrite return address  
- Mitigation: ASLR, DEP/NX

### Race Conditions (TOCTOU)
- Check and use time gap exploited due to context switches  
- Example: swapping a file with a symlink

### Command Injection
- Unsanitized input passed to shell  
- Example: `rm $filename` with malicious input

### Privilege Escalation
- Exploiting SetUID binaries  
- Exploiting kernel bugs  
- Driver vulnerabilities

### Rootkits
- Hide processes, files, system calls  
- OS output becomes untrustworthy

### Zero-days
- Unknown vulnerabilities exploited before patching  
- Defense: Defense in Depth

---

## 10. Sysadmin Commands Summary

### Privileges
- Linux: `sudo`
- Windows: RunAs / Start-Process -Verb RunAs

### File Permissions
- Linux: `chmod`, `chown`, `ls -l`
- Windows: `icacls`, `takeown`

### Process Management
- Linux: `ps aux`, `top`, `systemctl`, `kill`
- Windows: `Get-Process`, `Stop-Process`, `Get-Service`

### Disk / FS Management
- Linux: `df -h`, `du -sh`, `find`, `tar`
- Windows: `Get-Volume`, `Compress-Archive`

### Logs
- Linux: `tail -f`, `grep`
- Windows: `Get-Content -Wait`, `Select-String`

### Scheduling
- Linux: `crontab -e`
- Windows: `Register-ScheduledTask`

---

## 11. Further Study Topics

- Real-world rootkit case studies  
- Meltdown & Spectre (CPU speculative execution flaws)  
- DMA attacks (bypassing OS using direct hardware access)  
- Mitigations for SUID programs  



---

## Connections to Earlier Material

- [New topic] → relates to [old topic] because…
- [ ]

---
## Questions for Discussion / Research

1. **Rootkits in Real Attacks**  
   - Find documented cyberattacks where rootkits played a central role.  
   - Describe how the rootkit altered system behavior (e.g., hiding files/processes, tampering with logs).  
   - Explain how the attackers installed the rootkit despite OS protections.

2. **Side-Channel Attacks (Meltdown & Spectre)**  
   - Investigate how speculative execution works at the CPU level.  
   - Explain how attackers exploited it to read kernel memory from user mode without triggering permission checks.  
   - Summarize which processors and systems were affected.

3. **DMA (Direct Memory Access) Attacks**  
   - Explore how DMA devices access RAM without CPU involvement.  
   - Identify how malicious devices (e.g., corrupted USB-C dock, Thunderbolt device) can access system memory.  
   - Review mitigations such as IOMMU, kernel isolation, and BIOS security settings.

4. **SUID Security Risks & Mitigations**  
   - How does the SUID mechanism enable privilege escalation in Linux?  
   - What classes of vulnerabilities (buffer overflow, race conditions) are commonly used against SUID binaries?  
   - What OS-level mitigations exist (e.g., removing SUID flags, using capabilities, AppArmor/SELinux, rewriting tools to avoid elevated permissions)?

5. **Trusted Computing Base (TCB) Hardening**  
   - Which components belong to a system’s TCB?  
   - What design principles reduce TCB size?  
   - Why does a smaller TCB improve overall system security?

6. **Log Integrity & Forensics Readiness**  
   - Evaluate methods for protecting logs from tampering (append-only storage, remote syslog).  
   - Explain how logs play a role in detecting privilege escalation or rootkit activity.  
   - Compare log retention and auditing policies across OSs (Linux, Windows, macOS).

7. **OS Scheduling Strategies**  
   - Examine the trade-offs between fairness and throughput in CPU schedulers.  
   - Compare Linux CFS, Windows scheduler, and RTOS priority-based scheduling.  
   - Identify scenarios where each approach is optimal.

8. **Isolation in Modern Systems**  
   - Compare process isolation, container isolation, VM isolation.  
   - Explain which threats each isolation level mitigates.  
   - Research weaknesses (container escapes, VM hypervisor vulnerabilities).

9. **Authentication & Password Storage**  
   - Investigate modern password hashing algorithms (PBKDF2, bcrypt, scrypt, Argon2).  
   - Explain how salting and key stretching improve security.  
   - Discuss future directions, including passwordless authentication (FIDO2/WebAuthn).

10. **Operating System Design Philosophy**  
    - Compare monolithic, microkernel, and hybrid kernel architectures.  
    - Discuss performance vs security implications.  
    - Analyze why Linux stayed monolithic but macOS and Windows adopted hybrid designs.



---

## Diagrams / Examples / Code

### Diagram / Example
# Diagrams / Examples / Code Snippets

---

## 1. Kernel vs User Space Diagram

```
+--------------------------------------------------------+
|                     User Space                         |
|  ----------------------------------------------------  |
|  Applications:  bash, chrome, python, games, etc.      |
|  ----------------------------------------------------  |
|           (restricted: cannot touch hardware)          |
+--------------------------------------------------------+
                 | System Calls (API) |
+--------------------------------------------------------+
|                     Kernel Space                       |
|  ----------------------------------------------------  |
|   Kernel: process mgmt, memory mgmt, drivers, FS       |
|   Schedulers, Interrupt Handlers, Security             |
|  ----------------------------------------------------  |
|            (privileged: full HW access)                |
+--------------------------------------------------------+
```

---

## 2. System Call Flow (Example: write())

```
User Program (printf)
        |
        | calls write()
        v
+---------------------------+
| libc wrapper for write()  |
+---------------------------+
        |
        | triggers software interrupt
        v
+---------------------------+
|      Kernel Handler       |
|  validates permissions    |
|  writes to file/socket    |
+---------------------------+
        |
        v
Returns result to user space
```

---

## 3. Context Switch Diagram

```
CPU executing Process A
        |
        | timer interrupt
        v
Save registers of A → PCB(A)
Load registers of B ← PCB(B)
        |
CPU executes Process B
```

**PCB (Process Control Block) contains:**
- Program Counter  
- Stack Pointer  
- CPU Registers  
- Open files  
- Process state  

---

## 4. Virtual Memory Mapping Example

```
Process sees (virtual):
0x0000  ----------------
        | Code         |
0x3000  ----------------
        | Heap         |
0x8000  ----------------
        | Stack        |
0xFFFF  ----------------

MMU + Kernel translate to:

Physical RAM:
0xA000  -> Code
0xF000  -> Heap
0x12000 -> Stack
```

**Crash example:**
```
Segfault when accessing 0xFFFFF000
(no mapping in page table)
```

---

## 5. File Permissions (Linux)

### Symbolic
```
-rwxr-x---
| |  |  |
| |  |  +---- Others (---)
| |  +------- Group (r-x)
| +---------- Owner (rwx)
+------------- regular file
```

### Octal
```
Owner (7) = rwx
Group (5) = r-x
Other (0) = ---
Final: 750
```

### Command
```
chmod 750 script.sh
chown root:admin file.txt
```

---

## 6. SUID Example (Dangerous)

### Find SUID binaries
```
find / -perm -4000 2>/dev/null
```

### Example output
```
-rwsr-xr-x 1 root root /usr/bin/passwd
```

This binary **runs with root privileges** even when called by normal users.

---

## 7. Buffer Overflow Example in C

```c
#include <stdio.h>
#include <string.h>

int main() {
    char buf[8];
    gets(buf);   // UNCHECKED input
    printf("You typed: %s\n", buf);
}
```

**Exploit concept:**
- attacker enters >8 bytes  
- overwrites saved return address  
- program jumps to attacker’s shellcode  

---

## 8. Race Condition (TOCTOU) Example

```
Process A:
if (access("/tmp/x", W_OK) == 0)
    write("/tmp/x");

Attacker:
Replace "/tmp/x" → symlink to "/etc/shadow"

Context switch occurs between check and use.
```

---

## 9. Command Injection Example (Shell)

```bash
# Vulnerable
filename="$USER_INPUT"
rm $filename
```

Attacker input:
```
file.txt; rm -rf /
```

OS executes both commands.

---

## 10. Linux I/O Blocking vs Interrupts

```
User Process ----> read() syscall ----> sleep()
                                   (waiting for disk)

Disk finishes → hardware interrupt → kernel ISR → wake process
```

---

## 11. Linux Commands (Examples)

### Directory & File Management
```
ls -la
cd /path/to/dir
mkdir newfolder
touch file.txt
rm -r folder
cp src.txt dest.txt
mv old new
```

### Permissions
```
chmod 644 file
chmod u+x script.sh
chown user:group file
```

### Searching & Filtering
```
find /var/log -name "*.log"
grep -R "error" /var/log
grep -i "failed" auth.log | wc -l
ls -la | grep txt
```

### Piping Examples
```
ps aux | grep python
dmesg | tail -20
cat file | sort | uniq -c | sort -nr
tar -czf backup.tar.gz folder/ | pv
```

---

## 12. Process Management

```
ps aux
top
htop
kill -9 <PID>
systemctl status ssh
systemctl restart apache2
```

---

## 13. Auditd Example (Linux Auditing)

### Watch for writes to /etc/shadow
```
sudo auditctl -w /etc/shadow -p wa -k shadow_change
```

### Query audit log
```
sudo ausearch -k shadow_change
sudo aureport -f
```

---

## 14. Diagram: OS Security Model

```
+-----------------------+
|   Users & Processes   |
+-----------------------+
           |
           v
+-----------------------+
|  Authentication (UID) |
+-----------------------+
           |
           v
+---------------------------------+
| Authorization (DAC / MAC / ACL) |
+---------------------------------+
           |
           v
+-----------------------+
|   Kernel Enforces     |
|   via TCB + Syscalls  |
+-----------------------+
```

---

## 15. Windows vs Linux Permissions

### Linux (Simple, POSIX)
```
User / Group / Other
rwx / rw- / r--
chmod 754 file
```

### Windows (ACL-based)
```
icacls file
Get-Acl file.txt
Set-Acl file.txt
```

