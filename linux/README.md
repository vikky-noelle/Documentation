# Linux

## Introduction to Linux

Linux is an open-source operating system. Linux kernel is the main component on which different versions of Linux often referred to as Distributions or Distros are based off.
It was made to have stability and security, hence why it is used in servers and other critical things. It is also lightweight compared to other OS.
Linux was designed to be similar to UNIX but has been evolved to run in phones to supercomputers. The Linux kernel is the most important aspect of it.

# RUN `man` command_name to get the documentation for a specific command.

## Files & Processes

In Linux, everything is either a file or a process. The file is the source of a stream of data.
On the other hand is just a program that is currently running, a file stores the instructions that are executed for that process to run.

## Listing Files & Directories

Commands that are used often:

- `ls` a command that lists out all the files in a directory.
- `ls -ll` tag gives detailed information about the directory/files along with reading, write rights on the file, owner, and when the file was created.
- `ls -A` gives the list of all files including the hidden ones.

## The Directory Structure

`Directory` Description

- `/`
  Primary hierarchy root and root directory of the entire file system hierarchy.
- `/bin`
  Essential command binaries that need to be available in single-user mode; for all users, e.g., cat, ls, cp.
- `/boot`
  Boot loader files, e.g., kernels, initrd.
- `/dev`
  Device files, e.g., /dev/null , /dev/disk0 , /dev/sda1 , /dev/tty , /dev/random.
- `/etc`
  Host-specific system-wide configuration files.
  There has been controversy over the meaning of the name itself. In early versions of the UNIX Implementation Document from Bell labs, /etc is referred to as the etcetera directory, as this directory historically held everything that did not belong elsewhere (however, the FHS restricts /etc to static configuration files and may not contain binaries). Since the publication of early documentation, the directory name has been re-explained in various ways. Recent interpretations include acronyms such as "Editable Text Configuration" or "Extended Tool Chest."
- `/etc/opt`
  Configuration files for add-on packages that are stored in /opt .
- `/etc/sgml`
  Configuration files, such as catalogs, for software that processes SGML.
- `/etc/X11`
  Configuration files for the X Window System, version 11.
- `/etc/XML`
  Configuration files, such as catalogs, for software that processes XML.
- `/home`
  Users' home directories, containing saved files, personal settings, etc.
- `/lib`
  Libraries are essential for the binaries in /bin and /sbin.
- `/lib<qual>`
  Alternative format essential libraries. Such directories are optional, but if they exist, they have some requirements.
- `/media`
  Mount points for removable media such as CD-ROMs (appeared in FHS-2.3 in 2004).
- `/mnt`
  Temporarily mounted filesystems.
- `/opt`
  Optional application software packages.
- `/proc`
  Virtual filesystem providing process and kernel information as files. In Linux, corresponds to a procfs mount. Generally automatically generated and populated by the system, on the fly.
- `/root`
  The home directory for the root user.
- `/run`
  Run-time variable data: Information about the running system since last boot, e.g., currently logged-in users and running daemons. Files under this directory must be either removed or truncated at the beginning of the boot process, but this is not necessary on systems that provide this directory as a temporary filesystem (tmpfs).
- `/sbin`
  Essential system binaries, e.g., fsck, init, route.
- `/srv`
  Site-specific data served by this system, such as data and scripts for web servers, data offered by FTP servers, and repositories for version control systems (appeared in FHS-2.3 in 2004).
- `/sys`
  Contains information about devices, drivers, and some kernel features.
- `/tmp`
  Temporary files (see also /var/tmp). Often not preserved between system reboots, and maybe severely size restricted.
- `/usr`
  Secondary hierarchy for read-only user data; contains the majority of (multi-)user utilities and applications.
- `/usr/bin`
  Non-essential command binaries (not needed in single-user mode); for all users.
- `/usr/include`
  Standard include files.
- `/usr/lib`
  Libraries for the binaries in /usr/bin and /usr/sbin.
- `/usr/lib<qual>`
  Alternative format libraries, e.g. /usr/lib32 for 32-bit libraries on a 64-bit machine (optional).
- `/usr/local`
  Tertiary hierarchy for local data, specific to this host. Typically has further subdirectories, e.g., bin, lib, share.
- `/usr/sbin`
  Non-essential system binaries, e.g., daemons for various network-services.
- `/usr/share`
  Architecture-independent (shared) data.
- `/usr/src`
  Source code, e.g., the kernel source code with its header files.
- `/usr/X11R6`
  X Window System, Version 11, Release 6 (up to FHS-2.3, optional).
- `/var`
  Variable files—files whose content is expected to continually change during normal operation of the system—such as logs, spool files, and temporary e-mail files.
