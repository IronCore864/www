---
title: "Python Tutorial: 8. Input and File Handling"
author: "Tiexin Guo | 郭铁心"
authorLink: https://www.guotiexin.com
tags: ["python"]
categories: ["Python Tutorial"]
date: 2022-07-18
cover:
  image: "1200px-Python-logo.png"
  alt: "Python Tutorial"
---

There are several ways to present the output of a program; data can be printed in a human-readable form, or written to a file for future use.

## 1 Output Formatting

Often you'll want more control over the formatting of your output than using the `print()` function which simply prints space-separated values.

There are several recommended ways to format output:

### 1.1 Formatted String Literals

(Also called f-strings for short.)

Begin a string with `f` or `F` before the opening quotation mark or triple quotation mark.

Inside this string, you can write a Python expression between `{` and `}` characters that can refer to variables or literal values. Examples:

```python
>>> year = 2016
>>> event = 'Referendum'
>>> f'Results of the {year} {event}'
'Results of the 2016 Referendum'
```

### 1.2 The String format() Method

Basic usage of the `str.format()` method looks like this:

```python
>>> print('We are the {} who say "{}!"'.format('knights', 'Ni'))
We are the knights who say "Ni!"
```

A number in the brackets can be used to refer to the position of the object passed into the str.format() method:

```python
>>> print('{0} and {1}'.format('spam', 'eggs'))
spam and eggs
>>> print('{1} and {0}'.format('spam', 'eggs'))
eggs and spam
```

If keyword arguments are used in the str.format() method, their values are referred to by using the name of the argument:

```python
>>> print('This {food} is {adjective}.'.format(
...       food='spam', adjective='absolutely horrible'))
This spam is absolutely horrible.
```

---

## 2 Handling Files

### 2.1 Reading and Writing Files

`open()` returns a file object, and is most commonly used with two positional arguments and one keyword argument: `open(filename, mode, encoding=None)`

```python
>>> f = open('workfile', 'w', encoding="utf-8")
```

- The first argument is a string containing the filename.
- The second argument is another string containing a few characters describing how the file will be used.

> More words on the mode: Mode can be 'r' when the file will only be read, 'w' for only writing (an existing file with the same name will be erased), and 'a' opens the file for appending; any data written to the file is automatically added to the end. 'r+' opens the file for both reading and writing. The mode argument is optional; 'r' is the default value if it's omitted.

- Normally, files are opened in _text mode_, which means, you read and write strings from and to the file, which are encoded in a specific encoding. If encoding is not specified, the default is platform-dependent. Because UTF-8 is the modern de-facto standard, `encoding="utf-8"` is recommended unless you know that you need to use a different encoding.
- Appending a 'b' to the mode opens the file in binary mode. Binary mode data is read and written as bytes objects. You can not specify encoding when opening a file in binary mode.
- In text mode, the default when reading is to convert platform-specific line endings (`\n` on Unix, `\r\n` on Windows) to just `\n`. When writing in text mode, the default is to convert occurrences of `\n` back to platform-specific line endings. This behind-the-scenes modification to file data is fine for text files but will corrupt binary data like that in JPEG or EXE files. Be very careful to use binary mode when reading and writing such files.

It is good practice to use the `with` keyword when dealing with file objects. The advantage is that the file is properly closed after its suite finishes, even if an exception is raised at some point. Using with is also much shorter than writing equivalent `try-finally` blocks:

```python
>>> with open('workfile', encoding="utf-8") as f:
...     read_data = f.read()
>>> # We can check that the file has been automatically closed.
>>> f.closed
True
```

If you're not using the with keyword, then you should call `f.close()` to close the file and immediately free up any system resources used by it.

### 2.2 Methods of File Objects

The rest of the examples in this section will assume that a file object called f has already been created.

To read a file's contents, call `f.read(size)`, which reads some quantity of data and returns it as a string (in text mode) or bytes object (in binary mode). size is an optional numeric argument. When the size is omitted or negative, the entire contents of the file will be read and returned; it's your problem if the file is twice as large as your machine's memory. Otherwise, at most size characters (in text mode) or size bytes (in binary mode) are read and returned. If the end of the file has been reached, f.read() will return an empty string ('').

```python
>>> f.read()
'This is the entire file.\n'
>>> f.read()
''
```

`f.readline()` reads a single line from the file; a newline character (`\n`) is left at the end of the string and is only omitted on the last line of the file if the file doesn't end in a newline. This makes the return value unambiguous; if `f.readline()` returns an empty string, the end of the file has been reached, while a blank line is represented by '`\n`', a string containing only a single newline.

```python
>>> f.readline()
'This is the first line of the file.\n'
>>> f.readline()
'Second line of the file\n'
>>> f.readline()
''
```

For reading lines from a file, you can loop over the file object. This is memory efficient, fast, and leads to simple code:

```python
>>> for line in f:
...     print(line, end='')
...
This is the first line of the file.
Second line of the file
```

If you want to read all the lines of a file in a list you can also use `list(f)` or `f.readlines()`.

`f.write(string)` writes the contents of the string to the file, returning the number of characters written.

```python
>>> f.write('This is a test\n')
15
```

Other types of objects need to be converted – either to a string (in text mode) or a bytes object (in binary mode) – before writing them:

```python
>>> value = ('the answer', 42)
>>> s = str(value)  # convert the tuple to string
>>> f.write(s)
18
```

File objects have some additional methods, which we won't talk about for now.

---

## Summary

- formatting strings, which can be quite useful in output
- opening files, reading lines of a file

Next chapter: errors, exceptings, and handling those exceptions.
