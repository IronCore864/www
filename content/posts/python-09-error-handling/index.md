---
title: "Python Tutorial: 9. Error Handling"
author: "Tiexin Guo | 郭铁心"
authorLink: https://www.guotiexin.com
tags: ["python"]
categories: ["Python Tutorial"]
date: 2022-07-19
cover:
  image: "1200px-Python-logo.png"
  alt: "Python Tutorial"
---

We have only slightly mentioned error messages. If you have tried out some of the code examples yourself, I'm pretty sure you've met a few more errors and exceptions. Today, we will go over errors in general.

There are (at least) two distinguishable kinds of errors:

- syntax errors
- exceptions

---

## 1 Syntax Errors

Syntax errors, also known as _parsing errors_, are caused by incorrect syntax, or _grammar_.

They are perhaps the most common kind of complaints you get while you are learning Python:

```python
>>> while True print('Hello world')
  File "<stdin>", line 1
    while True print('Hello world')
                   ^
SyntaxError: invalid syntax
```

The parser repeats the offending line and displays a little 'arrow' pointing at the earliest point in the line where the error was detected.

The error is caused by (or at least detected at) the token preceding the arrow. In the example above, the error is detected at the function `print()`, since a colon (`:`) is missing before it.

File name and line number are printed so you know where to look in case the input came from a script. It's extremely important to learn to figure out where went wrong and why, because that's all you do when programming.

---

## 2 Exceptions

Even if a statement or expression is syntactically correct, it may cause an error when an attempt is made to execute it.

_Errors detected during execution are called exceptions_ and are not always "fatal" in every condition. You will soon learn how to handle exceptions in Python.

Most exceptions are not handled by programs, however, and result in error messages as shown here:

```python
>>> 1/0
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero
>>> 4 + spam*3
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'spam' is not defined
>>> '2' + 2
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can only concatenate str (not "int") to str
```

The last line of the error message indicates what happened.

Exceptions come in different _types_, and the type is printed as part of the message.

The types in the example are ZeroDivisionError, NameError, and TypeError. 

The rest of the line provides detail based on the type of exception and what caused it.

---

## 3 Handling Exceptions

It is possible to write programs that handle selected exceptions.

Read the following example, which asks the user for input until a valid integer has been entered, but allows the user to interrupt the program (using Control-C or whatever the operating system supports.)

Note that a user-generated interruption is signaled by raising the KeyboardInterrupt exception:

```python
>>> while True:
...     try:
...         x = int(input("Please enter a number: "))
...         break
...     except ValueError:
...         print("Oops!  That was no valid number.  Try again...")
...
```

The try statement works as follows:
- The `try` clause (the statement(s) between the try and except keywords) is executed.
- If no exception occurs, the except clause is _skipped_ and execution of the try statement are finished.
- If an exception occurs during the execution of the `try` clause, _the rest of the clause is skipped_. Then, if the exception's type matches the exception named after the `except` keyword, the `except` clause is executed, and _then execution continues after the try/except block_.
- If an exception occurs that _does not match the exception named in the `except` clause_, it is _passed on_ to outer `try` statements (if there is); if no outer `try` handler is found, it is an _unhandled exception_, and execution stops.

It's worth noting that a `try` statement may have _more than one_ `except` clause, to specify handlers for different exceptions. _At most one handler will be executed_. Handlers only handle exceptions that occur in the corresponding `try` clause, not in other handlers of the same `try` statement.

An `except` clause may name multiple exceptions as a parenthesized tuple, for example:

```python
... except (RuntimeError, TypeError, NameError):
...     pass
```

The `try … except` statement has an optional `else` clause, which, when present, must follow all except clauses. It is useful for code that must be executed if the try clause does not raise an exception. For example:

```python
for arg in sys.argv[1:]:
    try:
        f = open(arg, 'r')
    except OSError:
        print('cannot open', arg)
    else:
        print(arg, 'has', len(f.readlines()), 'lines')
        f.close()
```

The use of the `else` clause is better than adding additional code to the try clause because it avoids accidentally catching an exception that wasn't raised by the code being protected by the `try … except` statement.

Exception handlers don't just handle exceptions if they occur immediately in the try clause, but also if they occur inside functions that are called (even indirectly) in the try clause. For example:

```
>>> def this_fails():
...     x = 1/0
...
>>> try:
...     this_fails()
... except ZeroDivisionError as err:
...     print('Handling run-time error:', err)
...
Handling run-time error: division by zero
```

