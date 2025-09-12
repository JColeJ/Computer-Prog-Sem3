# **LINUX NOTES**

## Week #01:

### Create file (touch):

- To create a clean file in Linux use the *touch* command
  - Ex: `touch Hello.txt`
  - Output: *Creates a new file named `Hello.txt`*


### Echo

- Displays a line of text or variables
  - Ex: `echo Jordan Coleman`
  - Output: *prints out `Jordan Coleman`*
- Another way you can use echo is putting text into a file already made, or a file you're creating.
  - Ex: `echo Jordan Coleman > name.txt`
  - Output: *no output if typed correctly*
 

### Cat

- Displays the contents found within a file
  - Ex: `cat name.txt`
  - Output: `Jordan Coleman`


### Create Directory (mkdir)

- To create a new directory use the command mkdir
- You can create new directories in any location by using either a full path or reference path
  - Ex Full Path: `mkdir /home/user/Documents/Jordan`
  - Ex Reference: `mkdir Documents/Jordan` (Assuming you're in the user directory)


### ls

- Lists files and directories.
- If no pathname is given, lists the current directory (.)
  - Ex: `ls`
  - Output: *Outputs all files and directories under the current directory*
- Common Options: `-l, -a, -d, -i`

- ls -l: lists in long format (File type and perms, number of links, Owner, Group, File Size/Name, Modification date/time)
  - Ex: `ls -l`
  - Output: `drwxr-xr-x 2 user user 4096 Sep 12 10:15 folder`

- ls -a: All Files
  - Ex: `ls -a`
  - Output: `. .. .bashrc .profile file.txt folder` (`.` is the current directory, `..` is the parent directory.)
 
- ls -d: Directories only (Lists the directory itself instead of its contents. Useful for seeing metadate of directories)
  - Ex: `ls -ld folder`
  - Output: `drwxr-xr-x 2 user user 4096 Sep 12 10:15 folder`
    - Explanation: Without -d, it would list the contents of `folder`, not `folder` itself.
    - Explanation 2: If you used `ls -d folder` the output would just be `folder` as it would list the directory name and not any info about it.

- ls -i: Inode numbers (Displays the inode number for each file or directory. An inode is a unique identifier for a file in the filesystem)
  - Ex: `ls -i`
  - Output: `123456 file.txt 123457 folder`
    - Explanation: Inodes are useful when you're trying to identify hard links or toubleshoot file system issues.


**Combined Example**

- Ex: `ls -lai`
- Output: All files, With Inode numbers, In long listing format