- `/var/cache`
  Application cache data. Such data are locally generated as a result of time-consuming I/O or calculation. The application must be able to regenerate or restore the data. The cached files can be deleted without loss of data.
- `/var/lib`
  State information. Persistent data modified by programs as they run, e.g., databases, packaging system metadata, etc.
- `/var/lock`
  Lock files. Files keeping track of resources currently in use.
- `/var/log`
  Log files. Various logs.
- `/var/mail`
  Mailbox files. In some distributions, these files may be located in the deprecated /var/spool/mail.
- `/var/opt`
  Variable data from add-on packages that are stored in /opt.
- `/var/run`
  Run-time variable data. This directory contains system information data describing the system since it was booted.
  In FHS 3.0, /var/run is replaced by /run ; a system should either continue to provide a /var/run directory, or provide a symbolic link from /var/run to /run , for backwards compatibility.
- `/var/spool`
  Spool for tasks waiting to be processed, e.g., print queues and outgoing mail queue.
- `/var/spool/mail`
  Deprecated location for users' mailboxes.
- `/var/tmp`
  Temporary files to be preserved between reboots.

## Making directories

`mkdir` directory_name is the command to make directories.
E.g `mkdir new_folder`

## The Directories . and ..

There are 2 major things when you are going about the directories.
The current directory and parent directory can be relatively symbolized as double dots and single dots respectively.
They are usually hard links present in every directory and are hidden hence not shown in normal ls command but can be seen in ls -a.

If you don’t understand how it will be used, refer to the next section and read it combined with this.

## Changing Directories & Pathnames

Consider this directory structure.

<pre>
|---Folder1
|---Folder2---|----ChildFolder1
|             |----ChildFolder2
</pre>

### There are two ways you can change directories.

- Providing the absolute path to the directory, that is saying `Folder2/ChildFolder1`.
  Typically it would look like `cd /home/Folder2/ChildFolder1`.
- Providing a relative path is where the previous section comes in. Let us assume that we are in Folder2
  You can access ChildFolder1 by `cd ./ChildFolder1`.
  You can access Folder1 by `cd ../Folder1`.

## Copying Files

Copying files is fairly easy and can be done with the cp command, but the cp command can not copy directories, and if directories are to be copied use `cp -R`.
`Cp [source] [destination]`

`cp example.txt ../folderOne`
The files can also be renamed while copying by simply giving a name with the destination for the file, the same holds for directories.
`cp example.txt ../folderOne/renamed.txt`

## Moving Files

Moving files or directories are fairly easy and can be done with the mv command.
`mv [source] [destination]`

`mv example.txt ../folderOne`
The files can also be renamed while copying by simply giving a name with the destination for the file, the same holds for directories.
`mv example.txt ../folderOne/renamed.txt`

## Removing Files and Directories

- Removing a file can be done with `rm file_name`.
- Removing a directory, given that it is empty can be done by either `rm -d directory_name` or `rmdir` directory_name.
- Removing a non-empty directory can be done by `rm -R directory_name` where `-R` stands for recursively which in turn means removing child folders and files first.

## Displaying the contents of a file

You can view the contents of the file using cat, less, more, and gnome-open.
Use command[cat, less, more, gnome-open] filename.

`cat example.txt`

**Output** [example.txt]

`This is an example.`

## Searching Content In A File

- Searching in files can be done through the command line using `grep`.
  `grep keyword1 keyword2 filename`
- You can ignore casing by using `-i`.
  `grep -i keyword1`
- You can use invert match to find files that do not have the string.
  `grep -v keyword1`
- You can use `-c` to count the result set.
  `grep -c keyword1`

## Redirection

The work of any command is either taking input or gives an output or both. So, Linux has some command or special character to redirect these input and output functionalities. For example: suppose we want to run a command called “date” if we run it will print the output to the current terminal screen. But our requirement is different, we don’t want the output to be displayed on the terminal. We want the output to be saved in a file. This could be done very easily with output redirection. Redirection here simply means diverting the output or input.

### Types of Redirection

1.  Overwrite

    `>` standard output
    `<` standard input

2.  Appends

    `>>` standard output
    `<<` standard input 3. Merge

    `p >& q` Merges output from stream p with stream q
    `p <& q` Merges input from stream p with stream q

### Command examples

`cat example.txt > output.txt`

`cat < example.txt` overwrites the file

`cat << example.txt` appends in the file

## Pipes

A pipe is a form of redirection (transfer of standard output to some other destination) that is used in Linux and other Unix-like operating systems to send the output of one command/program/process to another command/program/process for further processing. The Unix/Linux systems allow stdout of a command to be connected to stdin of another command. You can make it do so by using the pipe character `|`.

