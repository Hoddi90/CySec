---
tags:
  - Category/Lecture-Notes
aliases:
  - Lecture-Note
---

·       In terms of **virtualization** **Host Machine/OS** is defined as “_the physical computer on which virtualization software runs_”. **A guest machine/OS** (Virtual machine) _is “a software-based, isolated computer system that runs on the host”_ and a **hypervisor** (virtual machine monitor) is “_the software layer that creates, runs, and manages virtual machines_”.

·       There are two types of hypervisors. A **type 1 hypervisor** (Bare-metal) which runs directly on the host hardware, without an underlying operating system. It has high performance, greater security and is enterprise-grade (Vmware ESXi).

·       A **type 2 hypervisor** (hosted hypervisor) runs as an application on top of a conventional host operating system. It is easer to set up and good for desktop development and testing (Oracle VirtualBox).

We have 5 different virtualization methods.

1.       **Full virtualization** where the hypervisor fully simulates hardware and the guest OS runs unmodified. It has high compatibility with most operating systems, high isolation between VMs and the hsot, flexible (e.g., Windows on a linux host) and near native performance with hardware assistance. However it has higher overhead without hardware assistance due to full simulation, is resource-intensive and requires CPU support for hardware-assisted features for optimal spped.

2.       **Paravirtualization** where the guest OS is modified/aware it is virtualized and communicates directly with the hypervisor. Thus the guest OS and hypervisor work together to get better performance and lower overhead, achieving more efficient use of resources. However due to modification or special drivers for the guest OS kernel, it has less compatibility and can be more complex to set up.

3.       **Hardware-Assisted virtualization** which leverages special CPU instructions e.g. Intel VT-x and AMD-V, to accelerate virtualization.

4.       **OS-level virtualization (Containerization)** which shares the host OS kernel but isolates applications in “containers”. Thus, each container has its own isolated user space, procescesses, file system, and network interfaces. It focuses on isolating applications and their dependencies, not the entire operating system. It is extremely lightweight and fast startaup with extremely efficient resource utilization (no separate OS kernel per container), highly portable, and thusly ideal for microservices and continuous integration/delivery (CI/CD). However, a shared kernel is a single point of failure and all containers must run on the same host OS kernel (linux containers on Linux only).

5.       **Emulation** which simulates an entire hardware platform, often for different CPU architechtures. The guest code is translated on the fly to run on the host’s native architechture. Frequently used to play retro games. The guest software needs no modifications. However, it has extremely high performance overhead, is highly resource-intensive. It is primarily used when virtualization is not an option due to fundamental architechtural differences. Rarely used for general-purpose server consolidation or cloud infrastructure due to low performance.

Virtualization introduces new security challenges

1.       **VM/Container Escape** where breaking out of the guest OS comprimises the host/hypervisor.

2.       **Hypervisor vulnerabilites** wher falws in the core virtualization can affect all guests, a single point of failure.

3.       **Resource exhaustion (DoS)** where ong guest excessivley consumes the host’s resources, starving others

4.       **Management Plane security** where compromise of virtualization management tools gives full control.

5.       **Insecure Images/Templates** where a guest OS is deployed with known vulnerabilities or misconfigurations

A **type 1 hypervisor** (bare metal) is the most secure virtualization due to it’s strong isolation and small attack surface since it is an indepentent OS. However, if the hypervisor has a bug, it will impact all VMs, thus making management tools a high value target for attackers.

A **type 2 hypervisor** hosted hypervisor()has good isolation between VMs and leverages host OS security tools (AV, firewall) but has a larger attack surface. It’s interlink with the host OS makes it reliant on the host’s security being up to date and it has weaker isolation overall than type 1.

**OS-level virtualization - Containers** have a small attack service per container due to not having full OS and they have rapid patching/deployment of immutable images. However, they have a single point of failure (kernel) which can affect all containers. Furthermore, they are highly reliant on secure images making them a tempting target for attackers.

**Emaluation** has strong isolation from host due to full translation but is not designed for secure, multi-tenant production. It also has high performance overhead and if the emulator has a vulnerability, it can be exploited by an attacker.

**In terms of security,** physical hardware is the best followed by type 1 virtualization, type 2 virtualization, OS-level Virtualization (Containers) and Emulation.

The best way to manage these risks is to keep patches up to date, apply principles of least privilege, disable anything that is unused (features/ports) and enforce strong access control), isolate management guest and host networks, scan images/templates for vulnerabilities and use trusted sources, monitor logs, apply security best practices within each VM/container and follow vendor guidelines about hypervisors as well as removing unnecessary software.

Further studies

**Under what specific scenarios would you have to choose VMs over containers for security reasons, and vice-versa?** 
You would choose VM’s over containers for security reasons when isolation is important and you are designing for multi-tenancy, e.g., if you are a cloud provider you want many users to share the same physical server, but not to interact with each other. VMs isolate at the hardware/OS level which makes it hard for attackers to get into other user’s system. You would choose a container for security reasons when you want a smaller per-container attack surface and rapid patching.

**Research historical examples of VM escape vulnerabilities (e.g., specific CVEs for VMware, VirtualBox, KVM, or Docker). What were the root causes?**

The following CVE’s were researched: CVE-2015-3456 (more to be added later)

In CVE-2015-3456 (VENOM)  Qemu, Xen, KVM and Virtualbox were vulnerable due to a flaw in QEMU’s virtual floppy disk controller which allowed local guest users to cause a denial of service or execute arbitrary code via the (1) FD_CMD_READ_ID, (2) FD_CMD_DRIVE_SPECIFICATION_COMMAND, or other unspecified commands.

The root causes of VENOM cause was a [[Buffer Overflows]] vulnerability in the virtual floppy disk controller in QEMU, which could allow an attacker (guest VM) to escape to the host.

Side-channel attacks:

**What is a side-channel attack (in the context of virtualization)?** 
A [[Side-Channel attack]] is a technique where an attacker infers secrets (like cryptographic keys) by measuring _indirect_ information from a system, such as timing, power use, electromagnetic emissions, or cache behavior, instead of breaking the algorithm itself.
In the context of virtualization an attacker obtains information about a virtual machine (VM) e.g., by observing cache timing or memory behavior. It means that an attacker who has their own virtual machine located on the same physical server as the victim can observe the hardware side effects of the victim’s activity and use this information to plan an attack.

**Why is this especially problematic for cloud environments?** 
This is especially problematic for cloud environments due to multi-tenancy. Cloud providers generally put many customers’ virtual machine’s on the same server to save resources. That means that he hacker can try to get a VM that is on the same server as the victim’s and once they do, the attacker and victim share various resources, e.g. a CPU cache. The attacker could thusly relatively easily obtain unintentional information about the victim and plan accordingly to attack the shared server.

Find recent examples of such attacks and discuss their impact.

What mitigation strategies exist to counter these types of attacks?

**What are the risks associated with using untrusted or vulnerable container images from public repositories?** 
The risk with using untrusted or vulnerable container images from public repositories is that it could include code that is malware, fully intended to harm our computer or the container image could be outdated, unintentional leading to security vulnerabilities
# Lecture Title

**Date:** {{25.11.2025}}
**Created:** {{30.11.2025}}

---

## Key Concepts & Takeaways

- [[Side-Channel attack]]
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

