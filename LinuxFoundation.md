#Linux Foundation:

####Basic Operations:
```
Relative pathname: .(present directory)   ..(parent directory)   ~(home directory)
cd // change to home directory
cd .. // change to upper directory
cd - // change to previous directory
cd /  // change to root directory
pwd // present working directory
cat
echo
ls // list the contents in pwd
ls -a // list all files including hidden files and folders
tree // display a tree view of the filesystem
tree -d // display a tree view for the current directory
man
exit
login: ssh username@remote-server.com // secure shell(SSH)

```

####Searching for files
```
locate // get the directory of a file
updatedb
wildcard: ? // match any single character
          * // match any string of characters
          [set] // matches any character in the set of characters
          [!set] // matches any character not in the set of characters
find // list all files in the current and all of its subdirectories.
find -type (f //regular file, d // directory, I // symbolic link)
find -name (files with certain pattern)
find -iname (ignore the case of file names)
find -name "*.md" -exec rm {} ';' // find and remove all of files with ".md"
find -ctime 3
find -atime
find -mtime
find -size +10M  // + means greater, - means less, without + or - means exact number
find / // find everything from root directory
grep

```

####Working with files
```
cat // view the file without scroll-back
tac // look at the file backwards, starting with the last line
less // view the file with scroll-back
tail // print last 10 lines by default
head // print first 10 lines by default


mkdir // create a directory
touch // used to set or update the access, change, and modify times of files.
touch <filename> // create an empty file

mv // rename a file or folder
rm <filename> // remove a file
rm -f <filename> // forcefully remove a file
rm -i <filename> // interactively remove a file
rmdir // only remove an empty dirctory
rm -rf // forcefully remove a directory recursively

sudo apt-cache search <software_name>
sudo apt-get install <software_name>
sudo apt-get remove <software_name>
sudo apt-get upgrade <software_name>
```

####Comparing files and file types
```
diff <filename1> <filename2>
diff -c // provides a listing of differences that include 3 lines of context before and after the lines differing in content
diff -i // ignore the case of letters
diff -w // ignore differences in spaces and tabs (white space)
diff -r // used to recursively compare subdirectories as well as the current directory
diff3 // comparing three files at once

file <filename or folder> // determin type of files
```

####Backing up and compressing data
```
cp file1 file2// can only copy files to and from destinations on the local machine
cp -r dir1 dir2 // copy dirctory 1 to directory2
rsync // can also copy files from one machine to another.
rsync -r project-x archive-machine:archives/project-x

gzip * // compress all files in the current directory; each file is compresssed and renamed with a .gz extension
gzip -r projectX // compress all files in the projectX directory along with all files in all of the directories under projectX
gunzip fool // De-compress foo found in the file foo.gz. under the hood, gunzip command is actually the same as gzip -d

bzip2 *
bunzip2 *.bz2 // the same as bzip2 -d

xz *
xz foo
xz -dkbar.xz
xy -dcf a.txt b.txt.xz > abcd.txt
xz -d *.xz

zip backup *
zip -r back.zip ~
unzip backup.zip

tar scf mydir.tar
tar zcvf mydir.tar.gz mydir
tar jcvf mydir.tar.bz2 mydir
tar Jcvf mydir.tar.bz2 mydir
tar xvf mydir.tar.gz

disk-to-disk copying

```

####User Environment
```
who // list current logged-on users
who -a // list all information
whoami // to identify the current user

sudo useradd turkey
id // list current user information

// adding and removing group
sudo /usr/sbin/groupadd newGroup
sudo /usr/sbin/groupdel groupName

groups user // check user group
sudo /usr/sbin/usermod -G groupName user // add user to group

//view current set environment variables
set
env
export

//setting environment variables
echo $SHELL // show the value of a specific varible
export VARIABLE=value (or VARIABLE = value; export VARIABLE) // export a new variable value
//add a variable permanently
1. edit ~/.bashrc and add the line export Variable=value
2. type source ~/.bashrc or bash

//PATH variable
export PATH=$HOME/bin:$PATH

//Keyboard shortcut
ctrl + L //clears the screen
ctrl + D // exits the current shell
ctrl + Z // puts the current process into suspended background
ctrl + C // kills the current process
ctrl + H // works the same as backspace
ctrl + A // goes to the beginning of the line
ctrl + W // deletes the word before the cursor
ctrl + U // delets from beginning of line to cursor position
ctrl + E // goes to the end of the line
TAB // auto-completes files, directories, and binaries


// file permissions
chown // Used to change user ownership of a file or directory
chgrp // used to change group ownership
chmod // used to change the permissions on the file which can be done separately for owner, group and the rest of the world.

rwx: rwx : rwx // read, write, and execute
u:    g:    o // user, group, and other

chmod o+w, o-r test.java // add write to other; remove r from other
ls -l <fileName> // check permission privilege; information of fileName with long version.

4 read permission, 2 writer permission, 1 execution permission
chmod 777 test.java

sudo chown root test.java
sudo chgrp dev test.java
```

