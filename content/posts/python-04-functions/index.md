---
title: "Python Tutorial: 4. Functions"
author: "IronCore"
authorLink: https://www.guotiexin.com/
tags: ["python"]
categories: ["Python Tutorial"]
date: 2022-07-12

cover:
  image: "1200px-Python-logo.png"
  alt: "Python Tutorial"
---

## 1 Defining Functions

We can create a _function_ that writes the Fibonacci series to an arbitrary boundary (if you have forgotten about the Fibonacci series, refer to the [second tutorial](../python-02-informal-intro/)):

```python
>>> def fib(n):    # write Fibonacci series up to n
...     a, b = 0, 1
...     while a < n:
...         print(a, end=' ')
...         a, b = b, a+b
...     print()
...
>>> # Now call the function we just defined:
... fib(2000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597
```

- The keyword `def` introduces a function definition.
- `def` must be followed by the function name, then the parenthesized list of parameters.
- The statements that form the body of the function start at the next line and must be indented.

A word on variable scope: when using a variable, Python will first look if the variable is defined inside the function, if not, then look for it in the outer scope, and then the global scope.

It is simple to write a function that returns a list of the numbers of the Fibonacci series, instead of printing it:

```python
>>> def fib2(n):  # return Fibonacci series up to n
...     """Return a list containing the Fibonacci series up to n."""
...     result = []
...     a, b = 0, 1
...     while a < n:
...         result.append(a)    # see below
...         a, b = b, a+b
...     return result
...
>>> f100 = fib2(100)    # call it
>>> f100                # write the result
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
```

Some explanation about the example above:

- The `return` statement returns with a value from a function.
- The statement `result.append(a)` calls a method of the list object result. A method is a function that "belongs" to an object.
- The function returns a list.

---

## 2 Default Parameter Value

We can specify a default value for parameters. This creates a function that can be called with fewer parameters than it is defined. For example:

```python
def ask_ok(prompt, retries=4, reminder='Please try again!'):
    while True:
        ok = input(prompt)
        if ok in ('y', 'ye', 'yes'):
            return True
        if ok in ('n', 'no', 'nop', 'nope'):
            return False
        retries = retries - 1
        if retries < 0:
            raise ValueError('invalid user response')
        print(reminder)
```

This function can be called in several ways:

- giving only the mandatory parameter: `ask_ok('Do you really want to quit?')`
- giving one of the optional parameters: ``ask_ok('OK to overwrite the file?', 2)`
- or even giving all parameters: `ask_ok('OK to overwrite the file?', 2, 'Come on, only yes or no!')`

This example also introduces the `in` keyword. `in` tests whether or not a sequence contains a certain value.

For example:

```python
def find_needle_in_hay(list_of_nums, nums_to_be_found):
    if nums_to_be_found in list_of_nums:
        return "Found!"


print(find_needle_in_hay([1, 2, 3], 3)) # prints "Found!"
```

---

## 3 Keyword Parameter

Functions can also be called using keyword parameters. For instance, the following function:

```python
def parrot(voltage, state='a stiff', action='voom', type='Norwegian Blue'):
    print("-- This parrot wouldn't", action, end=' ')
    print("if you put", voltage, "volts through it.")
    print("-- Lovely plumage, the", type)
    print("-- It's", state, "!")
```

accepts one required parameter (voltage) and three optional parameters (state, action, and type). This function can be called in any of the following ways:

```python
parrot(1000)                                          # 1 positional parameter
parrot(voltage=1000)                                  # 1 keyword parameter
parrot(voltage=1000000, action='VOOOOOM')             # 2 keyword parameters
parrot(action='VOOOOOM', voltage=1000000)             # 2 keyword parameters
parrot('a million', 'bereft of life', 'jump')         # 3 positional parameters
parrot('a thousand', state='pushing up the daisies')  # 1 positional, 1 keyword
```

but all the following calls would be invalid:

```python
parrot()                     # required parameter missing
parrot(voltage=5.0, 'dead')  # non-keyword parameter after a keyword parameter
parrot(110, voltage=220)     # duplicate value for the same parameter
parrot(actor='John Cleese')  # unknown keyword parameter
```

---

## 4 Coding Style

Now that you are about to write longer, more complex pieces of Python code, it is a good time to talk about coding style.

Most languages can be written (or more concise, formatted) in different styles; some are more readable than others. Making it easy for others to read your code is always a good idea, and adopting a nice coding style helps tremendously for that.

For Python, the "PEP8" style has emerged as the style guide that most projects adhere to; it promotes a very readable and eye-pleasing coding style. Every Python developer should read it at some point; here are the most important points from PEP8 extracted for you:

- Use 4-space indentation and no tabs.
- 4 spaces are a good compromise between small indentation (allows greater nesting depth) and large indentation (easier to read). Tabs introduce confusion and are best left out.
- Write shorter lines, make sure a single line don't exceed 79 characters.
- Use blank lines to separate functions and classes, and larger blocks of code inside functions.
- When possible, put comments on a line of their own.
- Use spaces around operators and after commas, but not directly inside bracketing constructs: `a = f(1, 2) + g(3, 4)`.
- Name your classes and functions consistently; the convention is to use `UpperCamelCase` for classes and `lowercase_with_underscores` for functions and methods. Always use `self` as the name for the first method parameter.

---

## Summary

Today, we learned about functions and coding styles. Tomorrow, we will look at data structure.
