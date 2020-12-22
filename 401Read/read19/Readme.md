# Table of contents
|Read No. | Name of chapter|
|:---------: |:--------------:|
|19|[Python Regular Expressions Tutorial](Python-Regular-Expressions-Tutorial.md)
|19|[shutil](shutil.md)






# Python Regular Expressions Tutorial
## Inroduction:
### Regular Expressions, often shortened as regex, are a sequence of characters used to check whether a pattern exists in a given text (string) or not. If you've ever used search engines, search and replace tools of word processors and text editors - you've already seen regular expressions in use. They are used at the server side to validate the format of email addresses or passwords during registration, used for parsing text data files to find, replace, or delete certain string, etc. They help in manipulating textual data, which is often a prerequisite for data science projects involving text mining.

## Regular Expressions in Python
### In Python, regular expressions are supported by the re module. That means that if you want to start using them in your Python scripts, you have to import this module with the help of ```import```

## Basic Patterns: Ordinary Characters
### Ordinary characters are the simplest regular expressions. They match themselves exactly and do not have a special meaning in their regular expression syntax.

### Examples
```python
pattern = r"Cookie"
sequence = "Cookie"
if re.match(pattern, sequence):
    print("Match!")
else: print("Not a match!")
```
### The ```match()``` function returns a match object if the text matches the pattern. Otherwise, it returns ```None```

### Do you notice the ```r``` at the start of the pattern Cookie?
### This is called a **raw string literal**. It changes how the string literal is interpreted. Such literals are stored as they appear.


## Wild Card Characters: Special Characters
### Special characters are characters that do not match themselves as seen but have a special meaning when used in a regular expression.

- ```.``` - A period. Matches any single character except the newline character.

```python
re.search(r'Co.k.e', 'Cookie').group()
```
```
'Cookie'
```

### With the search function, you scan through the given string/sequence, looking for the first location where the regular expression produces a match. The group function returns the string matched by the re. 

- ```^``` - A caret. Matches the start of the string.

```python
re.search(r'^Eat', "Eat cake!").group()
```
```
'Eat'
```

- ```$``` - Matches the end of string.
- [abc] - Matches a or b or c.
- [a-zA-Z0-9] - Matches any letter from (a to z) or (A to Z) or (0 to 9).

- ```\``` - Backslash.

### If the character following the backslash is a recognized escape character, then the special meaning of the term is taken 
### Else if the character following the \ is not a recognized escape character, then the \ is treated like any other character and passed through.
### ```\``` can be used in front of all the metacharacters to remove their special meaning.

### There is a predefined set of special sequences that begin with '\' and are also very helpful when performing search and match. Let's look at some of them up close...

- ```\w ```- Lowercase 'w'. Matches any single letter, digit, or underscore.
- ```\W``` - Uppercase 'W'. Matches any character not part of \w (lowercase w).
- ```\s``` - Lowercase 's'. Matches a single whitespace character like: space, newline, tab, return.
- ```\S``` - Uppercase 'S'. Matches any character not part of \s (lowercase s).
- ```\d``` - Lowercase d. Matches decimal digit 0-9.
- ```\D``` - Uppercase d. Matches any character that is not a decimal digit.
- ```\t``` - Lowercase t. Matches tab.
- ```\n``` - Lowercase n. Matches newline.
- ````\r``` - Lowercase r. Matches return.
- ```\A``` - Uppercase a. Matches only at the start of the string. Works across multiple lines as well.
- ```\Z``` - Uppercase z. Matches only at the end of the string.
- ```\b``` - Lowercase b. Matches only the beginning or end of the word.

## Repetitions
- ```+``` - Checks if the preceding character appears one or more times starting from that position.

- ```*``` - Checks if the preceding character appears zero or more times starting from that position.

- ```?``` - Checks if the preceding character appears exactly zero or one time starting from that position.

### But what if you want to check for an exact number of sequence repetition?

### For example, checking the validity of a phone number in an application. re module handles this very gracefully as well using the following regular expressions:

- ```{x}``` - Repeat exactly x number of times.
- ```{x,}``` - Repeat at least x times or more.
- ```{x, y}``` - Repeat at least x times but no more than y times.

