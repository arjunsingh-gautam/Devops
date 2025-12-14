# <span style="color:orange">Assignment-1</span>

## Q1) Write the Command to display all Files including Hidden Files in Last Modifiction Time Order. Oldest should be First and recent should be Last. It should include Inode Number and the Number of Blocks used by that File. The Output should be in Long listing Form?

```sh
ls -atrisl
```

## Q2) Which Command will Lists all Files including Hidden Files along with their Inode Numbers?

```sh
ls -ai
```

## Q3) Which Command will make a Long listing of all the Files in our System including Hidden Files, sorted by Modification Date (Oldest First)?

```sh
 ls -atrl
```

## Q4) `ls -r` will List the Files sorted by Modification Date (Oldest First)?

> False,it will sort in natural reverse order based on lexicographical first files and then directories

## Q5) ls -la will not produce the Same Result as ls -al

> False,order of options doesn't matter