####Text Editors
```
//method1: create myfile
cat <<EOF > myfile
line one
line two
line three
EOF

//method2
echo lineone > myfile
echo linetwo >> myfile
echo linethree >> myfile


//vim
i // insert mode
: // line command mode

vi myfile // start the vi and edit the myfile
vi -r myfile// start the vi and edit myfile in recovery mode from a system crash.
:r file2 // read in file2 and insert at current position
:w //writer to file
:w myfile // write out the file to myfile
:w! file2 //overwrite file2
:x  or :wq // exit vi and write out modified file
:q // quit vi
:q! //quit vi even though modifications have not been saved

```

####Security principles
```
last // shows the last time each user logged into the system, which can be used to hlep identify potentially inactive accounts which are candidates for system removal

useradd <userName>
passwd <userName>

```

####Networking
```
hostname // view system's host name
ping // check whether a host is online
host google.com // check google.com website information
nslookup google.com // 
dig google.com
ping <hostname>
route -n // show current routing table
route add -net address // add static route
route del -net address // delete static route
traceroute <domain> // inspect the route which the data packet takes to reach the destination host which makes it quire useful for troubleshooting network delays and errors.

ethtool // queries network interfaces and can also set various parameters such as the speed
netstat // displays all active connections and routing tables. Useful for monitoring performance and troubleshooting
nmap // scan open ports on a network. Important for security analysis
tctdump // dumps network traffic for analysis
iptraf // monitors network traffic in text mode

curl google.com // read a cul
curl -o saved.html google.com // save google.com to saved.html

ssh <remotesystem>
scp <localFile> <user@remotesystem>:/home/user/
```

####Manipulating Text
```
cat file1 file2 // concatenate multiple files and display the output
cat file1 file2 > newfile // combine multiple files and save the out into a new file
cat file >> existingFile // Append a file to the end of an existing file
cat > file // any subsequent lines typed will go into the file until ctrl-D is typed
cat >> file // any subsequent lines are appended to the file until ctrl-D is typed

tac //prints the lines of a file in reverse order.


echo string > newFile // the specified string is placed in a new file
echo string >> existingFile // the specified string is appended to the end of an already existing file
echo $variable // the contents of the specified environment variable are displayed


sed -e command <filename> // specify editing commands at the command line, operate on file and put the output on standard out
sed -f scripfile <fileName> // specify a scriptfiloe containing sed commands, operate on file and put output on standard out.


sort <filename> // sort the lines in the specified file
cat file1 file2 | sort // append the two files, then sort the lines and display the output on the terminal
sort -f <filename> // sort the lines in reverse order

//uniq is used to remove duplicate lines in a text file and is useful for simplifying text display.

sort file1 file2 | uniq > file3 // To remove duplicate entries from some files
sort -u file1 file2 > file3 // equivalent

paste file1 file2 // combine each line
paste -d ':' file1 file2 // combine each line and seperate with  delimiter

join file1 file2 // combine two files on a common field

// regular expression
. // any single character
a|z // match a or z
$ // match end of string
* // match preceding item 0 or more times
a.. // match azy
b.|j. // mathch both br and ju
..$ // match og
l.* // match lazy dog
l.*y // match lazy
the.* // match the whole sentence

grep [pattern] <filename> // search for a pattern in a file and print all matching lines
grep -v [pattern] <filename> // print all lines that do not match the pattern
grep [0-9] <filename> // print the lines that contain the numbers 0 through 9
grep -C 3 [pattern] <filename> // print context of lines (specified number of lines above and below the patter) for matching the pattern. Here the number of lines is specified as 3.

// tee takes the output from any command, and while sending it to standard output, it also saves it to a file.
ls -l | tee newFile // list the contents of a directory on the screen and save the output to a file

wc -l filename // (word count) display the number of lines
wc -c filename // display the number of bytes
wc -w filename // display the number of words

//cut is used for manipulating column-base files and is designed to extract specific columns.
ls -l | cut -d" " -f3 // display the third column delimited by a blank space

// less is used to view large file. Because it does not load the whole file into memory.
less <filename> //
cat <filename> | less 
head -n 5 <filename> // only read the first 5 lines of file
tail -n 15 <filename> // only read the last 15 lines of file
tail -f <filename> // to continue monitor new output in a growing log file

//strings is used to extract all printable character strings found in the file or files given as arguments. It is useful in locating human readable content embedded in binary files: for text files one can just juse grep

strings filename | grep my_string // search for the string my_string in a spreadsheet

zcat compressed-file.txt.gz // view a compressed file
zless <filename>.gz // to page through a compressed file
zmore <filename>.gz // to page through a compressed file
zgrep -i less test-file.txt.gz // to search inside a compressed file
zdiff file1.txt.gz file2.txt.gz // to compare two compress files
```