## Function provided by 're'
### ```compile(pattern, flags=0)```
### Regular expressions are handled as strings by Python. However, with ```compile()```, you can computer a regular expression pattern into a regular expression object. When you need to use an expression several times in a single program, using ```compile()``` to save the resulting regular expression object for reuse is more efficient than saving it as a string. This is because the compiled versions of the most recent patterns passed to ```compile()``` and the module-level matching functions are cached.

```python
pattern = re.compile(r"cookie")
sequence = "Cake and cookie"
pattern.search(sequence).group()
```
```
'cookie'
```
### ```search(pattern, string, flags=0)```

### With this function, you scan through the given string/sequence, looking for the first location where the regular expression produces a match. It returns a corresponding match object if found, else returns None if no position in the string matches the pattern. 

### ```match(pattern, string, flags=0)```
### Returns a corresponding match object if zero or more characters at the beginning of string match the pattern. Else it returns None, if the string does not match the given pattern.
### ```findall(pattern, string, flags=0)```
### Finds all the possible matches in the entire sequence and returns them as a list of strings. Each returned string represents one match.

### ```finditer(string, [position, end_position])```

### Similar to findall() - it finds all the possible matches in the entire sequence but returns regex match objects as an iterator.

## Compilation Flags
### An expression's behavior can be modified by specifying a flag value. You can add flags as an extra argument to the different functions that you have seen in this tutorial. Some of the more useful ones are:

- IGNORECASE (I) - Allows case-insensitive matches.
- DOTALL (S) - Allows . to match any character, including newline.
- MULTILINE (M) - Allows start of string (^) and end of string ($) anchor to match newlines as well.
- VERBOSE (X) - Allows you to write whitespace and comments within a regular expression to make it more readable.



# shutil

## Copying Files
### copyfile() copies the contents of the source to the destination and raises IOError if it does not have permission to write to the destination file.

### Because the function opens the input file for reading, regardless of its type, special files (such as Unix device nodes) cannot be copied as new special files with copyfile().

### The implementation of copyfile() uses the lower-level function copyfileobj(). While the arguments to copyfile() are filenames, the arguments to copyfileobj() are open file handles. The optional third argument is a buffer length to use for reading in blocks.

### The copy() function interprets the output name like the Unix command line tool cp. If the named destination refers to a directory instead of a file, a new file is created in the directory using the base name of the source.
## Copying File Metadata
### By default when a new file is created under Unix, it receives permissions based on the umask of the current user. To copy the permissions from one file to another, use copymode().

### To copy other metadata about the file use copystat().
## Working With Directory Trees
### shutil includes three functions for working with directory trees. To copy a directory from one place to another, use copytree(). It recurses through the source directory tree, copying files to the destination. The destination directory must not exist in advance.

### The symlinks argument controls whether symbolic links are copied as links or as files. The default is to copy the contents to new files. If the option is true, new symlinks are created within the destination tree.

### copytree() accepts two callable arguments to control its behavior. The ignore argument is called with the name of each directory or subdirectory being copied along with a list of the contents of the directory. It should return a list of items that should be copied. The copy_function argument is called to actually copy the file.

## Finding Files
### The which() function scans a search path looking for a named file. The typical use case is to find an executable program on the shell’s search path defined in the environment variable PATH.

## Archives
### Python’s standard library includes many modules for managing archive files such as tarfile and zipfile. There are also several higher-level functions for creating and extracting archives in shutil. get_archive_formats() returns a sequence of names and descriptions for formats supported on the current system.
### Use make_archive() to create a new archive file. Its inputs are designed to best support archiving an entire directory and all of its contents, recursively. By default it uses the current working directory, so that all of the files and subdirectories appear at the top level of the archive. To change that behavior, use the root_dir argument to move to a new relative position on the filesystem and the base_dir argument to specify a directory to add to the archive.

## File System Space
### It can be useful to examine the local file system to see how much space is available before performing a long running operation that may exhaust that space. disk_usage() returns a tuple with the total space, the amount currently being used, and the amount remaining free.