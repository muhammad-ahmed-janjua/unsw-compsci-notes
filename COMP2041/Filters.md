### What is a filter?

- A filter is a program that transforms a byte stream.
- reads bytes from stdin -> performs transformations -> write transformation to the stdout

### Using filters:

- **Shell I/O redirection**
	- specify source and destination file
	- **Input Redirection '<'**
		- instead of taking input from the terminal the program takes the input from the specified file
	- **Out Redirection '>'**
		- Redirects the output of a command to a file 
- Filters can be chained with the following
	- filter1 | filter2 | ... | filterN

### Filter options

- '-' -> introduces the option
- '-v' -> option short form
- '--verbose' option long form
- '-av' and '-a -v' are the same

### To find while filters are available use -> apropos *filter*


## Filters

### cat
- Copies the input into the output (files are unchanged #identityfilter)
- ##### cat options 
	- `'-n'` -> number of output lines (from 1)
	- `'-A'` display non-printing characters (debugging)
	- `'-s'` squeezes consecutive black lines into one
	- `'-tac'` reverses the order of lines
	- `'-rev'`reverses the order of characters in lines

### grep
- `grep` copies to stdout the lines that match a specified [[Regular Expressions (RegEx)]]
- It has useful flags:
	- ##### grep options
	    - `-i` ignores upper/lower case `grep -i 'h' file.txt`
	    - `-v` displays lines that do not match the pattern `grep -v 'h' file.txt`
	    - `-c` print a count of matching lines
	    - `-w` only match pattern if it makes a complete word
	    - `-F` matches strings only (no regex)
	    - `-G` matches a subset of regex
	    - `-E` matches full POSIX regex***
	    - `-P` matches POSIX regex + Perl extensions
### wc: word count
- summaries it's input as a single line
- It has useful flags:
	- ##### wc options
	    - `-c` print number of characters
	    - `-w` print the number of wrods (non-white-space)
	    - `-l` print the number of lines only
	- by default wc prints, the number of lines, words and characters in it's inputs
	```
	$ wc /etc/passwd 
	49 79 2793 /etc/passwd
	```

# ==tr: transliterate characters==
- reads chars and writes characters, mapping (replacing) some chars with others
- the mapping is specified as 2 arguments: tr sourceChars destChars**
```
tr 'abc' '123' < someText
```
- 𝑠𝑜𝑢𝑟𝑐𝑒𝐶ℎ𝑎𝑟𝑠 = 'abc', 𝑑𝑒𝑠𝑡𝐶ℎ𝑎𝑟𝑠 = '123': a → 1 b → 2 c → 3

- tr doesn’t accept file names on the command line - it uses stdin 
- only tr is not line-based it works with individual chars 
- most tr implementations do not support multi-char characters (UTF8) 
	- they really work with bytes not characters!
- Chars that are not in 𝑠𝑜𝑢𝑟𝑐𝑒𝐶ℎ𝑎𝑟𝑠 are copied unchanged to output. 
- If there is no corresponding char (i.e. 𝑑𝑒𝑠𝑡𝐶ℎ𝑎𝑟𝑠 is shorter than 𝑠𝑜𝑢𝑟𝑐𝑒𝐶ℎ𝑎𝑟𝑠), then the last char in 𝑑𝑒𝑠𝑡𝐶ℎ𝑎𝑟𝑠 is used. 
- Shorthand is available for specifying char lists: E.g. 'a-z' is equivalent to 'abcdefghijklmnopqrstuvwxyz' 
- Note: newlines can be modified if the mapping specification requires it.
- It has useful flags:
	- ##### tr options
	    - `-c` map all bytes not occurring in 𝑠𝑜𝑢𝑟𝑐𝑒𝐶ℎ𝑎𝑟𝑠 (complement)
	    - `-s` squeeze adjacent repeated characters out (only copy the first)
	    - `-d` delete all characters in 𝑠𝑜𝑢𝑟𝑐𝑒𝐶ℎ𝑎𝑟𝑠 (no 𝑑𝑒𝑠𝑡𝐶ℎ𝑎𝑟𝑠)
```
# map all upper-case letters to lower-case equivalents tr 'A-Z' 'a-z' < text 
# naive encryption (a->b, b->c, ... z->a) 
tr 'a-zA-Z' 'b-zaB-ZA' < text 
# remove all digits from input 
tr -d '0-9' < text 
# break text file into individual words, one per line tr -cs 'a-zA-Z0-9' '\n' < text
```

### head/tail: select first/last lines
- head -> prints the first n (default 10) lines of input.
- tail -> prints the last n lines of input. 
- **head/tail options:**
	- `-n` :  changes the number of lines head/tail prints.

### cut: vertical slice
- prints selected parts of input lines
- can select fields, ***column separator defaults to tab***
- **cut options:**
	- `-f`*listOfCols:* prints only the specified fields (tab-separated).
	- `-c`*listOfPos*: prints only chars in the specified position.
	- `-d`c: use character c as the field separator. 
- lists are specified as range (1-5) or comma separated (2, 4, 5)
- cut cannot refer to last column without counting the columns 
- cut cannot reorder the columns
```
# print the first column 
cut -f1 data 
# print the first three columns 
cut -f1-3 data 
# print the first and fourth columns 
cut -f1,4 data 
# print all columns after the third 
cut -f4- data 
# print the first three columns, if '|'-separated 
cut -d'|' -f-3 data 
# print the first five chars on each line 
cut -c1-5 data
```

### sort: sort lines
- default sort is based on the first character of the line
- sort can also:
	- understand that text data sometimes occurs in delimited fields i.e it can sort fields (columns).
	- can distinguish numbers and sort them
	- can ignore punctuation or case differences 
	- can sort files "in place" as well as behaving like a filter
	- capable of sorting very large files 
- **sort options:**
	- `-r` sort in descending order (reverse sort) 
	- `-n` sort numerically rather than lexicographically 
	- `-d` dictionary order: ignore non-letters and non-digits 
	- `-t𝑐` use character 𝑐 to separate columns (default: non-blank to blank transition) 
	- `-k𝑛` sort on column `n`

### uniq: remove or count duplicates
- remove all but one copy of adjacent identical lines
- **uniq options:**
	- `-c` also print number of times each line is duplicated 
	- `-d` only print (one copy of) duplicated lines 
	- `-u` only print lines that occur uniquely (once only)
- useful:
	- for data analysis and summary
	- in tandem with cut
	- it tandem with sort to ensure that identical lines are adjacent
```
# extract first field, sort, and tally 
cut -f1 data | sort | uniq -c
```

### sed: stream (pipeline) editor
- editing commands are specified on command-line or in a file
- **Innerworkings of sed:**
	- read each line of input 
	- check if it matches any patterns or line-ranges
	- apply related editing commands to the line
	- write the transformed line to output
- sed can also:
	- parition lines based on patterns, not collumns
	- extract ranges of lines based on patterns or line numbers
- **sed options:**
	- `-n` do not print lines by default, applies all editing commands but does not print any output 
	- `-E` extended regex similar to grep
- **editing commands:**
	- p print the current line 
	- d delete (don't print) the current line 
	- `s / regex / replace` replace first instance of string matching regex with ***replace*** string 
	- `s / regex / replace / g` replace all instances of string matching regex with ***replace*** string
	- `q` terminate execution of sed
- when changing files with sed ensure you are not reading and writing from the same file
	- use a temp file instead
```
sed 's/[aeiou]//g' story.txt > story.txt # DANGER story.txt will be destroyed 
```
- The shell truncates story.txt to zero length before running sed.

### find: search for files
- allows to search for files based on specified properties
	- dictionary trees
- takes actions for all matching files
	- default print file names
- Invocation: find directories tests actions 
	- where the tests examine file properties like name, type, modification date 
	- the actions can be simply to print the name or execute an arbitrary command on the matched file
```
# find all new HTML files below ~/public_html 
find ~/public_html -name '*.html' -mtime -1 
# find background colours in my HTML files 
find ~/public_html -name '*.html' -exec grep -H 'bgcolor' {} \;
```

### join: database operator 
- merges two files using the values in a field in each file as a common key
- they can be in different positions in each file, but the files be ordered on that field
	- default field is 1
- **join operations**
	- `1k` key field in first file is k
	- `2k` key field in second file is k
	- `aN` print a line for each unpairable line in file *N* (1 or 2)
	- `-i` ignore case
	- `-t c` tab character is c 

```
$ cat data1 
Bugs Bunny 1953 
Daffy Duck 1948 
Donald Duck 1939 
Goofy 1952 
Mickey Mouse 1937 
Nemo 2003 
Road Runner 1949
```

```
$ cat data2 
Warners Bugs Bunny 
Warners Daffy Duck 
Disney Goofy 
Disney Mickey Mouse 
Pixar Nemo
```

```
$ join -t' ' -2 2 -a 1 data1 data2 
Bugs Bunny 1953 Warners 
Daffy Duck 1948 Warners 
Donald Duck 1939 
Goofy 1952 Disney 
Mickey Mouse 1937 Disney 
Nemo 2003 Pixar 
Road Runner 1949
```

### paste: combine files
- displays several text files "in parallel" on output
- if the input files are a, b, c
	- the first line of output is composed of the first lines of a, b, c
	- so on and so forth
- lines from each different file are separated by a tab character or specified delimiter 
- in case of mismatching file sizes there is output for all the lines of the longest file with empty strings for missing lines

### tee: second copy of pipeline to file
```
$ echo Hello Andrew | tee copy.txt 
Hello Andrew 
$ cat copy.txt 
Hello Andrew
$
```

### xargs: run commands with arguments from standard input 
- xargs operations: 
	- `-nmax-args` use at most max-args arguments per command line 
	- `-Pmax-procs` run up to max-procs processes at a time
	- `-ireplce-str` replace occurrences of replace-str with words read from stdin
```
# remove home directories of users named Andrew: 
grep Andrew /etc/passwd | cut -d: -f6 | xargs rm -r 

# run make in every sub-directory below /usr/src/ 
# with a Makefile, run up to 8 make's in parallel 
find /usr/src -name Makefile | sed 's/Makefile//' | xargs -P8 -i@ make -C @
```

### process substitution (AKA named pipes)
- bash provides process substitution
- **syntax:**
	- `< (command)`
	- eg. `diff < (sort file1)  < (sort file2)`
		- runs sort file1 and sort file2 then passes fake filenames to diff as arguments
	- `> (command)`
		- eq `tar cf - somedir | tee >(shasum > dir.tgz.shasum)  > (md5sum > dir.tgz.md5sum) > dir.tar`
			- runs shasum, md5sum and creates dir.tar all with the output of tar
- useful for commands which don't provide any way of reading from stdin or writing to stdout
	- check if - as filename works
	- and also /dev/stdin/dev/stdout may be available
- useful for combining two pipelines

### Summary:
- **Horizontal slicing - select subset of lines:** cat, head, tail, grep, sed, uniq 
- **Vertical slicing - select subset of columns**: cut , sed 
- **Substitution:** tr, sed 
- **Aggregation, simple statistics:** wc, uniq 
- **Assembly - combining data sources:** paste, join 
- **Reordering:** sort 
- **Viewing (always end of pipeline):** more, less 
- **File system search:** find 
- **Programmable filters:** sed (also awk, python, perl, …)
