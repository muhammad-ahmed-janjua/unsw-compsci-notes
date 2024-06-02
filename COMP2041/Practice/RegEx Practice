##### Write a regex to match C preprocessor commands in a C program source file
```
^#
```
##### All the lines in a C program except preprocessor commands
```
^[^#]|^$
```
- `^[^#]`: Any line that starts with a character that is not # 
- `^$`: matches an empty line
##### The names "Barry", "Harry", "Larry" and "Parry”
```
^[BHLP]arry$
```
##### All lines in a C program with trailing white space (one or more white space at the end of line)
```
\s*$
```
- `\s`: is a bracket expression that matches any white space character
##### A string containing the word "hello" followed, some time later, by the word "world”
```
hello.*world
```
##### The word "calendar" and mis-spellings where 'a' is replaced with 'e' or vice-versa
```
c[ae]l[ae]nd[ae]r
```
- `c[a|e]l[a|e]nd[a|e]r` would not work as all special characters except for the caret lose their special meaning inside the brackets. 
##### A list of positive integers separated by commas
```
^[1-9][0-9]*(,[0-9][1-9]*)*
```
##### A C string whose last character is newline
```
^[^\n]*\n$
```
##### This regular expression [0-9]*.[0-9]* is intended to match floating point numbers such as '42.5'. Is it appropriate?
```
(0|[1-9][0-9]*)\.([0-9]*[1-9]|0)
```