####Scripts
```
#!/bin/bash

/usr/bin/perl
/bin/bash
/bin/csh
/usr/bin/python
/bin/sh


// bash scripts
# //comment. However, \# or #! is used as starting a script
\ // used at the end of a line to indicate continuation on the next line
; // used to interpret what follows as a new command
$ // indicates that follows is a variable

//example 1
#!/bin/bash
echo "Hello, please enter your name: "
read sname
echo "welcome " $sname


// split long commands over multiple line
scp abc@server1.linux.com:\
/var/ftp/pub/userdata/read \
abc@server2.linux.com:\
/opt/oradal/master/abc/
```

Putting multiple commands on a single line
```
$make ;make install; make clean // three commands will all execute even if the ones preceding them fail
$ make && make install && make clean // the subsequent commands will abort if one fails. && (and operator)
$cat file1 || cat file2 || cat file3 // or operator

```

Functions
```
function_name() {
    command...
}
```

Build-in shell commands
```
complied applications: rm, ls, df, vi, gzip
bash commands: cd, pwd, echo, read, logout, printf, let, ulimit

```

Command substitution
```
By enclosing the inner command with backticks(')
By enclosing the inner command in $()
```

Script parameters
```
$0 // script name
$1 // First parameter
$2, $3, etc // second, third parameter, etc
$* // all parameters
$# / number of arguments

//example
#!/bin/bash
echo "Hello, please enter your name: "
read sname

echo "welcome " $sname

echo "the script name is : " $0
echo "the first parameter is: " $1
echo "second parameter is : " $2
echo "third parameter is : " $3

//output redirection
file > /tmp/file.txt 

//input redirection
#!/bin/bash
echo "Line Count"
wd -l < /temp/test.txt
```


IF statement
```
// numerical or string comparisons
// return value of a command (0 for success)
// File existence or permissions

// file conditionals
-e file // check file existence
-d file // check if the file is a directory
-f file // check if file is a regular file
-s file // check if file is of non-zero size
-g file // check if file has sgrid set
-u file // check if the file has suid set
-r file // check if the file is readable
-w file // check if the file is writable
-x file // check if the file is executable

// string conditionals
string1 == string2 

// numerical conditionals
-eq //equal to
-ne // not equal to
-gt // greater than
-lt // less than
-ge // greater than or equal to 
-le // less than or equal to




if [condition]
then 
    statements
else 
    statements
fi

//Example: check file existence
#!/bin/bash
file=$1
if [-f $file ]
then
    echo -e "The $file exists"
else 
    echo -e "The $file does not exist"
fi


// Nested if statement
#!/bin/bash
echo "Enter the first number: "
read n1
echo "Enter the second number: "
read n2
echo "Choose calculation: 1 for addition, 2 for subtraction, 3 for multiplication"
read oper

if [ $oper -eq 1 ]
then 
    echo "Addition: " $(($n1 + $n2))
else 
    if [ $oper -eq 2 ]
    then
        echo "Subtraction: " $(($n1 - $n2))
    else
        if [ $oper -eq 3 ]
        then
            echo "Multiplication: " $(($n1 * $n2))
        else 
            echo "Invalid input"
        fi
     fi
fi


//Example: Elif
#!/bin/bash
echo "enter a number: "
read n

if [ $n -eq 100 ]
then 
    echo "Input is 100"
elif [ $n -gt 100 ]
then
    echo "Input is greater than 100"
else 
    echo "Input is less than 100"
fi
```


