# Linux File Searching

## Overview

Linux provides commands to find files and directories without manually checking every folder.

The `find` command is useful for locating application files, configuration files, logs, and other files during troubleshooting.

## 1. Search by Filename

```bash
find /home/gowtham -name "backup.sh"
```

Finds files or directories named `backup.sh` under `/home/gowtham`, matching capitalization exactly.

## 2. Search Using Wildcards

```bash
find /home/gowtham/linux-practice -type f -name "*.log"
```

Finds regular files whose names end in `.log`.

The quotes prevent the shell from expanding the wildcard before `find` receives it.

Common patterns:

- `"*.log"` matches names ending in `.log`.
- `"config*"` matches names beginning with `config`.
- `"*config*"` matches names containing `config`.

## 3. Search for Directories

```bash
find /home/gowtham/linux-practice -type d -name "backup"
```

Finds directories named `backup`.

## 4. Search Without Case Sensitivity

```bash
find /home/gowtham/linux-practice -type f -iname "*.LOG"
```

Finds regular files ending in `.LOG`, `.log`, or another capitalization of that extension.

- `-name` matches capitalization exactly.
- `-iname` ignores capitalization.

## 5. Find Large Files

```bash
find /home/gowtham -type f -size +1M
```

Finds regular files larger than 1 MiB.

This is useful when investigating files that might be consuming significant storage.

## 6. Find Empty Files

```bash
find /home/gowtham/linux-practice -type f -empty
```

Finds empty regular files.

Empty files may be intentional, so inspect them before deciding whether they should be removed.

## 7. Search by Modification Time

```bash
find /home/gowtham/linux-practice -type f -mmin -1440
```

Finds regular files modified less than 1,440 minutes (24 hours) ago.

```bash
find /home/gowtham/linux-practice -type f -mmin -10080
```

Finds regular files modified less than 10,080 minutes (7 days) ago.

## 8. Combine Search Conditions

```bash
find /home/gowtham/linux-practice -type f -name "*.log" -mmin -10080
```

Finds regular `.log` files modified within the last seven days.

All the conditions must match for a file to appear in the output.

## 9. Limit Search Depth

```bash
find /home/gowtham/linux-practice -maxdepth 1 -type f -iname "*config*"
```

Finds matching regular files directly inside the starting directory without descending into its subdirectories.

`-maxdepth` controls how deeply `find` searches, starting with the specified location at depth zero.

## 10. Practical Troubleshooting

### Scenario: A configuration file is missing

Search by a filename pattern:

```bash
find /home/gowtham/linux-practice -type f -iname "*config*"
```

### Scenario: A deployment log was recently updated

```bash
find /home/gowtham/linux-practice -type f -name "*.log" -mmin -1440
```

### Scenario: A large file might be consuming disk space

```bash
find /home/gowtham -type f -size +100M
```

This identifies regular files larger than 100 MiB. Investigate the results before taking action.

## Key Takeaway

`find` becomes more useful when several conditions are combined, such as filename, file type, size, modification time, and search depth.

Always inspect the results before moving or deleting files.

## Learning Status

**Status:** Foundation-level file-searching practice completed.