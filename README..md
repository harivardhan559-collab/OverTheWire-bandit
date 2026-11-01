# OverTheWire Bandit Solutions

## Level 0 -> Level 1
- **Objective:** Find the password in the `readme` file.
- **Commands Used:** `cat readme`
- **What I Learned:** Basic file reading in Linux.

## Level 1 -> Level 2
- **Objective:** Read the file named `-`.
- **Commands Used:** `cat ./-`
- **What I Learned:** How Linux handles special characters in filenames.
- ( . )  this character is used to determine the current working directory.
- ( / )  its just determine the path.

## level 2 -> level 3
**Objective:** Read the file named `--spaces in this file--`.
- **Commands Used:** ` cat "./--spaces in this filename--"`
- **What I Learned:** --spaces in this filename-- is the file name can not able to see directly. In Linux, filenames with spaces must be wrapped in quotes (or escaped with backslashes `\`) so the shell treats the whole name as a single file instead of multiple arguments.

## level 3 -> level 4
**Objective:** Read the hidden file named inside an Directory  `Directory = inhere & hidden file = ...Hiding-from-you`.
- **Commands Used:** `ls , cd inhere , ls -a, cat ...Hiding-from-you `
- **What I Learned:** moving inside an specific directory and listing both files and hidden files ls -a command used to list the hidden files  and viewing the hidden file.

## level 4 -> level 5
**Objective:** Read an human readable file  inside an Directory  `Directory = inhere &  files = -file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09`
- **Commands Used:** ls, cd, ls -l, file ./*, cat .
- **What I Learned:**  file ./* -> this command is literally used to determine the type of data inside an file wheather its an human-readable or not wheather its an encrypted or not and so on.. rather than manually viewing all the files we can simply view an ruman readable file. 

## level 5 -> level 6
**Objective:** Read an human readable file  inside an Directory-inhere inside inhere many directories -  maybehere00  maybehere03  maybehere06  maybehere09  maybehere12  maybehere15  maybehere18 maybehere01 etc...

files = -file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09`
- **Commands Used:** ls, cd, cd ~, ls -l, file ./*, find inhere -type f -size 1033c ! -executable ,cat inhere/maybehere07/.file2 etc...
- **What I Learned:** cat inhere/maybehere07/.file2 inside this path i found the password (it resembles the path)
   new command  -> find inhere -type f -size 1033c ! -executable 
  
   Find : its used to search exactly what we need rather than seeing all of them 
 
  inhere: Searches inside the inhere folder and all of its subdirectories.(this is because inside this directory we have sub-directories)

  -type f: Looks only for files (ignoring folders because the password is stored inside file).

  -size 1033c: Searches specifically for a file that is exactly 1033 bytes (c stands for bytes because the size of the password was 1033 bytes).

  ! -executable: Excludes any file marked as executable (the file cant be executable just we can read or view it ).

  ## level 6 -> level 7
**Objective:** to determine the password  stored somewhere on the server and has all of the following properties:
owned by user bandit7 , owned by group bandit6 ,33 bytes in size.

- **Commands Used:** find / -user bandit7 -group bandit6 -size 33c , cat /var/lib/dpkg/info/bandit7.password , ls ,ls -a.
- **What I Learned:** new arrguments using both find and cat commands.
    - find /: Searches the entire file system starting from the root directory (/).
     - -user bandit7: Filters for files owned by the user bandit7.
      - -group bandit6: Filters for files owned by the group bandit6.
       - -size 33c: Filters for files that are exactly 33 bytes (c stands for bytes).
         - after executing the above command my terminal flooded with an permission denied paths out of that i have found a single path without permission denied i copied that path  and past as an argument for viewing password.

  ## level 7 -> level 8
- **Objective:** find the password which is stored in the file data.txt next to the word millionth.

- **Commands Used:** grep millionth data.txt 
 - syntax ->  grep(command) millionth(option) data.txt(pattern or file)
- **What I Learned:**  grep is an command which is used for finding the requirements by filtering. Given hint is next to the word millionth.


    ## level 8 -> level 9
- **Objective:** determine the password which is stored in the file data.txt and is the only line of text that occurs only once.

- **Commands Used:** sort data.txt, sort data.txt > hh.txt(my own file name), sort data.txt | uniq -u.

- **What I Learned:**  
   - this command (sort data.txt) just sorted the data but found difficult to determine the password so this command failed to determine the password.
  - sort data.txt > hh.txt(my own file name) -> (>)= this character it is used to erase the priveous content in file and writes new content. this command failed because i required permission.
  - sort data.txt | uniq -u =>  sort data.txt: This arranges all the lines alphabetically. It groups all identical lines next to each other so duplicates are touching.
| (The Pipe): This takes the sorted list and passes it directly to the next command without saving it to a file. uniq -u: Prints only lines that are non-repeated (unique lines that appear exactly once).


## level 9 -> level 10
- **Objective:**  password is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

- **Commands Used:** find . -type f , grep -rn "pattern" . , strings * | grep '=

- **What I Learned:**  

  - find . -type f: Searches the current directory (.) and every folder inside it, listing only files (ignoring all folders).

   - grep -rn "pattern" . : Searches inside every file across all subdirectories (-r) for a specific word or text string ("pattern"), and shows the exact line number (-n) where it appears.

   - strings * | grep '=' : Takes every file in your current folder (*), pulls out only human-readable text while ignoring binary trash (strings), and then passes that text (|) to grep to show only the lines containing an equal sign (=).

   ## level 10 -> level 11
- **Objective:**  password is stored in the file data.txt, which contains base64 encoded data.
 
- **Commands Used:** ls -l, cat data.txt, base64 -d data.txt

- **What I Learned:**   base64: The command-line utility used to encode or decode base64 data. -d: Tells the command to decode the data back into plain readable text (instead of encoding it). similarly -e:it indicates encoding.

## level 11 -> level 12
- **Objective:**  The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

- **Commands Used:** cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'

- **What I Learned:**  
   - tr = The tr command stands for translate. It replaces letters in the first list with letters from the second list in the exact order they appear.
    - 'A-Za-z' 'N-ZA-Mn-za-m' =  A-Z represents the entire top row from A to Z.N-ZA-M represents the entire bottom row:N-Z matches the first half (A–M -> N–Z).A-M matches the second half (N–Z -> A–M).

     

