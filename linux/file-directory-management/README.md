# Linux File and Directory Management

## Overview

Linux provides commands to create, copy, move, rename, and remove files and directories.

These operations are common in everyday DevOps work, such as preparing deployment folders, organizing application files, and creating backups.

Practice environment: Ubuntu on WSL.

## 1. Create Files

```bash
touch app.txt
```

Creates an empty file if it does not exist.

If the file already exists, `touch` updates its modification timestamp without changing its contents.

## 2. Create Directories

```bash
mkdir archive
```

Creates a directory named `archive`.

```bash
mkdir -p recursive-demo/logs
```

Creates the required directory hierarchy, including missing parent directories.

The `-p` option also avoids an error if the specified directories already exist.

## 3. Copy Files

```bash
cp app.txt app-copy.txt
```

Copies `app.txt` to `app-copy.txt`, leaving the original unchanged.

### Copy with Confirmation

```bash
cp -i app.txt notes.txt
```

Asks for confirmation before overwriting an existing destination file.

- `y` confirms the overwrite.
- `n` cancels the overwrite.

This helps prevent accidental replacement of important data.

## 4. Copy Directories

```bash
cp -r archive archive-backup
```

Copies the directory and its contents recursively when the destination does not already exist.

The `-r` option allows `cp` to copy directories and their contents.

Always inspect the destination structure after copying.

```bash
ls -R archive archive-backup
```

Displays the contents of both directories and helps verify the backup.

## 5. Move and Rename Files

```bash
mv app-copy.txt archive/
```

Moves the file into the `archive` directory.

```bash
mv app-backup.txt app-copy.txt
```

Renames a file when the source and destination are in the same directory.

## 6. Rename Directories

```bash
mv archive-backup release-backup
```

Renames a directory without creating an additional copy.

The files inside remain in that directory.

## 7. Understand Relative Paths

```bash
cd ..
```

Moves to the parent directory.

```bash
cp ../notes.txt .
```

Copies `notes.txt` from the parent directory into the current directory.

In this command:

- `..` represents the parent directory.
- `.` represents the current directory.

Relative paths depend on the current working directory. Use `pwd` when unsure of your location.

## 8. Remove Files

```bash
rm notes.txt
```

Removes the specified file.

Before running `rm`, confirm your current directory and inspect the exact filename. File recovery may not be straightforward.

## 9. Remove Empty Directories

```bash
rmdir old-staging
```

Removes a directory only if it is empty.

If the directory contains files or subdirectories, `rmdir` fails and reports that the directory is not empty.

## 10. Remove a Directory Recursively

```bash
rm -r recursive-demo
```

Removes the specified directory and its contents recursively.

**Safety:** Always inspect the target before using `rm -r`. A path mistake can remove unintended data.

Avoid using `rm -rf` unnecessarily. The `-f` option suppresses confirmation and some error messages, making mistakes harder to notice.

## 11. Inspect and Verify Changes

```bash
ls -l
```

Displays a detailed listing of files and directories.

```bash
ls -la
```

Also includes hidden entries.

```bash
ls -R archive
```

Displays the directory and its contents recursively.

```bash
ls -ld archive
```

Displays information about the directory itself.

Verification is an important part of file management. After copying, moving, renaming, or removing something, inspect the result.

## 12. Practical DevOps Lessons

### Preparing a Deployment Workspace

Use `mkdir` to create directories and `touch` to create empty files.

### Creating a Backup

Use `cp` to preserve the original file and create a separate copy.

### Organizing Application Files

Use `mv` to move files into the correct directories or rename them.

### Cleaning Up Temporary Files

Inspect the target before using `rm` or `rmdir`. Use recursive deletion only when the entire target directory and its contents are confirmed to be unnecessary.

## Key Takeaways

- `cp` copies files; `mv` moves or renames them.
- `rm` removes files; `rmdir` removes empty directories.
- `cp -r` copies directory contents recursively.
- `rm -r` removes directories and their contents recursively.
- `cp -i` asks before overwriting an existing destination.
- Always check your current directory and verify the result of important operations.

## Learning Status

**Status:** Foundation-level file and directory operations practised. Continue building confidence through safe, hands-on troubleshooting scenarios.