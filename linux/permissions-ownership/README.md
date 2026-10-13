# Linux Permissions and Ownership

## Overview

Linux permissions control who can read, modify, or execute files and who can access directories.

These concepts are important in DevOps because incorrect permissions can prevent applications from running or expose sensitive files.

## 1. Understanding Permission Categories

Linux permissions are divided into three categories:

| Category | Meaning |
|---|---|
| `u` | Owner (user) |
| `g` | Group |
| `o` | Others |
| `a` | All three categories |

The three basic permissions are:

| Permission | Meaning | Numeric value |
|---|---|---:|
| `r` | Read | 4 |
| `w` | Write | 2 |
| `x` | Execute | 1 |

For example:

```text
-rwxr-xr--
```

This means:

- Owner: read, write, execute
- Group: read, execute
- Others: read only

## 2. Inspect File Permissions

```bash
ls -l
```

Displays file permissions, ownership, size, and modification time.

```bash
ls -ld secure
```

Displays information about the `secure` directory itself.

```bash
id
```

Displays the current user's UID, primary GID, and group memberships.

```bash
groups
```

Displays the groups associated with the current user.

## 3. Change Permissions with chmod

### Numeric Permissions

```bash
chmod 600 credentials.txt
```

Sets the permissions to:

- Owner: read and write
- Group: no permissions
- Others: no permissions

This is commonly appropriate for private credential files when the application requirements support it.

```bash
chmod 755 deploy.sh
```

Sets the permissions to:

- Owner: read, write, execute
- Group: read and execute
- Others: read and execute

```bash
chmod 750 deploy.sh
```

Sets the permissions to:

- Owner: read, write, execute
- Group: read and execute
- Others: no permissions

### Symbolic Permissions

```bash
chmod g+w file.txt
```

Adds write permission for the group without changing other permission bits.

The symbolic form is useful when you want to change a specific permission without replacing the entire permission set.

## 4. Directory Permissions

Directory permissions behave differently from file permissions.

- Read (`r`): allows listing directory entries.
- Write (`w`): allows creating, removing, or renaming entries, subject to other access controls.
- Execute (`x`): allows searching or traversing the directory.

A directory commonly needs execute permission for users to access files inside it.

## 5. Setgid on Directories

The setgid bit can be applied to a shared directory:

```bash
chmod g+s shared-dir
```

When set on a directory, newly created files and subdirectories generally inherit the directory's group rather than the creator's primary group.

This helps teams share project files consistently. Actual access still depends on permissions and other access controls.

## 6. Understanding umask

`umask` controls which permission bits are removed from the default permissions assigned to newly created files and directories.

```bash
umask
```

Displays the current umask.

```bash
umask 0027
```

Sets the umask for the current shell.

With typical Linux creation modes:

- Files start from `666`.
- Directories start from `777`.

A umask of `0027` normally produces:

| Entry | Resulting permissions |
|---|---|
| Regular file | `640` (`rw-r-----`) |
| Directory | `750` (`rwxr-x---`) |

The umask affects newly created entries. It does not automatically change the permissions of existing files.

## 7. Troubleshooting Permissions

### Scenario: A script cannot be executed

Inspect the file:

```bash
ls -l deploy.sh
```

Check whether the appropriate execute permission is present for the user running it.

### Scenario: A file contains sensitive information

Inspect its current permissions and confirm that access is restricted to the required users.

For a private credential file, `chmod 600 credentials.txt` gives read and write permission only to its owner.

### Scenario: A team cannot access shared files

Use `id` and `groups` to inspect group membership. Check the directory's ownership and permissions before changing anything.

## Key Takeaways

- Use `ls -l` to inspect permissions and ownership.
- Use `chmod` to change permission bits.
- Use `id` and `groups` to inspect user and group membership.
- Setgid on a directory helps with group inheritance.
- `umask` affects the default permissions of newly created entries.
- Check permissions before making changes, especially on sensitive files.

## Learning Status

**Status:** Basic permissions, group inspection, setgid, and umask practised. User/group administration and ownership changes with `chown` remain to be covered.