# Linux Group Management

## 1. Overview

Linux groups allow administrators to organize users and manage shared access to files, directories, and application resources.

Instead of configuring access for each user separately, an administrator can assign users to a group and configure appropriate group permissions on the relevant resources.

Group membership alone does not grant access to every resource. Actual access also depends on permissions, ownership, ACLs, and other security controls.

## 2. Inspect an Existing Group

### Command

```bash
getent group release-team
```

Before the group was created, this command returned no output. No matching group record was found.

## 3. Create a Group

### Scenario

A company needs a group for users who manage application releases.

### Command

```bash
sudo groupadd release-team
```

### Output verified

```text
release-team:x:1004:
```

The group record contains:

| Field | Value | Meaning |
|---|---|---|
| Group name | `release-team` | Name of the group |
| Password marker | `x` | Group password field placeholder |
| GID | `1004` | Numeric group ID |
| Member list | Empty | No supplementary members are listed |

The GID may differ on another system.

## 4. Add a User to the Group

### Command

```bash
sudo usermod -aG release-team devops-trainee
```

This adds `release-team` to the user's supplementary groups.

The `-a` option appends the new membership, and `-G` specifies the supplementary group list.

### Verify the User

```bash
id devops-trainee
```

### Output after adding the group

```text
uid=1002(devops-trainee) gid=1003(devops-trainee) groups=1003(devops-trainee),100(users),1001(appgrp),1004(release-team)
```

The account now belongs to:

- Primary group: `devops-trainee`
- Supplementary group: `users`
- Supplementary group: `appgrp`
- Supplementary group: `release-team`

### Verify the Group Record

```bash
getent group release-team
```

Output:

```text
release-team:x:1004:devops-trainee
```

This confirms that `devops-trainee` appears in the group's supplementary member list.

## 5. Remove a User from a Group

### Scenario

The engineer no longer needs membership in `release-team`. Remove that membership without deleting the user account or the group.

### Command

```bash
sudo gpasswd -d devops-trainee release-team
```

### Output

```text
Removing user devops-trainee from group release-team
```

### Verify the Account

```bash
id devops-trainee
```

Final output:

```text
uid=1002(devops-trainee) gid=1003(devops-trainee) groups=1003(devops-trainee),100(users),1001(appgrp)
```

The `release-team` membership has been removed. The existing `users` and `appgrp` memberships remain.

### Verify the Group

```bash
getent group release-team
```

Final output:

```text
release-team:x:1004:
```

The group still exists, but its supplementary member list is empty.

## 6. Important Command Differences

| Command | Purpose |
|---|---|
| `getent group GROUP` | Retrieve a group's record |
| `groupadd GROUP` | Create a group |
| `usermod -aG GROUP USER` | Append a supplementary group membership |
| `id USER` | Inspect user and group IDs and memberships |
| `gpasswd -d USER GROUP` | Remove a user from a supplementary group |

## 7. Common Mistake: Replacing Group Memberships

Compare:

```bash
sudo usermod -aG users devops-trainee
```

with:

```bash
sudo usermod -G users devops-trainee
```

The first appends `users` to the existing supplementary memberships. The second replaces the supplementary group list with `users`.

Using the second command carelessly can remove access the account previously received through other supplementary groups.

Always inspect the current memberships before making changes, and verify them afterward with `id USER`.

## 8. DevOps Relevance

Group management is useful when:

- Several engineers need shared access to application resources.
- A new team member joins a project.
- A departing team member needs access removed.
- Troubleshooting group-based permission failures.
- Applying the principle of least privilege.
- Managing application-specific users and shared directories.

Remember: adding someone to a group does not automatically guarantee access. The file or directory must also have suitable permissions or ACL rules.

## 9. Key Takeaways

- Linux groups organize users for shared access.
- Each group has a numeric GID.
- `groupadd` creates a group.
- `usermod -aG` adds supplementary membership without replacing existing memberships.
- `gpasswd -d` removes supplementary membership.
- `id` and `getent group` help verify changes.
- Removing a user from a group does not delete the group.
- Always validate membership changes instead of assuming success.

## Learning Status

**Status:** Group creation, supplementary membership, membership removal, and verification practised in Ubuntu WSL.

**Practice state:** The `release-team` group exists with no supplementary members listed. The `devops-trainee` account remains in the WSL environment and still belongs to `appgrp` and `users`.
