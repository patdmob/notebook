# Bash

Still a work in progress, hope to have the content complete and well formatted soon!

- [Shortcuts](#shortcuts)
- [Command Search/Help](#command-searchhelp)
- [Basic Commands](#basic-commands)

## Shortcuts

 Command | Description 
 --- | --- 
 Ctrl+L | clear screen  
 Ctrl+C  | stop current command 
 Ctrl+Z  | suspend current command, to resume: fg (foreground) or bg (background )
 Ctrl+D  | log out of current session, similar to exit 
 !!      | repeat previous command

## Command Search/Help

 Command | Description 
 --- | --- 
help \<command> |  bash internal command documentation
\<command> --help | help documentation from command (help option on Win Git Bash)
man \<topic> |  displays the [manuel pages](http://man7.org/linux/man-pages/) (q to quit)
info \<topic> |  GNU project's preferred alternative to man (q to quit, h for help)
whatis \<command> 	| displays a short description of a command
apropos \<keyword> | search the whatis database for strings
which \<command>	| searches for the location of a command 
history \<number>	| prints a list of commands you've typed (stores 1000 unique commands)

### Examples

```bash
help echo        # Prints help documentation for internal command 'echo'
man echo         # Displays manual page for command 'echo' in 'less'
whatis echo      # Result: echo(1)  - write arguments to the standard output
which bash       # Result: /bin/bash
history 2        # Prints the last two commands
```

## Basic Commands

Some basic commands with common syntax. For more options see the command man or info pages.

 Command | Description 
 --- | --- 
ls  \<dir>   | list storage (-l list)(-a all) 
cd \<path>    | change directory
alias   | create an alias for a command or script
pushd  \<path> | saves current location in stack and cd to specified
popd   | cd to top value in pushd stack
locate \<pattern> | gives a list of paths for a given pattern
mkdir \<directory> | make directories 
rmdir \<directory> | remove empty directories
touch \<file> | creates an empty file or changes access and modification times
cp    \<sourcefile> \<path> | copy file 
mv   \<sourcefile> \<path \| name> | move or rename a file
rm   \<file> | remove files and directories (-r recursive) (-f force) (-i interactive)
echo  \<string> | displays a line of text either on standard output or to place in a file
head  \<file> | displays the first few lines (default 10) of a file or stout
tail \<file> | displays the last few lines (default 10) of a file or stdout 
cat  \<files \| stdin> | concatenate and print files; '-' reads from stdin until EOF ('^D')
open \<source> | opens the file (. for folder)
less  \<file>| used to view files instead of opening the file ('q' quit)('space' page down)
nano \<file> | basic text editor 

### Examples

```bash
ls -al                      # List all contents in current directory
ls ~                        # Show contents of home directory ('~' = home directory alias)
cd Downloads/               # Change current directory to 'Downloads'
cd ..                       # Change to parent directory ('..' = parent, '.' = current directory)
alias -p                    # Prints all defined aliases
alias ls='ls -l'            # Shorthand for: ls -l
touch myfile                # Create an empty file called myfile
touch -t 05231600 myfile    # Sets the timestamp for myfile to 4 p.m., May 23th (05 23 1600).
mkdir sampledir             # Creates 'sampledir' in current directory
rm -rf                      # Forcefully and recursively delete contents from a directory
cat file1 file2 > file3     # Concatenates contents from file1 and file2 into file3
cat file1 - file2           # Prints file1, prints input from stdin until EOF (`^D'), then prints file2
```

## File/Text/Search Manipulation  
 Command | Description 
 --- | --- 
sed | popular stream editor used to filter/substitute text in files and data streams  
awk   | typically used as a data extraction and reporting tool  
sort  | sorts lines (-r for descending) (-k 3 by third field) (-u returns uniq values after sort)  
uniq  | removes duplicate lines from text (requires consecutive duplicates) (-c for count)  
paste | merge lines/columns of a file(s) using -d delimiters  
join  | merge two files with similar columns without repeating the data  
split | breaks a file into 1000 line segments  
cut   | extract specific columns from column-based files   
grep    | print lines matching pattern (-v not match)(-C context above and below)  
strings | extracts all printable content from an argument file list  
tr      | text utility (translate)   
wc 	| word count displays lines, words, and characters (-l lines) (-c bytes) (-w words)  

### Examples

```bash
tr '{}' '()' < inputfile > outputfile           # Translate braces into parenthesis    
echo "This is for testing" | tr [:space:] '\t'	# Translate white-space to tabs    
echo "This   is a    test" | tr -s [:space:]    # Squeeze repetition of characters using -s  
```

## User Related Commands 
 Command | Description 
 --- | --- 
sudo        | enter command as root  
sudo -s     | change to root account (recommended over su)  
su \<user>   | change to \<user> account  
su - \<user> | change to \<user> account and navigate to their home directory  
users 	    | shows active users  
id	    | gives all pertinent information about user account  
whoami	    | returns the current user  
   
## Networking/Transfer/Web Related Commands 
 Command | Description 
 --- | --- 
arp       | address resolution display and control  
whois     | Internet domain name and network number directory service  
dig 	  | dig	Tests DNS workings. A good replacement for host and nslookup.  
ipconfig  | newer utility of ifconfig, may not be installed by default   
ifconfig  | configure network interface parameters  
ping      | send ICMP ECHO_REQUEST packets to network hosts  
netstat   | Displays all active connections and routing tables  
ssh	| secure shell  
sftp	| secure file transfer  
rsync	| efficiently transfer and sync files across computers by checking timestamp and size  
scp	| secure copy  
wget  |
curl  |
  
## Interaction
read \<varname>  - requests input from the user and stores in varname  
  
  
## Bash Scripting
### Header
#!/bin/bash

### Syntax

 Command | Description 
 --- | --- 
\#	| Used to add a comment, except when used as \\#, or as #! when starting a script    
\\	| Used at the end of a line to indicate continuation on to the next line    
;   | commands are executed sequentially, waiting for each to finish executing    
&   | the shell runs the following cmd immediately in the background    
&&  | executes the second command only if the first completes successfully    
\|\|  | executes the second command only if the first fails    
$	| Indicates what follows is an environment variable    
\>	| redirect standard output (stout) to a file    
\>>	| append output to a file if it exists, or > if the file does not exist    
<	| read from a file, formally known as redirect input    
\|    | pipe the standard output of one command into another command's standard input  
\|&   | the stderr and stdout of cmd1 are connected to cmd2 stdin; shorthand for 2>&1 |   
\#!      | shebang used at the top to tell linux where to find the executable    
exit    | used to set the return value; 0 for success, non-zero for failure    
echo $? | used to check the return value after a program has run     
  
### Script Parameters (arguments) 
 Command | Description 
 --- | --- 
$0		| Script name    
$1		| First parameter    
$2, $3, etc.	| Second, third parameter, etc.    
$*		| All parameters    
$#		| Number of arguments    
  
### Command Substitution
No matter the method, the innermost command will be executed in a newly launched shell environment, and the standard output of the shell will be inserted where the command substitution was done.    
\`\<cmd>`     
$(\<cmd>)     
Both of these methods enable command substitution; however, the $( ) method allows command nesting. New scripts should always use of this more modern method.    
ls /lib/modules/$(uname -r)/    
  
### Variables   
environment variables: HOME, PATH, HOST, etc.    
foo=bar		# no space!    
echo $foo    
\>  bar    
By default, the variables created within a script are local. To make them global (environment variables) use export:    
export VAR=value    
VAR=value ; export VAR    
export with no arguments will give a list of all currently exported environment variables    
  
### Functions  
The general syntax of a bash function is:
```bash
function_name () {  
    command...  
}  
```

Function arguments are position based. Within the function, the first argument can be referred to as $1, the second as $2, etc. To call a function, simply type the function name. Functions must be defined before use.

```bash
func1() {  
echo " This message is from function 1"  
}  
func2() {  
echo " This message is from function 2"   
}  
echo "Enter a number, 1 or 2"  
read n  
func$n  
```

### Flow Control
if TEST-COMMANDS; then CONSEQUENT-COMMANDS; fi  
A more general definition is:  

```bash
if [[ condition ]] 	# square brackets are used to delineate the test condition  
then  
    statements  
elif [[ condition ]]  
then  
    statements  
else  
    statements  
fi  

file=$1  
if [ -f file ]		# one set of square brackets will work but two is prefered  
then  
echo -e "The $file exists"  
else  
echo -e "The $file does not exist"  
fi  
```

### Conditional Syntax 
#### Files:  
 Conditional | Description 
 --- | --- 
-e   |	Checks if the file exists  
-d   |	Checks if the file is a directory  
-f   |	Checks if the file is a regular file (i.e., not a symbolic link, device node, directory, etc.)  
-s   |	Checks if the file is of non-zero size  
-g   |	Checks if the file has sgid set  
-u   |	Checks if the file has suid set  
-r   |	Checks if the file is readable  
-w   |	Checks if the file is writable  
-x   |	Checks if the file is executable  

Example:  
```if [[ -f file ]]``` 

#### Numeric: 
 Conditional | Description 
 --- | --- 
-eq	 | Equal to    
-ne	 | Not equal to    
-gt	 | Greater than    
-lt	 | Less than    
-ge	 | Greater than or equal to    
-le	 | Less than or equal to   

Example:  
```if [[ $first -eq 0 ]] && [[ $second -ne 0 ]]```  

#### Boolean:    
 Conditional | Description 
 --- | --- 
&&	|  AND	    
\|\|	|  OR	    
!	|  NOT	    

Example:  
```if [[ $first -eq 0 ]] && [[ $second -ne 0 ]]   ```

#### Strings:   
 Conditional | Description 
 --- | --- 
==	| EQUALS	    

Example:  
```if [ string1 == string2 ] ```

### Arithmetic Expressions:    
Using the var=$((...)) syntax:    
`echo $((x+1))`    
Using the built-in shell command let:    
`let x=( 1 + 2 ); echo $x`  
      

