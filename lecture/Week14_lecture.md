# Gen 349 - Week 14 - Programming for Biologists

# Basic UNIX Tutorial

**Original material by [Shane Dooley](https://github.com/skDooley/shell_tutorial) and Dr. Geetu Tuteja.
Modified and compiled by Ha Vu (Tuteja Lab).**

## Outline
0. Introduction to UNIX
1. Accessing HPC
2. General structure of a command in Unix
3. Navigating Directories
4. Creating and Destroying files
5. Shortcuts
6. Examining files on the command line
7. Conclusion


    
## Before we begin


### *Make sure you have access to either Putty, or Terminal. If you don't, tell us!*

### Take notes of commands we go through
Suggested format:

| Command | What it does | Example |
|:-:|:-:|:-:|
|  Command | What it does |  |

## Introduction to UNIX
### What is UNIX?
- A common operating system.
- What is an operating system?
    - An operating system is the suite of programs that make the computer work.
- The UNIX operating system is made up of the kernel, the shell, and the programs.
    - The **kernel** is the hub of the operating system. It allocates time and memory to programs.
    - The **shell** is the interface between the user and a kernel. It is a **command line** interpreter.
    - Shell commands can be run in the **terminal**.
    
<img src="/images/SHELL.png" width="500" height="400"/>

### UNIX based operating systems

#### Linux
- Operating system and bundled application programs.
- Derived from Unix.
- Linux is free (open source).
- Linux is stable.
- Linux systems are highly customizable.
- **Computing clusters are all Linux based.**

#### MacOSX
- More user friendly for beginners.

### UNIX in Bioinformatics
UNIX is useful...

- when you are trying to open a large FASTQ file.
- when you are searching for specific information from a large number of files.
- when you want to rename a large number of files.
- when you want to combine a large number of files into one file.
- when you need to run a program that is not available on Galaxy, and can only run in a UNIX-based environment.
- when you want to automate repetitive tasks.

## Accessing HPC class and some notes
Now we will connect to the HPC class for today's tutorial. Make sure to always follow these steps when working on class material. 

### Step 1: Connect to ISU Wifi or VPN (if off campus)

* Note an ISU guest Wifi will not work. For example: IASTATE-Guest

### Step 2: Connect to Nova

#### Windows:
If you are on Putty, put the information as in the picture here:

<img src="/images/hpc-class.PNG" width="360" height="350" />

Replace `hhvu` with your own NetID.

#### MACS:
Open the Terminal and copy and paste the command below and replace `your-net-id` with your own NetID:

```
ssh your-net-id@nova.its.iastate.edu
```
	
#### Enter Verification code
Type the GA code from the app on your device when "Verification code:" is prompted.

* Note: No characters will show in the terminal while you are typing. 

<img src="/images/verify.PNG" width="490" height="125" />

#### Enter your Net ID password.

* Note: No characters will show in the terminal while you are typing your password.

### Step 3: Request interactive access to a compute node in instruction partition
Please copy paste the following command to your terminal:

```
salloc -p instruction -N 1 -n 4 -t 3:00:00 -A s2024.gen.349.1
```
    
#### How to paste to terminal:
- If you are in Mac terminal: `Command + V`
- If you are in Putty: `Right click`

#### How to copy from terminal to other program:
- If you are in Mac terminal: highlight the text and then hit `Command + C`.
- If you are in Putty: highlight the phrase to copy.

Once the partition is granted, it will prompt some messages similar to the following:

<img src="/images/class-partition.PNG" width="950" height="110" />


## Cloning the GitHub Repository

- Copy and Paste the commands below to your terminal.
- Navigate to the `classtmp/` directory


	``` cd /work/classtmp/GEN349_S2024/ ```

- Make a directory named with your ISU NetID. 

	```mkdir krkies``` 

	Note: Replace `krkies` with your ISU NetID

- Navigate into your new directory: 
	```cd krkies/```

- Clone the GitHub repository for today's class. 

    ```git clone --single-branch --branch main https://github.com/Tuteja-Lab/gen349_week_14_15.git```


## Things to Remember!
### Tips
- Attention to detail is important.
    - Capitalization matters.
    - Spaces matter.
    - Semi colon, commas matter.
- Don’t try to rush through everything.
- If you get overwhelmed, take a deep breath and try again. You got this!

### If you have questions:
- Tell us if you need us to slow down.
- If you move faster than us, wait to ask your question until we get to the part you are on.

## General structure of a command in Unix

`program [-flags] argument1 argument2 ...`

- For example:
    `echo hello world`
    
| Term | Definition | Example |
|:-:|:-:|:-:|
|  program | the name (case sensitive) of the program  | echo |
|  argument | additional information you give the program to get it to do what you want it to do.  | hello world |    

- Flags = options to run the program. Flags start with a single dash `-` or two dashes `--`, and change the behaviour of a command.


## Navigating Directories

- A **directory** is similar to a folder that can hold files on your computer.
- Directories are organzied in a hierarchy. 

### pwd
- `pwd` = print working directory.
- Tells you where you are sitting in the directory tree.
- Whenever you start up a terminal, you will start in a special directory called the `home` directory. Every user has their own home directory where they have full access to do whatever they want.

### ls
- `ls` = list the files in the current directory.
- Another option: add flags to `ls`.
    - For example: `ls -l` 
- To explore all options to run `ls`, type `man ls`.
- Within the `man` page, use arrow keys to move up/down/left/right. To quit the `man` page, hit `q`.

### cd
- `cd` = change directory.
- Helps you navigate between different directories.

Now, let's navigate to the directory `lecture` replacing replace `krkies` with your NetID: `cd /work/classtmp/GEN349_S2024/krkies/gen349_week_14_15/lecture` 

Recheck where you are: `pwd`

Check what is in the directory: `ls`

### Root vs home; Relative vs. absolute path
- Root = the first or top-most directory in a hierarchy. Sometimes you won't have full access in `root`, e.g., when you are on university's high performance clusters.
- `home` directory is under the root.

<img src="/images/absolutePathNames.jpg"/>
Adapted from https://www.geeksforgeeks.org/absolute-relative-pathnames-unix/

- Where you are in the directory tree is called your **path**.
- In a path name, different directories and file names are separated by a slash `/`. The root has no name, so it's only one slash `/`.
    - For example:
    	* Note: Command line will not recognize comments beginning with #. 		These are used for documentation.
    
	    ```
	    cd / 
	    pwd
	    ls #check what is in the root directory
	    ```
    
    
- A path is either relative or absolute:
    - An absolute path = the root element and the complete directory list. For example, `/work/classtmp/GEN349_S2024/krkies/gen349_week_14_15/` is an absolute path. An absolute path always starts with `/`.
    - A relative path needs to be combined with another path in order to access a file. For example, `gen349_week_14_15/lecture` is a relative path.

<img src="/images/pathExample.png" width="500" height="400"/>

- The current directory is denoted by `.`.
- The parent directory is denoted by `..`.

- When we do `cd ..`, this will put us one directory above where we were.
- When we do `cd`, this will put us back to the `home` directory.

#### Question time!
1. There's a directory called `hearingData` under the directory `lecture`.
- How would you go to the directory if you are currently in the `gen349_week_14_15` directory?
- How would you go to the directory regardless of your current location?

2. Which files listed below are in the `hearingData` directory?
    <p> A. Data8355, Data7493, Data1235 </p>
    <p> B. Data0335, Data0492, Data0225 </p>


## Creating and Destroying files
| Command | Description |
|:-:|:-:|
|mkdir| makes a directory|
|rmdir| removes an empty directory|
|touch <nameOfFile>| creates an file|
|rm <nameOfFile> | removes a file|
|rm -r <directory> | removes an entire directory and all of its contents|
|cp <filename> <destination>| copy a file to a location|
|mv <filename> <destination>| moves a file to a location|
    
For example:

```
mkdir testdir
cd testdir
touch testfile.txt
ls
cd ../
rm testdir
```

You cannot `rm testdir` here. Why?

### `rm -r` 
`rm -r` will remove non-empty directories and all the files within them. 

* Make sure you ALWAYS know what you are deleting BEFORE you delete it!  
* `rm -r` HAS GIVEN ME NIGHTMARES. BE CAREFUL! 

## Shortcuts
   
### Wild card
- The `*` character matches against any set of characters.
- For example, the following command list all the files in our current directory that contain "md" at the end of the file names:
    `ls *md`
- If there is no file with the name pattern `*md` in the directory, it will throw an error `ls: cannot access *md: No such file or directory`.
    
	#### Question time!
	1. Make sure you are in the gen349_week_14_15 directory. Then, do this command: `ls lecture/hearingData/Data*4*2`. What do you observe from the patterns of the file names?


### Tab Completion
- Navigate to your `classtmp/` directory (in the command below, replace 'krkies' with your ISU Net ID)

	``` cd /work/classtmp/GEN349_S2024/krkies ```

- Typing out directory names can waste a lot of time. When you start typing out the name of a directory, then hit the tab key, the shell will try to fill in the rest of the directory name. For example, enter:

    `cd g<tab>`
    
- The shell will fill in the rest of the directory name for `gen349_week_14_15`. Once you change directories, enter:

    `ls lecture/Diverse<tab><tab>`
    
- When you hit the first tab, nothing happens. The reason is that there are multiple files in the `lecture` directory which start with `Diverse`. Thus, the shell does not know which one to fill in. When you hit tab again, the shell will list the possible choices.
- Tab completion can also fill in the names of programs. For example, enter `e<tab><tab>`. You will see the name of every program that starts with an `e`. One of those is `echo`. To quit out of the program list, hit `q`.
- If you enter `ec<tab>` you will see that tab completion works immediately, because there is only one program name starting with `ec`.

### clear

* Sometimes your terminal is filled with past commands/outputs, and you want to have a clean terminal to avoid confusion. Then, you can do:

    ```
    clear
    ```

	or hit `Ctrl + l`.

* You can use the up arrow key to see past commands/outputs.

### Quick check:
If I want to go to the directory `lecture` but I don't know where I am now, what should I do?

Let's go to the directory `lecture`!

* If you are not sure how to get there from your current directory you can always use this command:

```
cd /work/classtmp/GEN349_S2024/krkies/gen349_week_14_15/lecture/
```
    
## Examining files on the command line
### cat
- `cat` = concatenate.
- Displays contents of file on screen.
    - For example:

        `cat file1.bed`
        
    - This will display the entire file at once. So it will look overwhelming if you have a big file!
- If you put two file names, it will display the first file, followed by the 2nd file.
	- For example:
	
		`cat file1.bed file2.bed`

### less
- `less` opens the file, and lets you navigate through it.

	``` less DiverseCas9s.faa ```

- Use "space" to go forward and hit the "b" key to go backwards.
- The "g" key goes to the beginning of the file and "G" (i.e., `shift + G`) goes to the end.
- Finally, hit `q` to quit.

### head
- `head` writes the first ten lines of a file to the screen.
- To change the number of lines printed, type `head -n <number> <file name>`.
- Make sure you are in the directory `lecture`.
- Let's try: `head -n 5 DiverseCas9s.faa`

### tail
- `tail` writes the last ten lines of a file to the screen.
- To change the number of lines printed, type `tail -n <number> <file name>`.
    - For example, `tail -n 5 DiverseCas9s.faa`
    
### grep
- `grep` can search files for specific words or patterns.
- For example:
    `grep "locus" DiverseCas9s.faa`
- To explore other options, `man grep` or `grep -h` or `grep --help`
    
### sort
- `sort` provides different options to sort a file.
- For example, `sort DiverseCas9s-names.txt` will sort the file `DiverseCas9s-names.txt` alphabetically based on the first column.
- If your file has multiple columns, you can use `-k` and the column number to sort by another column than the first (default).
- For more options in `sort`, type `man sort` or `sort --help` (`-h` may not work in this case). Reminder: to exit the `man` page when doing `man sort`, hit `q`.
- Note: `sort -n` will compare according to numerical value, but it cannot understand the value of scientific notation such as `6E+10`.

    
#### Question time!
1. Read through the `man` page of `sort`. If I want to sort something in  **reverse** order, what `-flag` should I use?
    <p> A. `-b` </p> 
    <p> B. `-i` </p>
    <p> C. `-r` </p>
    <p> D. `-n` </p>
	

### uniq
- `uniq` can be used to identify lines that occur uniquely in a file (`-u`), lines that are duplicated in a file (`-d`), or to count the number of occurrences in a file (`-c`)
- Without any options, it is similar to `sort -u` (which only keeps unique entries).
- Files must be sorted before running this command.

### cut
- `cut` can be used to print only selected columns from a file.
- Examples:
    - Print column 1 of `DiverseCas9s-names.txt`, do `cut -f 1 DiverseCas9s-names.txt`.
    - Print column 1 and 3 from `DiverseCas9s-names.txt`, do `cut -f 1,3 DiverseCas9s-names.txt` (no space between `1,` and `3`).
- To explore other options, do `cut --help`.


### wc
- `wc` will print newline, word, and byte counts for each file.
- Do `man wc` to find out all options in `wc`.
- For example, if you want to count the number of lines in a file:

    `wc -l DiverseCas9s.faa`
    
#### Question time!
1. If I want to count the number of words in a file, what `-flag` should I use?
2. How many words are there in the file `hearingData/Data0526`?

### Redirect data `>` to a file
- The following command puts the output on the screen.

    `grep "gbkey=CDS" DiverseCas9s.faa`

- What if you want to store the output to another file?

    `grep "locus_tag=STER" DiverseCas9s.faa > Cas9sOutput.txt`

### Append data `>>`to a file
- What if you want to add the search results to your output file that already exists?

    `grep 'protein_id=YP' DiverseCas9s.faa >> Cas9sOutput.txt`

- If you only used the `>` the text that was already in the file would be overwritten.

### Pipe `|`
- The `|` command (hit `Shift + \`) allows you to connect the output of one command to the next command.
- Save time and memory when programming!
- For example:
    `grep 'protein_id=YP' DiverseCas9s.faa | wc -l`
	- In this command, we search for every line that has the pattern `protein_id=YP` in the file `DiverseCas9s.faa`, then immediately count the number of such lines.
	- The normal command of `wc` is `wc -l <input file>`, but here in the pipe, we only see `wc -l`, because the `<input file>` was piped directly from `grep 'protein_id=YP' DiverseCas9s.faa`.

## Conclusion
- The ability to use and navigate with UNIX is essential.
- Our best friends: Google, `man`, or `<program name> --help`.