Arithmetic Expressions
```
expr 8+ 8
echo $(expr 8+8)

echo $((x+1))
let x=(1+2); echo $x
```

String Manipulation
```
[ string1 > string2 ] // compares the sorting order of string1 and string2
[ string1 = string2 ] // compares the characters in string1 with the characters in string2
myLen1 = ${#string1} // save tyhe length of string1 in the variable myLen1
${string1:0:5} // substring of string1; char 0 to 5
${string1#*.} // to extract all characters in a string after a dot
```


Boolean Expression
```
&& // AND
|| // OR
! // NOT
```

Case Statement
```
case expression in
    patter1) execute commands;;
    patter2) execute commands;;
    patter3) execute commands;;
    * )      execute some default commands or donothing;;
esac


//Example
#!/bin/bash
echo "Enter a letter"
read letter

case "$letter" in
    "a"|"A") echo "you have typed a vowel!" ;;
    "e"|"E") echo "you have typed a vowel!" ;;
    "i"|"I") echo "you have typed a vowel!" ;;
    "o"|"O") echo "you have typed a vowel!" ;;
    "u"|"U") echo "you have typed a vowel!" ;;
    * )      echo "you have types a consonant !";;
esac
exit 0
```

Looping Constructs
```
for
while
until

//For Loop
for variable-name in list
do
    commands
done


//While Loop
while [ condition-is-true]
do
    commands
done

//Until Loop
until [ condition-is-false]
do
    commands
done


//Example
#!/bin/bash

echo "Beginning for loop"
sum=0
for i in 1 2 3 4
do
    sum=$(($sum+$i))
done
echo "The sum of $i numbers if: $sum"
echo "Ending for loop"


echo "Beginning while loop"
no=5
fact=1
i=1
while [ $i -le $no ]
do
    fact=$(($fact * $i))
    i=$(($i + 1))
done
echo "the factorial of $no is $fact"
echo "Ending while loop"


echo "Beginning until loop"
echo "Number"
mn=1
mx=10
until [ $mn -gt $mx ]
do
    echo "$mn"
    mn=$(($mn + 2))
done
echo "the factorial of $no is $fact"
echo "Ending until loop"

```

Debugging
```
bash -x ./script_file 
// debug mode
//1. it traces and prefixes each command with the + character
//2. it displays each command before executingit
//3. Partially debug
set -x # turn on debugging
...
set +x # turn off debugging

//example
bash sample.sh > error.txt
```


```
TEMP=$(mktemp /tmp/tempfile.XXXXXXX) // to create a temporary file
TEMPDIR=$(mktemp -d /tmp/tempdir.XXXX) // to create a temporary directory
$fine / > /dev/null //Discarding output with /dev/null
$RANDOM // generate a random number
```

####Process
```
A process is simply an instance of one or more related tasks(threads) executing on your computer

interactive processes // bash, firefox, top
Batch Process // updatedb
Daemons // httpd, sinetd, sshd
Threads // gnome-terminal, fireFox
Kernal Threads // kswapdo, migtration, ksoftirqd


PID // unique process ID number
PPID // process (parent) that started this process
TID // Thread ID number. This is the same as the PID for single-threaded processes. For a multi-threaded process, each thread shares the same PID but has a unique TID.


UID // user ID
RUID // real user ID
EUID // effective UID

RGID // real group ID
EGID // effective group ID


ps // provides information about currently running processes, keyed by PID
ps -u // display information of processes for a specified username
ps -ef // displays all the processes in the system in full detail
ps -eLf // goes one step further and displays on line of information for every thread.
```



##Complete commands
```
// Go to the sudo command

sudo su
```