---

## 4 Raising Exceptions

The raise statement allows the programmer to force a specified exception to occur. For example:

```python
>>> raise NameError('HiThere')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: HiThere
```

The sole argument to raise indicates the exception to be raised. This must be either an exception instance or an exception class (a class that derives from Exception). If an exception class is passed, it will be implicitly instantiated by calling its constructor with no arguments:

```python
raise ValueError  # shorthand for 'raise ValueError()'
```

If you need to determine whether an exception was raised but don't intend to handle it, a simpler form of the raise statement allows you to re-raise the exception:

```python
>>> try:
...     raise NameError('HiThere')
... except NameError:
...     print('An exception flew by!')
...     raise
...
An exception flew by!
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
NameError: HiThere
```

---

## 5 Exception Chaining

The raise statement allows an optional form that enables chaining exceptions. Syntax:

```python
# exc must be exception instance or None.
raise RuntimeError from exc
```

This can be useful when you are transforming exceptions. Example:

```python
>>> def func():
...     raise ConnectionError
...
>>> try:
...     func()
... except ConnectionError as exc:
...     raise RuntimeError('Failed to open database') from exc
...
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
  File "<stdin>", line 2, in func
ConnectionError

The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "<stdin>", line 4, in <module>
RuntimeError: Failed to open database
```

---

## 6 User-defined Exceptions

It's possible to create your type of exceptions. At the moment, only knowing this is more than enough; we won't put it into practical use any time soon.

---

## 7 Clean-up Actions

The `try` statement has another optional clause that is intended to define _clean-up actions_ that _must be executed under all circumstances_. For example:


```python
>>> try:
...     raise KeyboardInterrupt
... finally:
...     print('Goodbye, world!')
...
Goodbye, world!
KeyboardInterrupt
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
```

If a `finally` clause is present, the `finally` clause will execute as the last task before the try statement completes. The `finally` clause runs whether or not the try statement produces an exception.

Just remember, the `finally` clause will always be executed, no matter if there is an exception or not.

For example:

```python
>>> def bool_return():
...     try:
...         return True
...     finally:
...         return False
...
>>> bool_return()
False
```

A more complicated example:

```python
>>> def divide(x, y):
...     try:
...         result = x / y
...     except ZeroDivisionError:
...         print("division by zero!")
...     else:
...         print("result is", result)
...     finally:
...         print("executing finally clause")
...
>>> divide(2, 1)
result is 2.0
executing finally clause
>>> divide(2, 0)
division by zero!
executing finally clause
>>> divide("2", "1")
executing finally clause
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 3, in divide
TypeError: unsupported operand type(s) for /: 'str' and 'str'
```

As you can see, the `finally` clause is executed in any event. (The TypeError raised by dividing two strings is not handled by the except clause and therefore re-raised after the `finally` clause has been executed.)

---

## 8 Predefined Clean-up Actions

Some objects define standard clean-up actions to be executed when the object is no longer needed, regardless of whether or not the operation using the object succeeded or failed.

Read the following example, which tries to open a file and print its contents to the screen:

```python
for line in open("myfile.txt"):
    print(line, end="")
```

The problem with this code is that it leaves the file open for an indeterminate amount of time after this part of the code has finished executing. This is not an issue in simple scripts but can be a problem for larger applications.

The `with` statement allows objects like files to be used in a way that ensures they are always cleaned up promptly and correctly.

```python
with open("myfile.txt") as f:
    for line in f:
        print(line, end="")
```

After the statement is executed, the file `f` is always closed, even if a problem was encountered while processing the lines. It's always a good practice to open a file with the `with` statement like the example above. If you have forgotten about how to open and read a file, check the [previous tutorial](../python-08-input-output/).

---

## Summary

Congratulations, because for now, we've covered all the basics of Python. Let's take a quick look at what we've learned so far:

- interactive mode
- data types: numbers, strings, lists, 
- flow control: while loop, for loop, if/elif/else, etc.
- functions
- data types: more about lists: list comprehension, tuple, sequences, stack, queue
- data types: set, dict, loop through dicts
- modules
- input/output, read files
- handling errors

These are more than enough to start working on any small programs.

In the following chapters, we will cover:
- a little bit about class (which you don't have to use);
- using third-party modules to help you achieve what you want;
- managing different environments (if you are working on multiple projects, this can be useful;)
- how to learn everything.

Please give the previous chapters a quick review before moving on. See you in the next chapter!
