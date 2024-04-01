# Introduction to the Command Line for Bioinformatics

Welcome to the "Introduction to the Command Line" module, an essential component of our bioinformatics bootcamp. This module will guide you through the basics of command-line interfaces (CLI), focusing on Bash, the most common shell in UNIX and UNIX-like operating systems, which is crucial for bioinformatics workflows.

## Understanding the Command Line vs. GUI

The **command line interface (CLI)** and **graphical user interface (GUI)** are two primary ways users interact with computers. The GUI is what most are familiar with; it's visual, allowing interaction through graphical icons and visual indicators. On the other hand, the CLI is text-based, where users execute commands by typing text on a terminal.

### Why Use the Command Line in Bioinformatics?

- **Efficiency**: Performing repetitive tasks is faster and simpler in CLI.
- **Automation**: Scripts can automate repetitive tasks, saving time and reducing errors.
- **Power and Flexibility**: The CLI often allows for more detailed control and customization of operations.
- **Resource Efficiency**: CLI applications require fewer system resources than their GUI counterparts.

## Basic Command Line Navigation

Navigating the filesystem in Bash is a fundamental skill. Here are some essential commands:

- `pwd` (Print Working Directory): Displays the path of the current directory.
- `ls` (List): Lists files and directories in the current directory. 
	- `ls -l` (List Long): Show a list with details like file size and owner
	- `ls -a` (List All): Include hidden files.
- `cd` (Change Directory): Changes the current directory. 
	- `cd ..`: Move up one directory.
	- `cd`: Return to the home directory.
	- `cd directory_name`: Move to the provided directory.
- `mkdir` (Make Directory): Creates a new directory.
- `rmdir` (Remove Directory): Deletes an empty directory.
- `touch`: Creates a new empty file or updates the timestamp of an existing file.
- `rm` (Remove): Deletes files. Use carefully, especially with `rm -r` for recursive deletion. When used incorrectly, this can delete your whole file system, and unlike your computer's operating system, there is no bin to pull deleted files out of. When they are deleted, they are gone.

## Basic File Operations

Manipulating files is a frequent task. Here are some commands for basic file operations:

- `cp` (Copy): Copies files or directories. For example, `cp source.txt destination.txt`.
- `mv` (Move): Moves or renames files or directories. For example, `mv oldname.txt newname.txt`.
- `cat` (Concatenate): Displays the content of files. It can also combine multiple files.
- `head` and `tail`: Show the beginning and end of files, respectively. Useful for previewing data.
- `grep`: Searches for patterns within files. Extremely useful for finding specific data.


## Understanding File Permissions in UNIX/Linux

In UNIX and Linux systems, file permissions control the level of access granted to users for reading, writing, and executing files and directories. Understanding and managing file permissions is crucial for ensuring the security and proper functionality of files within the system.

### Viewing File Permissions

To view file permissions, you can use the `ls -l` command. This will display a list of files in the current directory, along with their permissions, number of links, owner, group, size, and modification date. The permissions are shown in the first column, and they look something like this: `-rwxr-xr--`.

The permissions string can be broken down as follows:

- The first character indicates the type of file (`-` for a regular file, `d` for a directory, etc.).
- The next three characters show the owner's permissions.
- The following three are for the group's permissions.
- The last three are for everyone else's (others) permissions.

Each set of three permissions represents:
- **r**: read permission
- **w**: write permission
- **x**: execute permission

### Changing File Permissions with `chmod`

The `chmod` (change mode) command is used to change the permissions of a file or directory. Permissions can be specified in symbolic mode (using letters) or numeric mode (using numbers).

#### Symbolic Mode

In symbolic mode, you can add, remove, or set permissions using the `+`, `-`, and `=` operators respectively, combined with the letters `r`, `w`, `x`, for the user (`u`), group (`g`), others (`o`), or all (`a`). For example:

- To add execute permission for all users: `chmod a+x filename`
- To remove write permission for the group: `chmod g-w filename`
- To set read and write permissions for the owner only: `chmod u=rw,go= filename`

#### Numeric Mode

Numeric mode uses octal numbers to represent permissions. Each of the read, write, and execute permissions has a numerical value:

- **r** (read) = 4
- **w** (write) = 2
- **x** (execute) = 1

The permissions are represented by a three-digit number, summing up the values for each set of permissions. For example:

- **7** (4+2+1) for read, write, and execute
- **6** (4+2) for read and write
- **5** (4+1) for read and execute

So, to set the owner permissions to read, write, and execute, the group to read and execute, and others to read only, you would use: `chmod 754 filename`

### Best Practices for Permissions

- Be cautious when setting execute permissions, especially for "others," to avoid security risks.
- For scripts and executable files, ensure only trusted users have write access.
- Use the most restrictive permissions necessary for a file or directory to function correctly.

Understanding and managing permissions is a key aspect of system administration and security. Regularly reviewing permissions and adjusting them as necessary can help protect sensitive data and maintain the integrity of your bioinformatics workflows.

## Introduction to Scripting

While Bash is our primary focus, being aware of other scripting languages such as Python, R, and Perl can be beneficial. These languages offer powerful libraries and tools for bioinformatics analysis, data manipulation, and automation.

## Practice Exercises

1. Navigate to your home directory and create a new directory named `bioinfo_projects`.
2. Inside `bioinfo_projects`, create an empty file named `sample.txt`.
3. Use `ls` to list all items within `bioinfo_projects` and `cat` to display the contents of `sample.txt`.
4. Practice More with this Online Tutorial from [Linux Journey](https://linuxjourney.com/lesson/the-shell)


Congratulations on completing this introductory module! You've taken your first step into the powerful world of command-line interfaces, a cornerstone of bioinformatics analysis.
