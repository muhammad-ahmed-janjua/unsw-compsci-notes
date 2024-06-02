#### What is a filter?

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
- #### Practice
	- [[Regex Practice]]