Syntax :
`command_1 | command_2 | command_3 | .... | command_N`

`ls -l | more`

`cat result.txt | grep "abc" | tee file2.txt | wc -l`

This command is used to display the content of result.txt and search for string abc and store the result in file2.txt and finally printing the line count.

## Filename Conventions

To prevent running into problems with your file paths on your site, these are the following guidelines:

- Name all your files lower case.
- Instead of using a space, use an `\_` or a `–`
- Use consistent file types. Use jpg or jpg. Don’t use both.
- Only alphanumeric characters, periods, underscores, and hyphens and don’t use symbols like `%`, `$`, and so forth.
- Keep the file names short and descriptive.

## Viewing processes

You can use the `top` or `ps -aux` or `sudo ps -a` command to view the current processes.
The **process ID** `PID` is essential to kill or control process on Linux. For example consider the following outputs:

`root 1 0.0 0.0 225868 9760 ? Ss 19:10 0:13 /sbin/init splash`

Where,

`root` User name

`1` PID (Linux process ID)

`19:10` Process start time

`/sbin/init splash` Actual process or command

There may be too many processes. Hence, it uses the following less command/more command as a pipe to display process one screen at a time:

`vivek@nixcraft:~$ ps -aux | more`

`vivek@nixcraft:~$ sudo ps -aux | less`

## Killing A Process

Now we come to the task of killing the process. We have two pieces of information that will help us kill the errant process:

- Process name
- Process ID

Which you use will determine the command used for termination. There are two commands used to kill a process:

- `kill` Kill a process by ID
- `killall` Kill a process by name

Different signals can be sent to both kill commands. What signal you send will be determined by what results in you want from the kill command. For instance, you can send the `HUP` (hangup) signal to the kill command, which will effectively restart the process. This is always a wise choice when you need the process to immediately restart (such as in the case of a daemon). You can get a list of all the signals that can be sent to the kill command by issuing kill -l. You’ll find quite a large number of signals (Figure 3).
Figure 3: The available kill signals.
The most common kill signals are:

`Signal Name` _Single Value_ **Effect**

- `SIGHUP` _1_ **Hangup**
- `SIGINT` _2_ **Interrupt from keyboard**
- `SIGKILL` _9_ **Kill signal**
- `SIGTERM` _15_ **Termination signal**
- `SIGSTOP` _17, 19, 23_ **Stop the process**

What’s nice about this is that you can use the Signal Value in place of the Signal Name. So you don’t have to memorize all of the names of the various signals.
So, let’s now use the kill command to kill our instance of chrome. The structure for this command would be:
`kill SIGNAL PID`
Where SIGNAL is the signal to be sent and `PID` is the **Process ID** to be killed.
We already know, from our ps command that the IDs we want to kill are `3827, 3919, 10764, and 11679`. So to send the kill signal, we’d issue the commands:

`kill -9 3827`

`kill -9 3919`

`kill -9 10764`

`kill -9 11679`

Once we’ve issued the above commands, all of the chrome processes will have been successfully killed.

## File System Security (Access Rights)

The Linux security model is based on the one used on UNIX systems and is as rigid as the UNIX security model (and sometimes even more), which is already quite robust. On a Linux system, every file is owned by a user and a group user. There is also a third category of users, those that are not the user owner and don't belong to the group owning the file. For each category of users, read, write and execute permissions can be granted or denied.

We already used the long option to list files using the `ls -l` command, though for other reasons. This command also displays file permissions for these three user categories; they are indicated by the nine characters that follow the first character, which is the file type indicator at the beginning of the file properties line. As seen in the examples below, the first three characters in this series of nine display access rights for the actual user that owns the file. The next three are for the group owner of the file, the last three are for other users. The permissions are always in the same order: read, write, execute for the user, the group, and the others. Some examples:

<pre>
marise:~> ls -l To_Do
-rw-rw-r-- 1 marise users 5 Jan 15 12:39 To_Do
marise:~> ls -l /bin/ls
-rwxr-xr-x 1 root root 45948 Aug 9 15:01 /bin/ls\*
</pre>

The first file is a regular file (first dash). Users with user name Marise or users belonging to the group users can read and write (change/move/delete) the file, but they can't execute it (second and third dash). All other users are only allowed to read this file, but they can't write or execute it (fourth and fifth dash).
The second example is an executable file, the difference: everybody can run this program, but you need to be root to change it.
The Info pages explain how the ls command handles the display of access rights in detail, see the section What information is listed.
For easy use with commands, both access rights or modes and user groups have a code. See the tables below.

### Access mode codes

`Code` Meaning

- `0 or -`
  The access right that is supposed to be on this place is not granted.
