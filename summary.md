# Summary of edX Course: Introduction to Linux

## Table of Contents

* Introduction: What's this summary about ?

* 1. Manipulating Files and Text 
   * a) File Operations: Command Line Operations - Keyboard Shortcuts on the Command Line - Display and Searching for Files - Compressing Data and Backing Up - Creating Files Witout Using an Editor - File Ownership
   * b) Text Editors: General Editors - Focus on VIM 
   * c) Manipulating Text: Environment Variables - Concatenate - Edit/Extract contents - File manipulation programs - Regular Expressions and Search Patterns - Miscellaneous Text Utilities
   
* 2. The Bash Shell and Scripting
   * a) Syntax: Splitting Long Commands Over Multiple Lines - Putting Multiple Commands on a Single Line - Script Parameters - Functions
   * b) Constructs: The if Statement - The elif Statement - The case Statement - Testing for Files - Looping Constructs - Boolean Expressions - Numerical Tests - Arithmetic Expressions - String Manipulation
   * c) Debugging: Syntax - Input/Output
   
* 3. Some More Knowledges
   * a) The File System Hierarchy
   * b) Processes: Priority - Load averages - Background and Foreground Processes - Scheduling Future Processes or pause them
   * c) Network Operations: Networking Configuration and Tools - Dowloading and Getting Information From the Net - Transferring Files
   
* Conclusion: For those who want to go deeper...
 
## Introduction

Hello World, I did a training course (**edX: Introduction to Linux**) and my job is to do a **short summary** of it. This course has 18 chapters, so of course I won't cover all details/every commands learned. The aim is to give you **first the main topics** and **second what I learned/surprised me the most**. I hope you enjoy it ! 

## 1. Manipulating Files and Text 

### a) File Operations

* Command Line Operations:

 Command | Usage
 --- | ---
 which *-arg* | Locationg Applications in the list of *$PATH*
 whereis *-arg* | Locationg Applications in the list of *$PATH* + packages
 tree | List contents of directories recursively in a tree-like format
 ln *file1* *file2* | Create a Hard Link *file2* of *file1*
 ln -s *file1* *file2* | Create a Soft (Symbolic) Link *file2* to *file1*
 pushd *PATH* | Change the directory instead of `cd` - this pushes the directory onto a list
 popd | Send you back to those directories (of the previous list) walking in reverse order
 dirs | Display the previous list of directories

* Keyboard Shortcuts on the Command Line:

 Keyboard shortcut | Task
 --- | ---
 CTRL-l | Clears the screen
 CTRL-d | Exits the current shell
 CTRL-z | Puts the current process into suspended background
 CTRL-c | Kills the current process
 CTRL-h | Works the same as backspace
 CTRL-a | Goes to the beginning of the line
 CTRL-w | Deletes the word before the cursor
 CTRL-u | Deletes from beginnning of line to cursor position
 CTRL-e | Goes to the end of the line

