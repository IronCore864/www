---
title: "Python Tutorial: 3. Flow Control"
author: "Tiexin Guo | 郭铁心"
authorLink: https://www.guotiexin.com
tags: ["python"]
categories: ["Python Tutorial"]
date: 2022-07-11

cover:
  image: "1200px-Python-logo.png"
  alt: "Python Tutorial"
---

In the [previous tutorial](../python-02-informal-intro/), we demonstrated the `while` statement, which is a "flow control" statement.

> In computer programming, _control flow_ or _flow of control_ is the order function calls, instructions, and statements are executed or evaluated when a program is running.

In Python (as in most other programming languages,) there are more usual flow control statements than just `while`.

---

## 1 `if` Statements

The most well-known flow control statement probably is the `if` statement. Example:

```python
>>> x = int(input("Please enter an integer: "))
Please enter an integer: 42
>>> if x < 0:
...     x = 0
...     print('Negative changed to zero')
... elif x == 0:
...     print('Zero')
... elif x == 1:
...     print('Single')
... else:
...     print('More')
...
More
```

_Notes:_

- There can be _0 or more_ `elif` parts.
- The `else` part is _optional_.
- The keyword ‘elif’ is short for ‘else if’, and is useful to avoid excessive indentation. For example:

```python
if x < 0:
    x = 0
    print('Negative changed to zero')
elif x == 0:
    print('Zero')
```

is equivalent to:

```python
if x < 0:
    x = 0
    print('Negative changed to zero')
else:
    if x == 0:
        print('Zero')
```

---

## 2 `for` Statements

Used for _loops_.

> A loop is a sequence of instructions that is continually repeated (indefinitely, or until a certain condition is reached.)

In Python, you can use `for` to:

- loop over an arithmetic progression of numbers;
- iterates over the items of any sequence (a list or a string), in the order that they appear in the sequence.

Examples:

```python
>>> # Measure some strings:
... words = ['cat', 'window', 'defenestrate']
>>> for w in words:
...     print(w, len(w))
...
cat 3
window 6
defenestrate 12
```

_Code that modifies a collection while iterating over that same collection can be tricky to get right._ For example:

```python
# Create a sample collection
users = {'Hans': 'active', 'Éléonore': 'inactive', '景太郎': 'active'}

# Strategy:  Iterate over a copy
for user, status in users.items():
    if status == 'inactive':
        del users[user]
```

Run the code above, and you will get an error "RuntimeError: dictionary changed size during iteration".

So, it is usually a good practice not to modify something while you are iterating over it. If you have to, a more straightforward way is to loop over a copy of the collection or to create a new collection:

```python
# Create a sample collection
users = {'Hans': 'active', 'Éléonore': 'inactive', '景太郎': 'active'}

# Strategy1:  Iterate over a copy
for user, status in users.copy().items():
    if status == 'inactive':
        del users[user]

# Strategy2:  Create a new collection
active_users = {}
for user, status in users.items():
    if status == 'active':
        active_users[user] = status
```

---

## 3 The `range()` Function

If you need to iterate over a sequence of numbers, the built-in function `range()` comes in handy.

It generates arithmetic progressions:

```python
>>> for i in range(5):
...     print(i)
...
0
1
2
3
4
```

The ending point is never part of the generated sequence; `range(5)` generates 5 values, starting from 0, and ending at 4; 5 is not included. This acts similarly like substring indexes and slices mentioned in the previous tutorial. Python is consistent.

It is possible to let the range start at another number, or to specify a different increment (even negative; sometimes this is called the _step_):

```python
>>> list(range(5, 10))
[5, 6, 7, 8, 9]

>>> list(range(0, 10, 3))
[0, 3, 6, 9]

>>> list(range(-10, -100, -30))
[-10, -40, -70]
```

To iterate over the indices of a sequence, you can combine `range()` and `len()` as follows:

```
>>> a = ['Mary', 'had', 'a', 'little', 'lamb']
>>> for i in range(len(a)):
...     print(i, a[i])
...
0 Mary
1 had
2 a
3 little
4 lamb
```

However, in cases like these, it is convenient to use the `enumerate()` function:

```python
a = ['Mary', 'had', 'a', 'little', 'lamb']
for i, word in enumerate(a):
    print(i, word)
```

If you print a range, a strange thing happens:

```python
>>> range(10)
range(0, 10)
```

In many ways, the object returned by `range()` behaves as if it is a list, except it isn’t. It is an "object" which returns the successive items of the desired sequence when you iterate over it, but it doesn't really create the list, thus saving memory.

> We say such an object is _iterable_, that is, suitable as a target for functions and constructs that expect something from which they can obtain successive items until the supply is exhausted. We have seen that the `for` statement is such a construct, while an example of a function that takes an iterable is `sum()`:

```python
# sum a list
>>> sum([0, 1, 2, 3])
# sum a range, which isn't a list, but an _iterable_
>>> sum(range(4))  # 0 + 1 + 2 + 3
6
```

Note that `range(4)` isn't a list, but the function `sum()` can support _iterable_ input, not only lists, so the above code works.

---

## 4 `break`, `continue` Statements, and `else` on Loops

The `break` statement breaks out of the innermost enclosing loop (when there are loop inside a loop, only the loop closest to the `break` is broken out of.)

Loop statements may have an `else` clause; it is executed when the loop terminates through exhaustion of the iterable (with `for`) or when the condition becomes false (with `while`), but _not when the loop is terminated by a `break` statement_. Example:

```python
>>> for n in range(2, 10):
...     for x in range(2, n):
...         if n % x == 0:
...             print(n, 'equals', x, '*', n//x)
...             break
...     else:
...         # loop fell through without finding a factor
...         print(n, 'is a prime number')
...
2 is a prime number
3 is a prime number
4 equals 2 * 2
5 is a prime number
6 equals 2 * 3
7 is a prime number
8 equals 2 * 4
9 equals 3 * 3
```

In this example, we demonstrated:
- nested loop
- breaking out of the innner loop
- the `else` clause belongs to the inner `for` loop, not the `if` statement (not many people know you can use `else` with a for loop :)

---

## 5 `pass` Statements

The `pass` statement does _nothing_.

It can be used when a statement must exist but the program doesn't have to do anything there. For example:

```python
>>> while True:
...     pass  # does nothing, the loop will only stop when you press Ctrl+C
```

Why does it exist? It is commonly used for place-holders for some part of code you must write later, allowing you to keep thinking at a more abstract level:

```python
>>> def initlog(*args):
...     pass   # Remember to implement this!
...
```

---

## 6 `match` Statements

A match statement takes an _expression_ and compares its value to successive patterns given as one or more case blocks. If no case matches, none of the branches is executed.

It acts like multiple `if`/`elif`.

Note that only the first pattern that matches gets executed and it can also extract components (sequence elements or object attributes) from the value into variables.

Example:

```python
def http_error(status):
    match status:
        case 400:
            return "Bad request"
        case 404:
            return "Not found"
        case 418:
            return "I'm a teapot"
        case _:
            return "Something's wrong with the internet"
```

> The last block: the `_` acts as a "wildcard" (matches everything and never fails to match.)

You can combine several literals in a single pattern using `|` (which means "or"):

```python
case 401 | 403 | 404:
    return "Not allowed"
```

---

## Summary

After reading this tutorial, you should be able to use:

- if/elif/else
- for
- range
- break/continue
- pass
- match

In the next chapter, we will talk about "functions."