```
An A-Z Index of the Bash command line for Linux.

  alias    Create an alias •
  apropos  Search Help manual pages (man -k)
  apt-get  Search for and install software packages (Debian/Ubuntu)
  aptitude Search for and install software packages (Debian/Ubuntu)
  aspell   Spell Checker
  awk      Find and Replace text, database sort/validate/index
b
  basename Strip directory and suffix from filenames
  bash     GNU Bourne-Again SHell 
  bc       Arbitrary precision calculator language 
  bg       Send to background
  break    Exit from a loop •
  builtin  Run a shell builtin
  bzip2    Compress or decompress named file(s)
c
  cal      Display a calendar
  case     Conditionally perform a command
  cat      Concatenate and print (display) the content of files
  cd       Change Directory
  cfdisk   Partition table manipulator for Linux
  chgrp    Change group ownership
  chmod    Change access permissions
  chown    Change file owner and group
  chroot   Run a command with a different root directory
  chkconfig System services (runlevel)
  cksum    Print CRC checksum and byte counts
  clear    Clear terminal screen
  cmp      Compare two files
  comm     Compare two sorted files line by line
  command  Run a command - ignoring shell functions •
  continue Resume the next iteration of a loop •
  cp       Copy one or more files to another location
  cron     Daemon to execute scheduled commands
  crontab  Schedule a command to run at a later time
  csplit   Split a file into context-determined pieces
  cut      Divide a file into several parts
d
  date     Display or change the date & time
  dc       Desk Calculator
  dd       Convert and copy a file, write disk headers, boot records
  ddrescue Data recovery tool
  declare  Declare variables and give them attributes •
  df       Display free disk space
  diff     Display the differences between two files
  diff3    Show differences among three files
  dig      DNS lookup
  dir      Briefly list directory contents
  dircolors Colour setup for `ls'
  dirname  Convert a full pathname to just a path
  dirs     Display list of remembered directories
  dmesg    Print kernel & driver messages 
  du       Estimate file space usage
e
  echo     Display message on screen •
  egrep    Search file(s) for lines that match an extended expression
  eject    Eject removable media
  enable   Enable and disable builtin shell commands •
  env      Environment variables
  ethtool  Ethernet card settings
  eval     Evaluate several commands/arguments
  exec     Execute a command
  exit     Exit the shell
  expect   Automate arbitrary applications accessed over a terminal
  expand   Convert tabs to spaces
  export   Set an environment variable
  expr     Evaluate expressions
f
  false    Do nothing, unsuccessfully
  fdformat Low-level format a floppy disk
  fdisk    Partition table manipulator for Linux
  fg       Send job to foreground 
  fgrep    Search file(s) for lines that match a fixed string
  file     Determine file type
  find     Search for files that meet a desired criteria
  fmt      Reformat paragraph text
  fold     Wrap text to fit a specified width.
  for      Expand words, and execute commands
  format   Format disks or tapes
  free     Display memory usage
  fsck     File system consistency check and repair
  ftp      File Transfer Protocol
  function Define Function Macros
  fuser    Identify/kill the process that is accessing a file
g
  gawk     Find and Replace text within file(s)
  getopts  Parse positional parameters
  grep     Search file(s) for lines that match a given pattern
  groupadd Add a user security group
  groupdel Delete a group
  groupmod Modify a group
  groups   Print group names a user is in
  gzip     Compress or decompress named file(s)
h
  hash     Remember the full pathname of a name argument
  head     Output the first part of file(s)
  help     Display help for a built-in command •
  history  Command History
  hostname Print or set system name
i
  iconv    Convert the character set of a file
  id       Print user and group id's
  if       Conditionally perform a command
  ifconfig Configure a network interface
  ifdown   Stop a network interface 
  ifup     Start a network interface up
  import   Capture an X server screen and save the image to file
  install  Copy files and set attributes
j
  jobs     List active jobs •
  join     Join lines on a common field
k
  kill     Stop a process from running
  killall  Kill processes by name
l
  less     Display output one screen at a time
  let      Perform arithmetic on shell variables •
  link     Create a link to a file 
  ln       Create a symbolic link to a file
  local    Create variables •
  locate   Find files
  logname  Print current login name
  logout   Exit a login shell •
  look     Display lines beginning with a given string
  lpc      Line printer control program
  lpr      Off line print
  lprint   Print a file
  lprintd  Abort a print job
  lprintq  List the print queue
  lprm     Remove jobs from the print queue
  ls       List information about file(s)
  lsof     List open files
m
  make     Recompile a group of programs
  man      Help manual
  mkdir    Create new folder(s)
  mkfifo   Make FIFOs (named pipes)
  mkisofs  Create an hybrid ISO9660/JOLIET/HFS filesystem
  mknod    Make block or character special files
  more     Display output one screen at a time
  most     Browse or page through a text file
  mount    Mount a file system
  mtools   Manipulate MS-DOS files
  mtr      Network diagnostics (traceroute/ping)
  mv       Move or rename files or directories
  mmv      Mass Move and rename (files)
