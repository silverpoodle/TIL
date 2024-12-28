# Linux Command Basics

### 1. Standard Files

```shell
표준 입력 (stdin): `0`
표준 출력 (stdout): `1`
표준 에러 (stderr): `2`
```

<br/>

### 2. Redirection

```shell
ls -l > output.txt # redirect output
wc -l < input.txt # redirect input
command 2 > file # error redirection
```

<br/>

### 3. Connecting Commands - Pipe

- output of one command can become the input of another

```shell
ps –ef | grep httpd | wc -l
# output of PS sent to grep
# grep passes search result to wc
# wc takes input and counts line number
```

<br/>

### 4. Basic Commands

```shell
which python # full path of command
su - <name> # switch user account
/ # root dir
. # denotes current dir
.. #dinotes parent dir
~ # home dir
```



<br/>

### 5. File Commands

```shell
cp  fromfile  tofile # Copy from the <fromfile> to the <tofile>
 
mv fromfile  tofile # Move/rename the <fromfile> to the <tofile>

touch sample.txt # Create an empty file

rm sample.txt # Remove the file named “sample.txt”
rm –r somedir
# -r: recursively, remove all files and directories contained in the <somedir>

mkdir newdir # Make a new directory called <newdir>

rmdir   olddir # Remove directories if they are empty
```

<br/>

```shell
ln –s /path/file /path/symlink
# create a new symbolic link(soft link), will fail if symlink exists already
```

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241022001929680.png?raw=true" alt="image-20240218203439687" style="zoom:50%;" />

<br/>

```shell
cat sample.txt # concatenate files and print on the standard output
cat  sample1.txt  sample2.txt  >  sample.txt
# read the contents of sample1.txt and sample2.txt and write the combined text to the file  sample.txt


more sample.txt # view a text file one page at a time, press spacebar to go to the next page

less sample.txt # similar to more, but which allows backward  movement in the file as well as forward movement
 f : forward, b:backword, q:quit
 j, k : scroll by one line
 / : search for text
 
head  sample.txt # displays the first 10 lines of a file
head -n sample.txt # display the first n lines

tail  sample.txt # Display the last 10 lines of a file
tail -n sample.txt # display the last n lines of the file
tail –f /var/log/syslog # view a growing log file in real time and see only the newer contents (-f: follow)

ls # see what files are in a directory
 -a: display both regular and hidden files 
 –l: get more information about the files(long format)
```

<br/>

```shell
find # Search for files in a directory

# searches for files named "readwrite.txt" within the current directory and its subdirectories
$ find  .  -name  “readwrite.txt”

# search for files with names that start with the word "read" followed by any sequence of characters
$ find  /home/ec2-user  -name  “read*”

# search for files with names that start with “hello" followed by a single character, and ends with ".txt"
$ find  .  -name  “hello?.txt”

# searches for files with names that start with a digit and end with ".log"
$ find  /home/ec2-user/  -name  “[0-9]*.log”
```

<br/>

```shell
chmod a+x filename # assigns execute privilege to user, group and others
chmod u-rx filename # Removes read and execute permission for the user
chmod 664 filename
```

<br/>

```shell
grep [option] pattern [file...] # search for specific patterns and print lines that match patterns

# search for "example" within a file named “file.txt”
$ grep example file.txt

# Show line number while displaying the output:  -n
$ grep -rn “hello” .

# Case insensitive search using grep -i
$ grep -ir hello 

# Match regular expression in files: two too
$ grep –r "t[wo]o“ .

```

<br/>

### 6. Compress & Decompress

```shell
# Compress
tar -czvf   archive.tar.gz  /path/directory-or-file
	-c: Create an archive
	-z: Compress the archive with gzip
	-v: Display progress in the terminal while creating the archive, also known as “verbose” mode 
	-f: Allows you to specify the filename of the archive

# Decompress
tar  -xzvf  archive.tar.gz

```

<br/>

### 7. Download files

```shell
wget <url>
```

<br/>

### 8. User Environment setup

```shell
.bash_profile
# executed when a user logs into the system
# configures initial settings for a user's login session

.bashrc
```

