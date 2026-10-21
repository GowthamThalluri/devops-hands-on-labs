# Linux User Management

## 1. Overview

Linux user management involves creating, inspecting, and modifying user accounts. Each account has a user ID (UID), a primary group ID (GID), a home directory, and a configured login shell.

In DevOps, user management helps administrators control who can access a server, application files, and shared resources.

## 2. Inspect a User Account

### Command

```bash
getent passwd gowtham
```

### Purpose

Retrieves the account record for `gowtham` from the configured account databases.

### Output from my environment

```text
gowtham:x:1000:1000::/home/gowtham:/bin/bash
```

### Field explanation

| Field | Value | Meaning |
|---|---|---|
| Username | `gowtham` | Account name |
| Password marker | `x` | Password information is normally stored in `/etc/shadow` |
| UID | `1000` | Numeric user ID |
| Primary GID | `1000` | Numeric ID of the primary group |
| Description | Empty | No description is set in this record |
| Home directory | `/home/gowtham` | User's home directory |
| Login shell | `/bin/bash` | Configured login shell |

## 3. Inspect a Group by GID

### Command

```bash
getent group 1000
```

### Output

```text
gowtham:x:1000:
```

This identifies the group named `gowtham` with GID `1000`.

The empty member list does not mean the user is outside the group. A group's member list commonly lists supplementary memberships; the user's primary GID is recorded separately in the user account record.

## 4. Inspect User Group Memberships

### Command

```bash
groups gowtham
```

### Output from my environment

```text
gowtham : gowtham adm cdrom sudo dip plugdev users appgrp
```

This command displays the groups associated with the specified account.

Group membership may grant access to shared files, devices, logs, or other resources, depending on the permissions and system configuration.

## 5. Create a Practice User

### Scenario

An application needs a separate Linux user account rather than running under a personal account.

### Command used

```bash
sudo useradd -m -s /bin/bash -G appgrp devops-trainee
```

### Explanation

- `sudo`: Runs the command with elevated privileges.
- `useradd`: Creates a user account.
- `-m`: Creates the user's home directory.
- `-s /bin/bash`: Sets Bash as the login shell.
- `-G appgrp`: Adds `appgrp` as a supplementary group.
- `devops-trainee`: The new username.

The command creates an account in the Linux environment. It does not automatically grant administrator privileges or set a usable password.

## 6. Verify the New Account

### Commands

```bash
id devops-trainee
getent passwd devops-trainee
```

### Verified output

```text
uid=1002(devops-trainee) gid=1003(devops-trainee) groups=1003(devops-trainee),1001(appgrp)
```

```text
devops-trainee:x:1002:1003::/home/devops-trainee:/bin/bash
```

### Key observations

- UID: `1002`
- Primary GID: `1003`
- Supplementary group: `appgrp`, GID `1001`
- Home directory: `/home/devops-trainee`
- Login shell: `/bin/bash`

Linux uses numeric IDs to identify users and groups internally.

## 7. Add a Supplementary Group Safely

### Scenario

The practice user needs membership in the `users` group but must retain existing memberships.

### Command

```bash
sudo usermod -aG users devops-trainee
```

Verify:

```bash
id devops-trainee
```

### Verified output

```text
uid=1002(devops-trainee) gid=1003(devops-trainee) groups=1003(devops-trainee),100(users),1001(appgrp)
```

The `-aG` options append the supplementary group rather than replacing the existing supplementary group list.

**Important:** Using `usermod -G` without `-a` can replace the existing supplementary group memberships. Check the impact before changing a real account.

## 8. Inspect Password Status

### Command

```bash
sudo passwd -S devops-trainee
```

### Output

```text
devops-trainee L 2026-10-21 0 99999 7 -1
```

The `L` status indicates that the password is locked.

The remaining fields report password-change and password-aging information. In this environment, the account was created without setting a password, so its password status was locked.

A locked password does not necessarily disable every possible authentication method.

## 9. DevOps Relevance

User management is useful when:

- Creating a dedicated account for an application.
- Investigating permission-denied errors.
- Checking user and group identities.
- Adding users to shared resource groups.
- Verifying account and password status.
- Avoiding unnecessary administrator privileges.

## 10. Key Takeaways

- A UID identifies a user numerically.
- A GID identifies a group numerically.
- The primary group is recorded in the user account entry.
- Supplementary groups provide additional group memberships.
- `getent`, `groups`, and `id` help inspect users and memberships.
- `useradd` creates accounts, while `usermod` modifies them.
- Always verify account changes after running administrative commands.

## Learning Status

**Status:** Foundation-level user inspection, account creation, supplementary group modification, and password-status inspection practised in Ubuntu WSL.

**Practice account:** `devops-trainee` remains in the WSL environment. Its password status was verified as locked.
