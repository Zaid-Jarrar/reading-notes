# Practice in Terminal
### The Command Line!

A command line or terminal is a text based interface which one can make changes on the computer and give feedback to what had happened.

How does it work?
It is simple, the user types a command and may then receive a response as feedback.

To get one just follow these instructions:

Reading from [ryanstutorials](https://ryanstutorials.net/linuxtutorial/commandline.php)

> Opening a terminal is fairly easy. I can't tell you exactly how to do it as every system is different but here are a few places to start looking.

> If you're on a Mac then you'll find the program Terminal under Applications -> Utilities. An easy way to get to it is the key combination 'command + space' which will bring up Spotlight, then start typing Terminal and it will soon show up.
If on Linux then you will probably find it in Applications -> System or Applications -> Utilities. Alternatively you may be able to 'right-click' on the desktop and there may be an option 'Open in terminal'.
> If you are on Windows and intend to remotely log into another machine then you will need an SSH client. A rather good one is [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) (free).

---------------------------------------

### Basic Navigation!
- pwd (print working directory) 
It shows the path of your current location. 

- ls (list) 
It shows the items in that directory
however its original format is `ls [options] [location]` 
where [] means they are optional and not required. 

one of the options is a long list which is `-l` for that location. And adding the location  `location` (either the absolute or relative path) to view the contents of that directory without entering it beforehand. 
`➜  ~ ls -l PrepCourse
total 4
drwxr-xr-x 22 zaid zaid 4096 Feb 15 16:32 prep-course-py-01`

- cd Change Directories - ie. move to another directory. **note: cd alone will move you back to the root directory**
---------------------------------
### Paths!
There are two main types of paths: 
1- Absolute path
2- Relative path

**Absolute path** has a / forward slash in it and begins from the root path ie **(/home/zaid)**

**Relative path**  specify a location (file or directory) in relation to where we currently are in the system and does not have a / forward slash.
`
➜  ~ ls PrepCourse
prep-course-py-01
➜  ~ ls /home/zaid/PrepCourse
prep-course-py-01
`
#### Other Paths!
- ~ (tilda) which is the root directory of the system can be used with ls and cd 
- . (dot) This is a reference to your current directory. Can also be used with ls and cd 

-  .. (double dots) This is a reference to the parent directory, ie it goes back to the previous directory from where you are at.

**Note:** 
Tab Completion can be used to auto complete lines
pressing tab x2 will show you the possibilities of it.

---------------------
### More About Files!
- Everything there is considered a file even directory is a file.

- Extentions can have 2 - 4 characters which tells what can tell what the file really is and to know exactly what the type of it is we use `file [path]` which gives out the type in the terminal.(linux will consider everything what it truly is even without the right extension)

- Spaces in names will be defined as seperate directories in ls or cd command ie `ls My Home ` will read **My** as directory and **Home** as another. To avoid running into this problem we either use **Quotes''or ""**
or have a back slash \ to escape the spaces and consider it as one name.

- Tab completion can be used to escape the spaces.

- Hidden files are those files starting with **.** and to see those files using **ls** we must add an option to it **-a** to make it like `ls -a`
---------------------------------------------
<br>

### Manual Pages!

They are pages where a user can find all the commands and what they do and how they are written in the terminal just by using this command line `man <command to look up>` i.e `man ls` will show all the details on that command.

Another way to search for a command is to search for its function and find out the command if you happen to not know it using this command `man -k <search term>` i.e `man -k move` will show all the commands with the word move in them. also you can search inside the **man** command by add `/<term>` and typing `n` to flip through the pages.

-------------------------------------------------
<br>

### File Manipulation!

#### <ins>Making a directory</ins>
To make a directory using terminal commands we type `mkdir [options] <Directory> ` where the options can be `-p` to make the directory a parent directory and `-v` to show us what the terminal is actually doing.
**The Directory** the name of it and other directories inside it.

#### <ins>Removing a directory</ins>
To remove a directory we can use this command
`rmdir [options] <Directory>` and it supports a `-p` and `-v`

#### <ins>Creating a Blank File</ins>
To creat a file we use this command `touch [options] <filename>` touch basically touches a file and if it doesnt exist it will create a new file.
and to edit on it we use `nano <filename>` to open it and edit it as we like.

#### <ins>Copying a File or Directory</ins>
To copy a file or a directory we use the following command `cp [options] <source> <destination>` where cp stands for copy. source is the path to the file you want to copy and destination is the path to either the file which will have the data as the file. however if the destination was a folder it will copy the file and name it as the source and put it inside the directory.
**note** we can use -r which stands for recursive which will enter all the subdirectories inside a directory and copy them if used with the `cp` command.

#### <ins>Moving a File or Directory</ins>
To move a file we use the command mv which is short for move. It operates in a similar way to cp. One slight advantage is that we can move directories without having to provide the -r option which moves everything inside them using this command.
`mv [options] <source> <destination>` ie `mv file2 directory1/file4` this moves file2 and puts it inside directory1 and names it file4.
We can also rename the same directory or file and move it.

#### <ins>Removing a file</ins>
we can use a similar command to remove a directory called rm and use this command:
`rm [options] <file>` this will remove the file but to remove a non-empty directory we use `rm -r <directory>` option and `-i` to give us a notification confirming the removal since there will be no going back after its removed.








