# Installing Linux Using a Virtual Machine

## 1. What Is a Virtual Machine?

A virtual machine (VM) is a software-created computer that runs inside a physical computer.

It has virtual CPU, memory, storage, and network devices and can run its own operating system.

## 2. Important Terms

| Term | Meaning |
|---|---|
| Host OS | The operating system on the physical computer |
| Guest OS | The operating system running inside the VM |
| Hypervisor | Software that creates and manages VMs |
| ISO file | An image used to boot and install an operating system |
| Virtual disk | A file that acts as the VM's disk |

## 3. Proposed Setup

- Host OS: Windows
- Hypervisor: Oracle VirtualBox
- Guest OS: Ubuntu Server
- Installation media: Ubuntu Server ISO
- Virtual storage: A virtual disk managed by the VM

This setup is a learning plan. A separate VM has not yet been installed.

## 4. Installation Workflow

1. Check available memory, disk space, and hardware virtualization.
2. Install a suitable hypervisor.
3. Download the Ubuntu ISO from the official Ubuntu website.
4. Create a VM and configure its virtual CPU, memory, and storage.
5. Boot the VM from the ISO.
6. Follow the Ubuntu installer to install Linux onto the virtual disk.
7. Restart the VM and verify that the guest OS boots successfully.

## 5. WSL 2 vs. a Traditional VM Installation

My current Ubuntu environment runs through WSL 2.

WSL 2 uses a lightweight virtual machine to run a Linux environment. It is suitable for learning commands, Bash, permissions, processes, and many DevOps fundamentals.

A traditional VM installation provides additional practice with bootable ISO media, virtual hardware, installation choices, and virtual disks.

## 6. Safety Considerations

- Keep the guest OS on its intended virtual disk.
- Read disk-selection and formatting screens carefully.
- Avoid changing Windows partitions during guest installation.
- Be cautious when configuring shared folders and host access.
- Check resource availability before starting a VM.

## 7. DevOps Relevance

VM knowledge helps when working with test environments, isolated operating systems, virtual servers, networking, storage, and infrastructure provisioning.

## Learning Status

**Theory:** Foundation-level VM concepts and installation workflow covered.

**Hands-on installation:** Pending. No separate VM has been installed yet.