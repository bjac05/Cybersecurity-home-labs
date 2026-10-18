# Day 3: Unix/Linux Command-Line Fundamentals

## Lab Overview

This lab introduces essential Unix command-line concepts
using macOS Terminal. The objective is to develop
foundational skills that transfer to Linux environments
commonly used in cybersecurity and system administration.

## Lab Objectives

- Navigate directories using the command line.
- List and inspect files and folders.
- Create directories and files using Terminal.
- Practice file management and basic security commands.
- Document commands and observations for a cybersecurity portfolio.

## Lab Environment

- Operating System: macOS
- Terminal: macOS Terminal (zsh)
- Text Editor: Visual Studio Code
- Lab Directory: Documents/Cybersecurity-Labs/Linux


## Commands Executed and Observations

### 1. File System Navigation

| Command | Purpose | Observation |
|---|---|---|
| `pwd` | Display current directory | Identified my home directory as `/Users/brandonjackson`. |
| `ls` | List directory contents | Identified folders and existing cybersecurity lab files. |
| `cd` | Change directories | Navigated into `Documents/Cybersecurity-Labs/Linux`. |
| `mkdir Linux` | Create a directory | Created a folder for Linux command-line exercises. |
| `touch day-03-linux-fundamentals.md` | Create an empty file | Created a Markdown document for lab findings. |
| `ls -a` | Show hidden directory entries | Observed `.` and `..` alongside my lab file. |
| `ls -l` | Display file details | Reviewed file ownership and read/write permissions. |
| `cat` | Display file contents | Viewed my Markdown lab report directly in Terminal. |

### 2. User Identity and Access Control

| Command | Purpose | Observation |
|---|---|---|
| `whoami` | Identify current user | Returned `brandonjackson`. |
| `id` | Display user and group IDs | Identified my user ID, primary group, and supplementary groups. |
| `id -Gn` | Display group names | Observed memberships including `staff` and `admin`. |

### 3. Process Monitoring

| Command | Purpose | Observation |
|---|---|---|
| `ps -ax` | List running processes | Identified running macOS system and application processes. |
| `ps -ax \| grep Terminal` | Filter processes by name | Located the Terminal application and its process ID. |
| `top` | Monitor processes in real time | Observed live CPU, memory, and process information. |

### 4. Operating System Identification

**Command:** `uname -a`

**Observed results:**
- Operating system kernel: Darwin
- Kernel version: 24.6.0
- Processor architecture: x86_64

**Security relevance:** Identifying system architecture and kernel versions supports system inventory, vulnerability research, and security investigations.

## Security Takeaways

- File permissions help enforce access restrictions and the principle of least privilege.
- User and group information supports identity and access management investigations.
- Process monitoring helps analysts identify programs that may require further investigation.
- Command-line tools can help analysts collect information and inspect files without a graphical interface.
- Precise filenames and verification are important when working in Terminal.

**Environment note:** These exercises were performed in macOS Terminal. The concepts and many commands transfer to Linux, but this lab did not use a native Linux operating system.


## Conclusion

During this lab, I gained hands-on experience using Unix command-line tools to navigate directories, create and inspect files, review permissions, identify user accounts, and monitor running processes. I also practiced troubleshooting a command error caused by an incomplete filename.

These exercises strengthened my understanding of file system management, access control, and basic system investigation techniques. Although I performed the exercises in macOS Terminal, many of the concepts and commands are transferable to Linux systems commonly used in cybersecurity environments.

This lab provided a foundation for future exercises involving log analysis, Linux administration, and security monitoring.