* Display and Searching for Files:

 Command | Usage
 --- | ---
 tac | Display the file backwards (starting with the last line) - opposite of `cat`
 less | Display large files with scroll-back (paping program) - use **/** to search for a  pattern in the forward direction and **?** for a pattern in the backward direction
 head | Display the first 10 lines of a file (by default) - opposite of `tail`
 diff | Compare files and directories
 find | Search for a file in the **file system** (pros: with the -exec option, one can run a command on the founded files)
 locate | Search for a file in the **database** (pros: speed)

 When searching a filename containing specific characters, one can use **wilddards**:

 Wildcard | Result
 --- | ---
 ? | Matches any single character
 \* | matches any string of characters
 *[set]* | Matches any character in the set of characters, for example [adf] will match any  occurrence of a, d or f - use *`[!set]`* for matching any character not in the set of characters

* Compressing Data and Backing Up:

   * Compressing:
   
    Command | Usage
    --- | ---
    gzip | The most frequently used Linux compression utility
    bzip2 | Produces files significantly smaller than those produced by `gzip`
    xz | The most space-efficient compression utility used in Linux
    zip | Often required to examine and decompress archives from other operating systems
    tar | Often used to group files in an archive and then compress the whole archive at once
    dd | Makes large exact copies -even of entire disk partitions- efficiently (Use with precaution)

   * Manipulate compressed Data:

    Command | Usage
    --- | ---
    zcat | To view a compressed file
    zless | To page through a compressed file
    zgrep | To search inside a compressed file
    ziff | To compare compressed files

* Creating Files Witout Using an Editor:
   * with `echo`:
    ```bash
    $ echo line one > myfile
    $ echo line two >> myfile
    $ echo line three >> myfile
     ```
   * with `cat`:
    ```bash
    $ cat << EOF > myfile
    > line one
    > line two
    > line three
    > EOF
    $
    ```

* File Ownership:

   * Change ownership/permissions:

    Command | Usage
    --- | ---
    chown | Change user ownership of a file or directory
    chgrp | Change group ownership
    chmod | Change the permissions (read **r**, write **w**, and execute **x**) on the file for  the 3 categories in order: owner(user **u**), group (**g**) and the rest (other **o**)

   * *chmod* algorithm:
    There're 3 digits, one for each category. One digit is the some of:
     * 4 if read permission is desired
     * 2 if write permission is desired
     * 1 if execute permission is desired

    **chmod** use case: `chmod 755 somefile` .

### b) Text Editors

* General Editors:

![general text editors][text_editors]

* Focus on **V**i **IM**mproved (*Programming Editor*):

 Mode | Key | Feature | Examples
 --- | --- | --- | ---
 Command | *Esc* | Default mode; each key is an editor command | Moving throughout the file - Copy/Paste
 Insert | *i* | Insert text into a file | Add a word
 Line |*:*  | Execute external command within *vim* | Save the file - Exiting

 ![vi basic commands][vi_commands]

### c) Manipulating Text

* Environment Variables:

   * Some environment variables:

    Variable | Content
    --- | ---
    HOME | Path to your home directory
    PATH | Ordered list of directories containing your programs/softwares
    SHELL | User's default command shell
    PS1 | Character string displayed as the prompt on the command line

   * To display the content of a variable, type `echo $VARIABLE`, as *VARIABLE* is the name of  the environment variable, *$VARIABLE* is its content and *echo* is printing it in the default stdout.

   * To create an **alias** permanently (shortcut for a command):
    Add the line: `alias shortcut_name='command'` in the `~/.bashrc` file.
    
   * To add a variable permanently:
    Add the line `export VARIABLE=value` in the `~/.bashrc` file.

* Concatenate:

 Command | Usage
 --- | ---
 cat *file1* *file2* > *newfile* | Concatenate the two files - i.e.: the entire content of the first file is followed by that of the second file - and save the output into a new file
 cat *file* >> *existingfile* | Append a file to the end of an existing file
 cat > *newfile* | Any subsequent lines typed will go into the *newfile*; until CTRL-d is typed
 cat >> *existingfile* | Any subsequent lines typed are appended to the *existingfile*; until CTRL-d is typed

* Edit/Extract contents:
   * sed (**s**tream **ed**itor): Filter text and datas substitution.
   * awk (**A**ho, **W**einberger, **K**ernighan): Interpreted programming language, typically used as a data extraction and reporting tool.

 Command | Use case
 --- | ---
 sed s/pattern/replace_string/ file | Substitute first string occurrence in every line
 awk -F: '{ print $1 }' file | Print first field (column) of every line, separated by a space 

* File manipulation programs:

 Command | Usage
 --- | ---
 sort | Rearrange the lines of a text file, in ascending or descending order
 uniq | Removes  duplicate consecutive lines in a sorted text file
 paste | Join files horizontally (**parallel merging**)
 join | Same as `paste` command but on a common field for joining
 split | Break up a file into equal-sized segments for easier viewing and manipulation

* Regular Expressions and Search Patterns:

 **Regex**: text strings used for matching a specific pattern , or to search for a specific location, such as the start or end of a line or a word. Regular expressions can contain both normal characters or so-called meta-characters, such as * and $.

 Search Patterns | Usage
 --- | ---
 . | Match any single character
 \* | Match preceding item 0 or more times 
 ^ | Match beginning of string
 $ | Match end of string
 a\|z | Match a or z

 grep *pattern* *filename* : Search for a pattern in a file and print all matching lines. It can be used with regular expressions. 

* Miscellaneous Text Utilities:

 Command | Usage
 --- | ---
 tr *options* *set1* *set2* | Translates specified characters into other characters or delete them
 tee | Takes the output from a command and both sends it to standard output and saves it to a file
 wc (**w**ord **c**ount) | Counts the number of lines, words, and characters in a file or list of files
 cut | Extract specific columns from column-based files

## 2. The Bash Shell and Scripting

### a) Syntax

* Splitting Long Commands Over Multiple Lines:

 Character | Description
 --- | ---
 \ | Used at the end of a line to indicate continuation on to the next line

* Putting Multiple Commands on a Single Line:

 Character | Description
 --- | ---
 && | Proceed commands until one fails
 \|\| | Proceed commands until one succeeds
 ; | Proceed commands regardless of the precedent error status

* Script Parameters:

 Parameter | Meaning
 --- | ---
 $0 | Script name
 $1,$2,...  | First parameter,second parameter,...
 $* | All parameters
 $# | Number of arguments

* Functions:
 ```bash
 function_name () {
 	command
 }
 ```

### b) Constructs

* The if Statement:
 ```bash
 if [ condition ]
 then
	 statements
 else
	 statements
 fi
 ```
* The elif Statement:
 ```bash
 if [ condition ] ; then
 	statements 
 elif [ somothertest ] ; then
 	statements 
 fi
 ```
* The case Statement:
 ```bash
 case expression in
 	pattern1) execute commands;;
 	pattern2) execute commands;;
 	pattern3) execute commands;;
 	pattern4) execute commands;;
 	* )       execute some default commands or nothing;;
 esac
 ```
* Testing for Files:

 Condition | Checks if the file ...
 --- | ---
 -e file | exists
 -d file | is a directory
 -f file | is a regular file (i.e. not a symbolic link, device node, directory,etc.)
 -s file | is of non-zero size
 -g file | has **sgid** set
 -u file | has **suid** set
 -r file | is readable
 -w file | is writable
 -x file | is executable

* Looping Constructs:

   * The for Loop (operates on each element of a list of items):
 ```bash
 for variable_name in list
 do
 	execute one iteration for each item in the list until the list is finished
 done
 ```
   * The while Loop (repeats a set of statements as long as the control command returns true):
 ```bash
 while [ condition is true ]
 do
 	Commands for execution
 done
 ```
   * The until Loop (repeats a set of statements as long as the control command is false):
 ```bash
 until [ condition is false ]
 do
 	Commands for execution
 done
 ```
* Boolean Expressions:

 Operator | operation | Meaning
 --- | --- | ---
 && | AND | The action will be performed only if both the conditions evaluate to TRUE.
 \|\| | OR | The action will be performed only if any one of the conditions evaluate to TRUE.
 ! | NOT | The action will be performed only if the condition evaluates to FALSE.

* Numerical Tests:

 Operator | Meaning
 --- | ---
 -eq | Equal to
 -ne | Not equal to
 -gt | Greater than
 -lt | Less than
 -ge | Greater than or equal to
 -le | Less than or equal to

* Arithmetic Expressions:
 To evaluate an arithmetic expression, one can use:
   * `expr`
   * `$((...))`
   * `let` 

* String Manipulation:

 Operator | Meaning
 --- | ---
 [[ *string1* > *string2* ]] | Compares the sorting order of *string1* and *string2*.
 [[ *string1* == *string2* ]] | Compares the characters in *string1* with the characters in *string2*
 *myLen*=${#*string1*} | Saves the length of *string1* in the variable *myLen*

### c) Debugging

* Syntax:
   * Run a bash script in debug mode: bash -x ./*script_file*
   * Run only parts of the script in debug mode: 
    ```
    set -x    # turns on debugging
    ...
    set +x    # turns off debugging
    ```

* Input/Output:

 File stream | Description | File Descriptor
 --- | --- | ---
 stdin | Standard Input, by default the keyboard for programs run from the command line | 0
 stdout | Standard Output, by default the terminal for programs run from the command line | 1
 stderr | Standard Error, where output error messages are shown or saved | 2

 Redirection | Use case
 --- | ---
 of error: 2> | *do_something* 2> *error-file*

 Exit Status Codes: 
   * sucess: 0
   * failure: non-zero value
   * display the error value of the last command run: `$?`

## 3. Some More Knowledges

### a) The File system Hierarchy

![file system main directories][file_system]

### b) Processes 

* Priority:
   * Nice (Niceness) value: From -20 to +19, -20 being top priority and +19 lowest priority.
   * To display nice value: `ps -ni`
   * To change nice value: `renice -n New_nicevalue -p PID_number` 
 
* Load averages:
 Amount of utilization the system is under, using 3 numbers (a, b, c): 
   * For the last **minute**, the system has been (a * 100 / X)% utilized on average;
   * For the last **5 minutes**, the system has been (b * 100 / X)% utilized on average;
   * For the last **15 minutes**, the system has been (c * 100 / X)% utilized on average;
 
    Where X stands for the number of CPU cores.

 To display the load averages: `w`, `top`, `uptime` .

* Background and Foreground Processes: 
   * Put a job in background: 
   `command &` 
    or 
    ```bash
    command
    bg
    ```
   * Use `fg` to put in back in foreground. 
   * Use CTRL-Z to suspend a foreground job or CTRL-C to terminate a foreground job.
    Another way for terminating a process: `kill -SIGKILL PID_number` or `kill -9 PID_number`

   * Display the processes in background: `jobs` .
   * Display currently running processes: `ps` (or `pstree`) or `top`( constant real-time updates). 

* Scheduling Future Processes or pause them :
   * `at`
   * `cron`
   * `sleep`

### c) Network Operations

* Networking Configuration and Tools:

   * `ip` is a very powerful program that can do many things. Older (and more specific) utilities such as `ifconfig` and `route` are often used to accomplish similar tasks.
   
   * `ping` is used to check whether or not a machine attached to the network can receive and send data; i.e. it confirms that the remote host is online and is responding. To check the status of the remote host, at the command prompt, type `ping <hostname>`.

   * One can use the `route` utility or the newer `ip route` command to view or change the IP routing table to add, delete, or modify specific (static) routes to specific hosts or networks. 

   * `traceroute` is used to inspect the route which the data packet takes to reach the destination host, which makes it quite useful for troubleshooting network delays and errors. By using `traceroute`, you can isolate connectivity issues between hops, which helps resolve them faster. To print the route taken by the packet to reach the network host, at the command prompt, type `traceroute <address>`.

* Dowloading and Getting Information From the Net:

   * To download multiple files and/or directories, or to perform this action from a command line or a script, use `wget`. Indeed, `wget` is a command line utility that can capably handle the following types of downloads:
     * Large file downloads;
     * Recursive downloads, where a web page refers to other web pages and all are downloaded at once;
     * Password-required downloads;
     * Multiple file downloads.
     
   To download a web page, you can simply type `wget <url>`, and then you can read the downloaded  page as a local file using a graphical or non-graphical browser.

   * To obtain information about a URL, such as the source code being used, use `curl`. Indeed, `curl` can be used from the command line or a script to read such information. You can read a URL using `curl <URL>`.

* Transferring Files: 

   * FTP clients: Enable you to transfer files with remote computers using the FTP protocol.
    Some command line FTP clients are: `ftp`, `sftp`, `ncftp`, `yafc` (Yet Another FTP Client).
     
   * SSH: Executing Commands Remotely:
    Secure Shell (SSH) is a cryptographic network protocol used for secure data communication. `ssh` is also used for remote services and other secure services between two devices on the network and is very useful for administering systems which are not easily available to physically work on, but to which you have remote access.

   * Copying Files Securely:
    One can also move files securely using Secure Copy (scp) between two networked hosts. `scp` uses the SSH protocol for transferring data.

## Conclusion

This is the end of this summary. It's rather longer than I expected it to be. I guess the reason is because **I learned a more lot** of things than I though (haha). I thank the **Linux Fondation** for this greatful course. But still, some of you would complain, arguing that this summary isn't fully complete. And you're certainely right. However, for every command or concept, if you want to go deeper (and you should !), there are documentations available, like the famous **man pages**, or of course this precise course (**edX Course: Introduction to Linux**) ! As the saying goes: 
> Give a man a fish, and you feed him for a day. Teach a man to fish, and you feed him for a lifetime. 

For that, I think I fulfilled the main goal. I hope you enjoyed this summary ! 

![fisherman metaphor][fisherman]

[text_editors]: images/text_editors.png "Text Editors"
[vi_commands]: images/vi_commands.png "Vi Commands"
[file_system]: images/dirtree.jpg "File System Hierarchy"
[fisherman]: images/fisherman.png "Fisherman Metaphor"
