# Linux Command Cheat Sheet
This sheet highlights the most commonly used Linux commands with context so you can navigate and manage your system confidently.

### Help Documentation / Manual aka "man"
```bash 
man <command> # display manual page for command; `man 5 passwd` shows section 5.
```

### Helpful Flags & Patterns
```bash
-h or --human-readable # display sizes in KB, MB, GB format (df, du, ls).
-r or -R # recursive operation (cp, rm, chmod, chown, grep).
-v # verbose output showing detailed operation progress.
-i # interactive mode prompting before destructive actions.
-f # force operation without prompts (use with caution).
```
**Tip:** Use `command --help` or `man command` to learn more about any command. Chain commands with `&&` to run sequentially only if previous succeeds, or `|` to pipe output between commands. Always verify destructive operations with `--dry-run` flags when available.


**Permission Reference:** Numeric values: `r=4, w=2, x=1`. Combine for permissions (e.g., 7=rwx, 6=rw-, 5=r-x). Symbolic: `u`=user, `g`=group, `o`=others, `a`=all. Operators: `+` add, `-` remove, `=` set exact.

###  File & Directory Navigation
```bash
pwd # print working directory; shows your current location.
cd <directory> # change directory; use `..` to move up one level, `-` to go back to previous.
ls -al # list directory contents; `-a` shows hidden files, `-l` uses long format with details.
ls -lh --color=auto # list with human-readable sizes and color highlighting.
```
###  File Operations
```bash
cat <file> # concatenate and display file contents; use multiple files to merge output.
cat -n <file> # number all lines in output.
head <file> # display first 10 lines; use `-n 20` to show 20 lines.
tail <file> # display last 10 lines; `-f` follows file updates in real-time.
touch <file> # create empty file or update timestamps.
cp <source> <dest> # copy files; use `-r` for recursive directory copy.
mv <old> <new> # move or rename files and directories.
rm <file> # remove files; use `-rf` for recursive force deletion (caution: irreversible).
mkdir <dir> # create directory; `-p` creates parent directories as needed.
rmdir <dir> # remove empty directory.
```
### File Viewing & Editing
```bash
less <file> # paginated file viewer; `/pattern` to search, `q` to quit.
more <file> # basic pager for viewing files.
nano <file> # simple terminal text editor.
vim <file> # powerful text editor with modal interface.
```
###  Text Processing & Search
```bash
grep "pattern" <file> # search for text patterns in files.
grep -rin "TODO" src/ # recursive case-insensitive search with line numbers.
grep -v "pattern" # invert match; show lines not matching pattern.
awk '{print $1}' <file> # pattern scanning; print first field of each line.
awk -F: '{print $1,$3}' /etc/passwd # use `:` as field separator.
sed 's/foo/bar/g' <file> # stream editor; replace all occurrences of foo with bar.
sed -i 's/old/new/g' <file> # edit file in-place.
cut -d: -f1 /etc/passwd # extract first field using `:` as delimiter.
sort <file> # sort lines alphabetically; `-n` for numeric, `-r` for reverse.
uniq # remove adjacent duplicate lines (often used with sort).
wc <file> # count lines, words, and bytes; `-l` for lines only.
```
### File Search & Comparison
```bash
find . -name "*.log" # search for files by name pattern.
find /var -type f -size +100M # find files larger than 100MB.
find . -name "*.log" -exec rm {} \; # execute command on found files.
diff <file1> <file2> # compare files line by line.
diff -u <old> <new> # unified diff format showing context.
```
### Permissions & Ownership
```bash
chmod 644 <file> # change file mode using numeric permissions (rw-r--r--).
chmod u+x <script> # add execute permission for user symbolically.
chmod -R 755 <dir> # recursively set permissions on directory.
chown <user> <file> # change file owner.
chown <user>:<group> <file> # change owner and group.
chown -R <user>:<group> <dir> # recursively change ownership.
```
**Permission Reference:** Numeric values: r=4, w=2, x=1. Combine for permissions (e.g., 7=rwx, 6=rw-, 5=r-x). Symbolic: u=user, g=group, o=others, a=all. Operators: + add, - remove, = set exact.

