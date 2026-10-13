# Linux Filesystem Basics and Navigation

## Overview

Linux organizes files and directories in a hierarchical structure that starts from the root directory `/`.

Understanding this structure helps DevOps engineers navigate servers, locate configuration files, inspect logs, and troubleshoot application issues.

Practice environment: Ubuntu on Windows Subsystem for Linux (WSL).

## 1. Linux Directory Structure

| Directory | Purpose |
|---|---|
| `/` | Root of the Linux filesystem |
| `/home` | Contains regular users' home directories |
| `/root` | Home directory of the root user |
| `/etc` | Contains system and application configuration files |
| `/var` | Stores variable data, such as logs |
| `/tmp` | Used for temporary files |
| `/usr` | Contains many system programs, libraries, and shared resources |
| `/opt` | Commonly used for optional or additional software |
| `/proc` | Virtual filesystem that exposes process and kernel information |

## 2. Basic Navigation Commands

### Check the Current Directory

```bash
pwd
```

Displays the absolute path of the current working directory.

Example output:

```text
/home/gowtham
```

### List Files and Directories

```bash
ls
```

Lists visible files and directories in the current location.

```bash
ls -l
```

Displays a detailed listing, including permissions, ownership, size, and modification time.

```bash
ls -la
```

Displays detailed information, including hidden entries.

```bash
ls -ld /home/gowtham
```

Displays information about the specified directory itself rather than listing its contents.

### Change Directory

```bash
cd /home/gowtham/linux-practice
```

Changes to a directory using an absolute path.

```bash
cd ..
```

Moves to the parent directory.

```bash
cd ~
```

Moves to the current user's home directory.

```bash
cd -
```

Returns to the previous working directory.

## 3. Absolute and Relative Paths

### Absolute Path

An absolute path starts from the root directory `/`.

Example:

```bash
cd /home/gowtham/linux-practice
```

This identifies the destination independently of the current working directory.

### Relative Path

A relative path is interpreted from the current working directory.

Examples:

```bash
cd linux-practice
```

Enters `linux-practice` if it exists inside the current directory.

```bash
cd ..
```

Moves one directory level upward.

## 4. Important Path Symbols

| Symbol | Meaning |
|---|---|
| `/` | Root directory |
| `~` | Current user's home directory |
| `.` | Current directory |
| `..` | Parent directory |
| `-` with `cd` | Previous working directory |

Example:

```bash
cd ../linux-practice
```

Moves to `linux-practice` inside the parent directory, if that path exists.

## 5. Practical Troubleshooting

### Scenario 1: You Don't Know Your Current Location

Run:

```bash
pwd
```

Use the output to understand where relative paths will start.

### Scenario 2: A File Is Not Visible in a Normal Listing

Run:

```bash
ls -la
```

This includes hidden entries whose names begin with a dot.

### Scenario 3: You Need to Inspect a Directory's Permissions

Run:

```bash
ls -ld /home/gowtham/linux-practice
```

Review its permissions and ownership.

### Scenario 4: A Relative Path Does Not Work

Run:

```bash
pwd
ls -la
```

Confirm your current location and check whether the expected file or directory exists there.

## 6. DevOps Applications

Linux navigation and filesystem knowledge help with:

- Finding application configuration files.
- Inspecting logs during troubleshooting.
- Navigating deployment directories.
- Identifying files and directories before performing operations.
- Understanding where system information and temporary data are stored.

## Key Takeaway

Before running a filesystem command, understand your current directory and the path you intend to use.

Commands such as `pwd`, `ls`, and `cd` provide the basic navigation skills needed for everyday Linux administration and DevOps work.

## Learning Status

**Status:** Foundation-level practice completed. Advanced filesystem administration is outside the scope of these notes and will be covered separately as needed.