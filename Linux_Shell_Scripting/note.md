- whoami: to display user name
- date
- cal

- Linux File System

  - Everything is file
  - Ordinary File
    - starts with '-'
  - Directory File
    - starts with 'd'
  - Linked File
    - starts with 'l'

- pwd
- ls
  - ls -l directory_name
  - ls -lr
  - ls -a
  - ls -lt
  - ls -ltr
- cd
  - cd .. : change to parent directory
  - cd 'directory name'
- root directory '/'

- mkdir: to create a directory
  - `mkdir "directory names" `
- rmdir: to remove directory if its is empty

- commands to create files
  - touch filename: to create empty file
  - rm filename: to remove file/non-empty dir
    - rm \*.txt : delete all files with extension txt
    - rm -rf directory_name
      - r:recursive
      - f:forcefully
  - cat command: Create file with data,print file data,append data to file
    - `cat > f1.txt`: create file with this data,if file exist replace the data
    - `cat >> f1.txt`: append data to file
    - `cat f1.txt`: print file data
    - `cat -n f1.txt`: print dat alon with line no.
- mv : to rename file,to move file one location another location

  - `mv present_name  new_name`
  - `mv filename/<present_location> directory_addres_to_move`

- tac: Print content of file from top to bottom --> `tac file_name`
- rev: `rev filename` print the string inside file in reverse order
- cp: `cp sourcefile destinationfile`: copies sourcefile text in destination file
  - applicable one you want to copy only one file data
  - It overwrites the copied data on present data
- For more than one file use cat command
  `cat f1.txt f2.txt > f3.txt`: overwrites
  `cat f1.txt f2.txt >> f3.txt`: appends

- wc: give word count information of a file `no_lines no_words no_characters file_name`
- diff: difference in content of two files
  `diff file1 file2`
- cmp: similar like diff but tale on difference in lines info does not display line
- history: show history of commands
- `head file`: top 10 lines are displayed
- `head -5 file`:top 5 line are printed
- tail: last 10 lines are displayed
- `tail -f file`
- grep: global regular expression print: use for searching text in file

  - `grep 'string_to_search' file`
  - `grep -i 'string_to_search file`: ignore casesensitivity
  - `grep -n 'string_to_search file`:print line no.
  - `grep -i -n 'string_to_search'`: search string on file in current working directory

- How to edit file in Linux

  - use vi(visula editor)
  - `vi file`: to edit file ,or create and edit
  - vi modes:
    - command mode
    - insert mode: `i`
    - escape mode: `esc`
    - exit vi: `:wq` with saving changes
      - `:q!`: save without changes

- SED Command

  - SED: Stream Editor
  - It is used for processing the data in the file
    - insert,deletion,updation without opening the file

- Eg. Replace java with python

  - `sed 's/java/python/' data.txt`:only replace first occurence of java in each line
  - how to replace 2nd occurence of java in each line
    `sed 's/java/python/2' data.txt`: replace only 2nd occurence of java in each line with python
  - s: subsitute
  - To remove all occurence of java in each line:`sed 's/java/python/g' data.txt`: g: global

  in sed original file does not get affected till now

  - to make changes in file also:use -i option
    `sed -i 's/java/python/g' data.txt`

- to delete use `d` option:
  eg. `sed '4d' data.txt`: 4th line will be delete
  eg. `sed '$d' data.txt`: delete last line
  eg. `sed '3,$d' data.txt`:delete 3rd line to last line
  eg. `sed '1,4d' data.txt`: delete from 1 to 4th line
  for permanent delete use -i option
- `sed -n '2,5p' data1.txt`: print 2nd line to 5 th line only
- `sed '/python/d' data1.txt` : delete line in python occurs
- to insert data

  - `sed '4i\C is a middle-level language' data1.txt`: insert a line befor 4th line
  - `sed 'a$i\Linux is an opensource OS' data1.txt`: insert at the end

  ## AWK

  - awk command is a text processing tool available in linux
  - manipulate and extract data
  - help us to query structured text data in a file

- Syntax: `awk 'patter {action}' file`

1. `awk '/manager/ {print}' file`: print lines where manager is available in column
2. `awk '{print $1,$4}' file`: print 1st and 4th column only
3. `awk '{print NR,$0 }' file`: print all rows and columns with line no.
4. `awk '{print NR "-" $1} file`:print 1st columns with `line_no-`