###  Process Management
```bash
ps aux # list all running processes with details.
ps -ef | grep <process> # find specific process.
top # real-time process viewer; press `k` to kill, `M` to sort by memory, `q` to quit.
kill <pid> # send TERM signal to process (graceful shutdown).
kill -9 <pid> # force kill process with KILL signal.
bg %1 # resume job in background.
jobs # list background jobs in current shell.
```
###  System Information
```bash
uname -a # display all system information (kernel, hostname, architecture).
hostname # show or set system hostname.
uptime # show how long system has been running and load average.
whoami # display current username.
who # show logged-in users.
date +"%Y-%m-%d %H:%M:%S" # display or format current date and time.
date -u # show UTC time.
```
###  Disk & Storage
```bash
df -h # show disk space usage in human-readable format.
df -T # include filesystem type in output.
du -sh * # summarize disk usage of each item in current directory.
du -h --max-depth=1 # show usage one level deep with human-readable sizes.
free -h # display memory usage in human-readable format.
```
###  Networking
```bash
ping <host> # test network reachability; `-c 4` to limit to 4 packets.
curl <url> # transfer data from URLs; `-O` to save with original filename.
curl -I <url> # fetch headers only; `-L` follows redirects.
dig <domain> # DNS lookup utility; `+short` for brief output.
ssh <user>@<host> # secure shell remote login.
ssh -i <keyfile> <user>@<host> # connect using specific private key.
scp <file> <user>@<host>:/path/ # secure copy file to remote system.
scp -r <dir> <user>@<host>:/path/ # recursively copy directory.
```
### Archives & Compression
```bash
tar -cvf archive.tar <dir> # create uncompressed tar archive.
tar -xvf archive.tar # extract tar archive.
tar -czf archive.tar.gz <dir> # create gzip-compressed archive.
tar -xzf archive.tar.gz # extract gzip archive.
zip archive.zip <file1> <file2> # create zip archive.
zip -r archive.zip <dir> # recursively zip directory.
unzip <file.zip> # extract zip archive; `-d <target>` specifies destination.
```
### Transfer & Sync
```bash
rsync -av <src> <dest> # fast incremental file transfer with archive mode and verbose output.
rsync -az --delete <host>:/data/ /local/ # sync with compression, deleting files not in source.
```
### Environment & Shell
```bash 
echo "text" # print text to stdout; `echo $VAR` displays variable value.
echo -n "text" # print without trailing newline; `-e` enables escape sequences.
env # display all environment variables.
export VAR=value # set environment variable for current session and child processes.
export PATH=$PATH:/new/bin # append to PATH variable.
alias ll='ls -alF' # create command shortcut for current session.
unalias ll # remove alias.
history # show command history; `!42` reruns command 42.
exit 0 # exit shell with success status; `exit 1` for error.
```
### File Linking
```bash 
ln <file> <hardlink> # create hard link (same inode, same data).
ln -s <target> <symlink> # create symbolic link (reference to path).
```
### User Management
```bash
passwd # change password for current user.
sudo passwd <user> # change password for specified user.
su - # switch to root user with root's environment.
su <username> # switch to specified user.
sudo <command> # execute command as root.
sudo -u <user> <command> # execute command as specified user.
sudo useradd -m <username> # create new user with home directory.
sudo userdel -r <username> # delete user and home directory.
```
### System Control
```bash
sudo reboot # restart the system.
sudo shutdown -h now # halt system immediately.
sudo shutdown -r +5 # reboot in 5 minutes.
```
### Advanced Utilities
```bash 
xargs # build and execute command lines from stdin; `cat list.txt | xargs rm` removes files listed.
tee <file> # read from stdin, write to file and stdout; `command | tee log.txt` captures output.
tee -a <file> # append to file instead of overwriting.
basename /path/to/file.txt # strip directory from filename.
basename <file.txt> .txt # also strip suffix.
mktemp # create temporary file; `-d` creates directory.
bc <<< "2^8" # arbitrary precision calculator for math operations.
yes # repeatedly output a string (default 'y'); `yes Y | head -n 5` outputs Y five times.
sleep 5 # delay for 5 seconds; supports `m` for minutes, `h` for hours.
dd if=/dev/zero of=file.bin bs=1M count=10 # create 10MB file (caution: destructive if wrong target).
```

# PowerShell vs Bash Feature Comparison

| **Feature**                | **PowerShell**                                                                 | **Bash**                                   | **Workaround in Bash**                                                                 |
|----------------------------|-------------------------------------------------------------------------------|-------------------------------------------|----------------------------------------------------------------------------------------|
| **Modules**               | Yes – `Import-Module` for structured cmdlets and functions                   | No native module system                  | Use `source` to load reusable scripts or create function libraries in `.sh` files     |
| **Object Pipeline**       | Yes – Pass rich .NET objects between commands                                | No – Passes plain text                   | Use JSON or key-value text; parse with `jq` or `awk` for structured data              |
| **Cross-Platform Cmdlets**| Yes – Consistent cmdlets across OS                                           | No – Commands vary by OS                 | Use POSIX-compliant commands or wrapper scripts for portability                       |
| **Type System**           | Strong typing with .NET types                                               | Weak typing (strings everywhere)         | Validate input manually or use external tools like `bc` for numeric operations        |
| **Error Handling**        | Try/Catch/Finally blocks                                                   | Basic exit codes (`$?`, `$PIPESTATUS`)   | Implement custom error handling with `trap` and conditional checks                    |
| **Package Management**    | Built-in (`Install-Module`, `Find-Module`)                                  | No native package manager for scripts    | Use `apt`, `yum`, or `brew` for system packages; custom script repos for functions    |
| **Remote Management**     | Yes – `Invoke-Command`, `Enter-PSSession`                                   | Limited – SSH only                       | Use SSH + `scp` for remote execution; combine with Ansible for automation             |
| **Integrated Help**       | Yes – `Get-Help` for cmdlets                                                | Limited – `man` pages for commands       | Add comments and `--help` flags in custom scripts                                     |
| **Tab Completion**        | Advanced, context-aware                                                    | Basic filename completion                | Enable `bash-completion` package for improved completion                              |
| **Configuration Profiles**| Yes – `$PROFILE` for startup scripts                                        | Yes – `.bashrc`, `.profile`             | Use `.bashrc` for aliases, functions, and environment variables                       |
