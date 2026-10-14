# Linux Distributions

## 1. What Is a Linux Distribution?

A Linux distribution combines the Linux kernel with system utilities, software packages, and tools to provide a usable operating system.

Examples include Ubuntu, Debian, Red Hat Enterprise Linux, and Alpine Linux.

## 2. Common Linux Distributions

| Distribution | Common use |
|---|---|
| Ubuntu | Development, learning, and cloud servers |
| Debian | Community-developed systems and servers |
| Red Hat Enterprise Linux (RHEL) | Enterprise environments |
| Amazon Linux | AWS cloud environments |
| Alpine Linux | Lightweight container images and other environments |

## 3. Package Managers

Package managers help install, update, remove, and inspect software.

| Distribution | Common package tool |
|---|---|
| Ubuntu / Debian | `apt` |
| RHEL family | `dnf` |
| Alpine Linux | `apk` |

The exact package tools and versions depend on the distribution and release.

## 4. Inspect the Installed Distribution

```bash
cat /etc/os-release
```

Displays information about the current Linux distribution.

My environment reported Ubuntu 26.04 LTS.

## 5. Check the apt Package Manager

```bash
command -v apt
```

Displays the path of the `apt` executable when available.

```bash
apt --version
```

Displays the installed `apt` version.

My environment reported:

```text
/usr/bin/apt
apt 3.2.0 (amd64)
```

## 6. Check dpkg

```bash
command -v dpkg
```

Displays the path of the `dpkg` executable when available.

My environment reported:

```text
/usr/bin/dpkg
```

`apt` provides higher-level package management, including dependency resolution and repository access. `dpkg` handles lower-level Debian package operations.

## Key Takeaway

Linux distributions may use different package managers and configurations. DevOps engineers should identify the target distribution before following installation or system-management instructions.

## Learning Status

**Status:** Foundation-level Linux distribution concepts and package-manager identification practised.