- `4 or r`
  read access is granted to the user category defined in this place
- `2 or w`
  write permission is granted to the user category defined in this place
- `1 or x`
  execute permission is granted to the user category defined in this place

### User group codes

`Code` Meaning

- `u`
  user permissions
- `g`
  group permissions
- `o`
  permissions for others

This straightforward scheme is applied very strictly, which allows a high level of security even without network security. Among other functions, the security scheme takes care of user access to programs, it can serve files on a need-to-know basis and protect sensitive data such as home directories and system configuration files.

The permission in the command line is displayed as `\_rwxrwxrwx 1 owner: group`

### User rights/Permissions

1. The first character that I marked with an underscore is the special permission flag that can vary.

2. The following set of three characters `rwx` is for the owner’s permission.

3. The second set of three characters `rwx` is for the Group permissions.

4. The third set of three characters `rwx` is for the All Users permissions.

Following that grouping since the integer/number displays the number of hard links to the file.
The last piece is the Owner and Group assignment formatted as Owner: Group.

## Changing Access Rights

To change directory permissions in Linux, use the following:

`chmod +rwx` filename to add permissions.

`chmod -rwx` directory name to remove permissions.

`chmod +x filename` to allow executable permissions.

`chmod -wx filename` to take out write and executable permissions.

Note that `r` is for read, `w` is for write, and `x` is for execute.
This only changes the permissions for the owner of the file.

### How to Change Directory Permissions in Linux for the Group Owners and Others

The command for changing directory permissions for group owners is similar, but add a `g` for group or `o` for users:

<pre>
chmod g+w filename

chmod g-wx filename

chmod o+w filename

chmod o-rwx foldername
</pre>

To change directory permissions for everyone, use `u` for users, `g` for the group, `o` for others, and `ugo` or `a` (for all).

`chmod ugo+rwx folder name` to give read, write, and execute to everyone.

`chmod a=r folder name` to give only read permission for everyone.

### How to Change Groups of Files and Directories in Linux

By issuing these commands, you can change groups of files and directories in Linux.

`chgrp group name filename`

`chgrp groupname foldername`

Note that the group must exit before you can assign groups to files and directories.

### How to Change Ownership in Linux

Another helpful command is changing ownerships of files and directories in Linux:

`chown name filename`

`chown name foldername`

These commands will give ownership to someone, but all sub files and directories still belong to the original owner.

You can also combine the group and ownership command by using:
`chown -R name:filename /home/name/directoryname`

This command gives someone the ownership of the directory tsfiles, and all files and subfolders. The `-R` stands for recursive, which transfers ownership of all subdirectories to the new owner.

### How to Change Permissions in Numeric Code in Linux

You may need to know how to change permissions in numeric code in Linux, so to do this you use numbers instead of `r`, `w`, or `x`.

- 0 = No Permission
- 1 = Execute
- 2 = Write
- 4 = Read

You add up the numbers depending on the level of permission you want to give.

Permission numbers are:

- 0 = ---
- 1 = --x
- 2 = -w-
- 3 = -wx
- 4 = r-
- 5 = r-x
- 6 = rw-
- 7 = rwx

For example:

`chmod 777 foldername` will give read, write, and execute permissions for everyone.

`chmod 700 foldername` will give read, write, and execute permissions for the user only.

`chmod 327 foldername` will give write and execute (3) permission for the user, w (2) for the group, and read, write, and execute for the users.

## Shell Variables

Shell variables are variables that you define in an instance of shell, they disappear as soon as the shell is destroyed and are often defined as variable=value and accessed through echo $variable

You can also unset these variables using the unset command unset variable_name.

## Other Useful Linux Commands

- `Sudo su` a command that takes you to the root and gives you absolute permission.
- `Clear` a command that clears the terminal of any content.
- `Sudo` a command that gives you root user rights, it can be used to run commands that need root permissions.
- `Pwd` is a command that tells you the path to the current directory.
- `which [filename1] [filename2] …` a command in Linux is a command which is used to locate the executable file associated with the given command by searching it in the path environment variable. It has 3 return statuses as follows:
  `0` If all specified commands are found and executable.
  `1` If one or more specified commands is nonexistent or not executable.
  `2` If an invalid option is specified.
- `find` command
- `-sh` tag lets you see the size of the files
- `Dd if=/dev/zero of=ramu bs=1M count=10` will create a 10MB file with the name of Ramu.
- `free` gives information on processes, eg. `free -h` will give the ram usage.
- `locate` command is also used to find files but it is not in real time and hence there is a lag between results. It is not enabled in systems by default. You can't use it to find files that were created a few minutes ago since locate is based upon indexing, and index is not updated in real time.