n
  netstat  Networking information
  nice     Set the priority of a command or job
  nl       Number lines and write files
  nohup    Run a command immune to hangups
  notify-send  Send desktop notifications
  nslookup Query Internet name servers interactively
o
  open     Open a file in its default application
  op       Operator access 
p
  passwd   Modify a user password
  paste    Merge lines of files
  pathchk  Check file name portability
  ping     Test a network connection
  pkill    Stop processes from running
  popd     Restore the previous value of the current directory
  pr       Prepare files for printing
  printcap Printer capability database
  printenv Print environment variables
  printf   Format and print data •
  ps       Process status
  pushd    Save and then change the current directory
  pv       Monitor the progress of data through a pipe 
  pwd      Print Working Directory
q
  quota    Display disk usage and limits
  quotacheck Scan a file system for disk usage
  quotactl Set disk quotas
r
  ram      ram disk device
  rcp      Copy files between two machines
  read     Read a line from standard input •
  readarray Read from stdin into an array variable •
  readonly Mark variables/functions as readonly
  reboot   Reboot the system
  rename   Rename files
  renice   Alter priority of running processes 
  remsync  Synchronize remote files via email
  return   Exit a shell function
  rev      Reverse lines of a file
  rm       Remove files
  rmdir    Remove folder(s)
  rsync    Remote file copy (Synchronize file trees)
s
  screen   Multiplex terminal, run remote shells via ssh
  scp      Secure copy (remote file copy)
  sdiff    Merge two files interactively
  sed      Stream Editor
  select   Accept keyboard input
  seq      Print numeric sequences
  set      Manipulate shell variables and functions
  sftp     Secure File Transfer Program
  shift    Shift positional parameters
  shopt    Shell Options
  shutdown Shutdown or restart linux
  sleep    Delay for a specified time
  slocate  Find files
  sort     Sort text files
  source   Run commands from a file '.'
  split    Split a file into fixed-size pieces
  ssh      Secure Shell client (remote login program)
  stat     Display file or file system status 
  strace   Trace system calls and signals
  su       Substitute user identity
  sudo     Execute a command as another user
  sum      Print a checksum for a file
  suspend  Suspend execution of this shell •
  sync     Synchronize data on disk with memory
t
  tail     Output the last part of file
  tar      Store, list or extract files in an archive
  tee      Redirect output to multiple files
  test     Evaluate a conditional expression
  time     Measure Program running time
  timeout  Run a command with a time limit
  times    User and system times
  touch    Change file timestamps
  top      List processes running on the system
  traceroute Trace Route to Host
  trap     Run a command when a signal is set(bourne)
  tr       Translate, squeeze, and/or delete characters
  true     Do nothing, successfully
  tsort    Topological sort
  tty      Print filename of terminal on stdin
  type     Describe a command •
u
  ulimit   Limit user resources •
  umask    Users file creation mask
  umount   Unmount a device
  unalias  Remove an alias •
  uname    Print system information
  unexpand Convert spaces to tabs
  uniq     Uniquify files
  units    Convert units from one scale to another
  unset    Remove variable or function names
  unshar   Unpack shell archive scripts
  until    Execute commands (until error)
  uptime   Show uptime
  useradd  Create new user account
  userdel  Delete a user account
  usermod  Modify user account
  users    List users currently logged in
  uuencode Encode a binary file 
  uudecode Decode a file created by uuencode
v
  v        Verbosely list directory contents (`ls -l -b')
  vdir     Verbosely list directory contents (`ls -l -b')
  vi       Text Editor
  vmstat   Report virtual memory statistics
w
  wait     Wait for a process to complete •
  watch    Execute/display a program periodically
  wc       Print byte, word, and line counts
  whereis  Search the user's $path, man pages and source files for a program
  which    Search the user's $path for a program file
  while    Execute commands
  who      Print all usernames currently logged in
  whoami   Print the current user id and name (`id -un')
  wget     Retrieve web pages or files via HTTP, HTTPS or FTP
  write    Send a message to another user 
x
  xargs    Execute utility, passing constructed argument list(s)
  xdg-open Open a file or URL in the user's preferred application.
  yes      Print a string until interrupted
  zip      Package and compress (archive) files.
  .        Run a command script in the current shell
  !!       Run the last command again
  ###      Comment / Remark
```
