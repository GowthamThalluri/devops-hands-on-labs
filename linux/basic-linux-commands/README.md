# Basic Linux Commands — Hands-On Practice

## Overview

This topic covers commands for inspecting files, reading logs, searching text, checking system information, creating symbolic links, and working with command output.

The exercises were performed in Ubuntu on WSL. The commands below are useful for everyday Linux administration and DevOps troubleshooting.

## 1. Identify File Types

```bash
file app.img
```

Identifies a file's contents using available format signatures and other clues.

Example output:

```text
app.img: data
```

This means the command could not identify a more specific format. It does not automatically mean the file is corrupted.

## 2. Inspect File Metadata

```bash
stat app.img
```

Displays metadata such as:

- File size
- File type
- Permissions and ownership
- Inode and hard-link count
- Access, modification, and metadata-change timestamps
- Creation time, when supported by the filesystem

Important timestamp differences:

- **Access:** Last recorded read/access time.
- **Modify:** Last time file contents changed.
- **Change:** Last time file contents or metadata changed.
- **Birth:** Creation time, when available.

The `Change` timestamp is not the same as the file creation time.

## 3. Display File Contents

```bash
cat app.log
```

Displays the contents of a file. It is useful for reading small configuration files and logs.

For very large files, use tools such as `less`, `head`, or `tail` to avoid flooding the terminal.

## 4. Read the End of a Log

```bash
tail -n 5 app.log
```

Displays up to the last five lines of a file.

If a file contains fewer than five lines, all available lines are displayed.

## 5. Follow a Log in Real Time

```bash
tail -f app.log
```

Displays the end of a file and waits for new lines to be appended.

Press `Ctrl + C` to stop following the file.

This is useful when observing application logs during deployments and troubleshooting. The command reads the log; it does not generate new log messages itself.

## 6. Count Lines

```bash
wc -l app.log
```

Counts newline characters in a file. For a normally newline-terminated text file, this corresponds to its line count.

Example:

```text
1 app.log
```

A file containing one log message may have just one line even if that message describes a serious error.

## 7. Search Logs Using grep

### Find error messages

```bash
grep -i "error" app.log
```

Searches for lines containing `error`, ignoring uppercase and lowercase differences.

### Include line numbers

```bash
grep -in "error" app.log
```

The `-n` option displays the line number for each matching line.

### Include filenames

```bash
grep -inH "error" app.log another.log
```

The `-H` option displays the filename alongside matching lines.

### Search specific log files

```bash
grep -inH "error" \
/path/to/application.log \
/path/to/app.log
```

Searches the listed files and reports matching filenames, line numbers, and text.

No output means no matching lines were found in the specified files. It does not prove that the application is healthy.

## 8. Navigate Large Files with less

```bash
less app.log
```

Opens a file for interactive inspection without printing its entire contents at once.

Useful controls:

- Up/Down arrows: move through the text.
- Space: move down one screen.
- `/error`: search for a term.
- `n`: move to the next search match.
- `q`: exit.

Use `less` when a file is too large to inspect comfortably with `cat`.

## 9. Check System Date and Time

```bash
date
```

Displays the configured system date, time, and timezone.

This is useful when comparing timestamps across system logs or investigating when an event occurred.

Always account for timezone differences when comparing logs from multiple systems.

## 10. Check System Uptime and Load

```bash
uptime
```

Displays the current time, uptime, logged-in user count, and load averages for the last 1, 5, and 15 minutes.

Load average is not a CPU-utilization percentage. Interpret it alongside CPU count, process state, memory, and other performance indicators.

In WSL, the reported uptime relates to the Linux environment.

## 11. Check Logged-In Sessions

```bash
who
```

Lists recorded login sessions when available.

It may return no output in WSL or other environments where traditional login-session records are unavailable. An empty result does not necessarily indicate a problem.

## 12. Create a Symbolic Link

```bash
ln -s /path/to/original.log /path/to/log-link
```

Creates a symbolic link pointing to an existing file or directory.

The first path is the target, and the second path is the new link.

Symbolic links can provide convenient paths to logs, configuration files, or application releases without copying the underlying content.

Check a link with:

```bash
ls -l /path/to/log-link
```

Confirm that the destination name is unused before creating a link. The link and its target are separate filesystem entries.

## 13. Read Command Manuals

```bash
man grep
```

Opens the manual page for a command.

Useful controls:

- Arrow keys: navigate.
- `/term`: search for a term.
- `n`: find the next occurrence.
- `q`: exit.

Manual pages are useful when learning unfamiliar options without relying on copied commands.

## 14. Locate Command Files

```bash
whereis grep
```

Searches standard locations for the command's executable, source files, and manual documentation.

Compare it with:

```bash
command -v grep
```

`command -v` tells you how the current shell resolves a command. `whereis` searches standard locations for related files.

## 15. Sort Text Output

```bash
printf 'warning\nerror\ninfo\nerror\n' | sort
```

Sorts the sample lines alphabetically.

The pipe (`|`) sends the output of one command to the next command.

`sort` retains duplicate lines unless additional processing is used.

## 16. Remove Duplicate Lines

```bash
printf 'error\nwarning\nerror\nerror\ninfo\n' | sort | uniq
```

Sorts the sample text and removes consecutive duplicate lines.

`uniq` only removes adjacent duplicates, so `sort | uniq` is a common combination when duplicates may be scattered throughout the input.

These commands operate on sample text and do not modify files.

## 17. Check a URL Without Downloading a File

```bash
wget --spider https://example.com
```

Checks a remote URL without saving a downloaded file.

A successful result may show:

- DNS resolution
- Connection establishment
- HTTP status such as `200 OK`

A successful HTTP response confirms that the particular request succeeded. It does not prove that every endpoint or application component is healthy.

## 18. Check Command Availability

```bash
command -v wget
```

Prints the command path when it is available in the current shell's search path.

If the command is unavailable, the command may produce no output. Do not install additional packages just to complete an optional exercise.

During this practice, `locate` and `cal` were checked but were not available in the environment. They were skipped rather than installed.

## 19. Practical Troubleshooting Workflow

When investigating an application issue:

1. Inspect the relevant log file using `less` or `tail`.
2. Search for relevant messages with `grep`.
3. Include line numbers and filenames when searching multiple logs.
4. Use `stat` to inspect file metadata when necessary.
5. Check the system time with `date` when comparing timestamps.
6. Use `wget --spider` for a basic URL request check when appropriate.
7. Treat the output as evidence and investigate the actual cause before changing anything.

### Important lesson

A log message is evidence, not proof that a server is currently down.

During practice, a local file contained:

```text
ERROR: Server connection timeout data
```

We confirmed that the message existed in the file and located its line number. We did not establish that a real server was currently unavailable.

## Key Takeaways

- Use `file` and `stat` to inspect unfamiliar files.
- Use `cat`, `less`, and `tail` to read logs.
- Use `wc` to count lines and `grep` to find matching text.
- Use `date` and `uptime` to inspect system time and uptime.
- Use `ln -s` to create symbolic links.
- Use `man` to learn command options.
- Use `sort | uniq` to sort text and remove duplicate lines.
- Use `wget --spider` for a basic remote URL check.
- Interpret command output in context before deciding on corrective action.

## Learning Status

**Status:** Additional basic Linux commands practised through hands-on exercises. Process management, networking diagnostics, service administration, and deeper system troubleshooting will be covered in their dedicated topics.