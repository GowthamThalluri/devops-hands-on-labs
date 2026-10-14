# Introduction to Linux

## 1. What Is Linux?

Linux is an open-source operating system kernel. It manages system resources such as CPU, memory, processes, and devices.

Operating systems such as Ubuntu use the Linux kernel along with system utilities, libraries, and applications.

## 2. Why Linux Is Important in DevOps

DevOps engineers use Linux to:

- Deploy and run applications.
- Inspect application logs.
- Manage processes and services.
- Troubleshoot disk-space and permission problems.
- Automate repetitive tasks using shell scripts.
- Work with cloud servers and container environments.

## 3. What Is a Linux Distribution?

A Linux distribution combines the Linux kernel with system utilities, software packages, and tools needed to provide a usable operating system.

Examples include Ubuntu, Debian, and Red Hat Enterprise Linux.

My practice environment uses Ubuntu through Windows Subsystem for Linux (WSL).

## 4. Identify the Linux Distribution

Command:

```bash
cat /etc/os-release
```

Purpose: Displays information about the installed Linux distribution.

Environment verified during practice:

- Distribution: Ubuntu
- Version: 26.04 LTS
- Version codename: resolute

## 5. Identify the Kernel Version

Command:

```bash
uname -r
```

Purpose: Displays the Linux kernel release version.

Output from my environment:

```text
6.18.33.2-microsoft-standard-WSL2
```

The output identifies a Microsoft-standard kernel build for WSL 2.

## 6. Identify the Configured Shell

Command:

```bash
echo "$SHELL"
```

Purpose: Displays the shell configured for the current user.

Output:

```text
/bin/bash
```

Bash is a command-line shell that interprets commands and supports variables, pipelines, and shell scripting.

## 7. Understand the Terminal, Shell, and Kernel

- **Terminal:** The interface where commands are entered and output is displayed.
- **Shell:** Interprets commands and helps run programs.
- **Kernel:** Manages processes, memory, devices, and other system resources.

These components work together when a user runs commands in Linux.

## 8. Understand Command Resolution

Command:

```bash
type -a ls
```

Purpose: Shows how Bash recognises a command, including aliases and executable paths.

In my environment, the output showed:

```text
ls is aliased to `ls --color=auto'
ls is /usr/bin/ls
ls is /bin/ls
```

The `ls` alias adds the `--color=auto` option. Bash can also locate the executable through the listed paths.

This command is useful when investigating aliases or unexpected command behaviour.

## 9. Linux in My DevOps Learning Environment

I use Ubuntu on WSL to practise Linux commands on my Windows computer.

My learning process focuses on understanding commands, inspecting their output, and applying them to realistic troubleshooting scenarios before moving to advanced topics.

## Key Takeaway

Linux fundamentals include understanding the distribution, kernel, shell, terminal, and command execution.

Knowing how to inspect the actual environment is an important first step when troubleshooting Linux systems.

## Learning Status

**Status:** Introduction to Linux — foundation-level concepts and environment inspection practised.
