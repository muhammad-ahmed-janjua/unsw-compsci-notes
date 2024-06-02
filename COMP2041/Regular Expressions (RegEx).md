### What is RegEx? 

- **Defines a pattern for matching strings:** A regex is a sequence of characters that defines a search pattern. It is used to match strings against this pattern.

- Programs like grep can check matches with the aforementioned set of strings 

- **Matching an Email Address:**
``^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$$``

- **Explanation:** 
	- \'^'  asserts the position at the start of the string.
	- `[a-zA-Z0-9._%+-]+`: denotes that the sequence matches one or more characters that can be lowercase or uppercase (`a-zA-Z`). As well as containing any special characters as represented with `._%+-`
	- `@`: Matches the "@" symbol
	- `[a-zA-Z0-9.-]+`: Matches one or more characters that can be lowercase or uppercase letters (`a-zA-Z`), digits (`0-9`), dots (`.`), or hyphens (`-`). This represents the domain name.
	- `\.`: Matches a literal dot (`.`).
	- same with the second sequence of characters
	- `[a-zA-Z]{2,}`: Matches two or more characters that are lowercase or uppercase letters (`a-zA-Z`). This represents the top-level domain (like `.com`, `.net`, etc.).
	- `$`: Asserts the position at the end of the string.

### Why use RegEx?

- **Validation:** used to validate input strings to ensure that they conform to expected format (e.g -> email addresses, phone numbers and dates).

- **Search and Replace**: Programs use regex to find and replace substrings within larger strings

- **Text Parsing**: Regex helps in extracting specific data from texts by defining patterns for the data to match.

### RegEx Lore:

- **1943**: Warren S. McCulloch and Walter Pitts began to develop models describing how the human nervous system works to try and understand how the brain could produce complex patterns using simple cells that are bound together.

- **1956**: *Stephen Kleen* described McCulloch-Pitts neural methods with an algebra notation which were penned ***'regular expressions'**.

- **1968**: *Ken Thompson* (Unix pioneer) implemented regex into the text editor 'ed' to implement advanced pattern matching in text files. 

### RegEx Rules

##### Basics: 
- any regex can \beta written using only (), \*, | and \.
- unless a character has a special meaning, it matches itself i.e a matches a.

|                          |                                                                                                           |
| ------------------------ | --------------------------------------------------------------------------------------------------------- |
| **p***                   | 0...infinity repititions of p.                                                                            |
| **pattern1 \| pattern2** | Union of pattern1 and pattern2. <br>- **i.e** ***hello \| world*** matches ***hello, world***             |
| **()**                   | Parentheses are used for grouping. <br>- **i.e**  (d\|e)*(f\|g) matches f, g, df, dg, ef, eg, ddf, deg, … |
| \                        | removes the special meaning of the following characters. <br>- i.e \. matches .                           |

##### Matching single characters:

|      |                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \.   | Matches any single character. <br>- i.e . matches a, b, ! ...                                                                                                                                                                                                                                                                                                                                                   |
| \[c] | Matches any one of a set of characters, similar to 'or'. <br>i.e <br>- ***\[aeiouAEIOU]*** matches any English vowel<br>- Shorthand for a range of characters ***\[a-z]*** matches any lowercase English letter<br>- '\^' inverts the meaning of the square brackets<br>- \[^123] matches any characters except 1, 2 and 3 Any ***other characters lose their special meaning inside bracket expressions***<br> |

##### Anchoring matches:

|     |                                                                                                                   |
| --- | ----------------------------------------------------------------------------------------------------------------- |
| \^  | When not inside square brackets, they match the start of the string <br>i.e \^h matches hello but not short       |
| \$  | Matches the end of a string<br>i.e `^cat.*dogs` matches any string starting with `cat` and ending with `dog`.<br> |

##### Matching repeating characters:

|        |                                           |
| ------ | ----------------------------------------- |
| p*     | Matches zero or more repetitions of p<br> |
| p+     | Matches one or more repetitions of p      |
| p?     | Matches zero or one repetitions of p      |
| p{n}   | Matches n repetitions of p                |
| p{n,m} | Matches n to m repetitions of p           |
| p{n,}  | Matches n or more repetitions of p        |
| p{,m}  | Matches m or less repetitions of p        |

##### Pratice:
[[Regex Practice]]
