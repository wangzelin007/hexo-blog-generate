---
title: linux基础命令
date: 2019-01-24 22:43:04
tags: [linux]
categories: Linux
toc: true
mathjax: true
---
# 介绍`ls` `cat ` `mv` `touch` 的基本用法

## ls
```
List directory contents.
  
- List files one per line:
  ls -1
   
- List all files, including hidden files:
  ls -a
   
- Long format list (permissions, ownership, size and modification date) of all files:
  ls -la
   
- Long format list with size displayed using human readable units (KB, MB, GB):
  ls -lh
   
- Long format list sorted by size (descending):
  ls -lS
   
- Long format list of all files, sorted by modification date (oldest first):
  ls -ltr
```

## cat

```
Print and concatenate files.

- Print the contents of a file to the standard output:
  cat file

- Concatenate several files into the target file:
  cat file1 file2 > target_file

- Append several files into the target file:
  cat file1 file2 >> target_file

- Number all output lines:
  cat -n file
```


## mv
```
Move or rename files and directories.

- Move files in arbitrary locations:
  mv source target

- Do not prompt for confirmation before overwriting existing files:
  mv -f source target

- Prompt for confirmation before overwriting existing files, regardless of file permissions:
  mv -i source target

- Do not overwrite existing files at the target:
  mv -n source target

- Move files in verbose mode, showing files after they are moved:
  mv -v source target
```

## touch
```
Change a file access and modification times (atime, mtime).

- Create a new empty file(s) or change the times for existing file(s) to current time:
  touch filename

- Set the times on a file to a specific date and time:
  touch -t YYYYMMDDHHMM.SS filename

- Use the times from a file to set the times on a second file:
  touch -r filename filename2
```

