---
title: "Python Tutorial: 7. Modules - Organizing Code"
author: "Tiexin Guo | 郭铁心"
authorLink: https://www.guotiexin.com
tags: ["python"]
categories: ["Python Tutorial"]
date: 2022-07-15
cover:
  image: "1200px-Python-logo.png"
  alt: "Python Tutorial"
---

## 0 Background

So far, we've been coding in the Python interpreter, which if we quit and re-enter, the functions and variables definitions we've made previously are lost.

Therefore, if you want to write a somewhat longer program, you'd be better off using a text editor to prepare the input for the interpreter and running it with that file as input instead - which is known as creating a script.

As your program gets longer, you may want to split it into several files for easier maintenance. You may also want to use a handy function that you've written in several programs without copying its definition into each program.

This is where the Python module kicks in.

---

## 1 Module

A module is a file containing Python definitions and statements. The file name is the module name with the suffix `.py` appended. Within a module, the module's name (as a string) is available as the value of the global variable `__name__`.

Each file can be a module, and definitions from a module can be imported into other modules or the main module.

For instance, use your favorite text editor (VIM or VSCode?) to create a file called `fibo.py` in the current directory with the following contents:

```python
def fib(n):    # write Fibonacci series up to n
    a, b = 0, 1
    while a < n:
        print(a, end=' ')
        a, b = b, a+b
    print()


def fib2(n):   # return Fibonacci series up to n
    result = []
    a, b = 0, 1
    while a < n:
        result.append(a)
        a, b = b, a+b
    return result
```

Now if we start the Python interpreter from the directory where the `fibo.py` is located, we can import it and call the functions defined in it:

```python
>>> import fibo
>>> fibo.fib(1000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987
>>> fibo.fib2(100)
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
>>> fibo.__name__
'fibo'
```

---

## 2 More on Modules

A module can contain _executable statements_ (besides function definitions.)

These statements are intended to initialize the module. They are executed _only the first time the module name is encountered in an import statement, and they are also run if the file is executed as a script._

Modules can import other modules.

It is customary (but not required) to place all import statements at the beginning of a module (or script, for that matter).

There is a variant of the `import` statement that imports certain names from a module only, directly, instead of importing the module:

```python
>>> from fibo import fib, fib2
>>> fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
```

This does not introduce the module name (so in the example, `fibo` is not defined.)

There is even a variant to import all names that a module defines:

```python
>>> from fibo import *
>>> fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
```

The "*" means to import all names, but _do not use this_ since it introduces an unknown set of names and causes poorly readable code. (It is okay to use it to save typing in interactive sessions, though.)

If the module name is followed by `as`, then it acts as if the name of the module is changed:

```python
>>> import fibo as fib
>>> fib.fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
```

This is effectively importing the module in the same way that import fibo will do, with the only difference of it being available as fib.

It can also be used when utilizing `from` with similar effects:

```python
>>> from fibo import fib as fibonacci
>>> fibonacci(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
```

---

## 3 Executing modules as scripts

When you run a Python module with

`python fibo.py <arguments>`

the code in the module will be executed, just as if you imported it, but with the `__name__` set to "__main__" (instead of 'fibo' which is the file/module name). That means that by adding this code at the end of your module:

```
if __name__ == "__main__":
    import sys
    fib(int(sys.argv[1]))
```

you can make the file usable as a script as well as an importable module because the code that parses the command line only runs if the module is executed as the “main” file:

```
$ python fibo.py 50
0 1 1 2 3 5 8 13 21 34
```

If the module is imported, the code is not run:

```python
>>> import fibo
```

This is often used either to provide a convenient user interface to a module, or for testing purposes (running the module as a script executes a test suite).

---

## 4 Standard Modules

Python comes with a library of standard modules which provide access to operations that are not part of the core of the language but are nevertheless built in, either for efficiency or to provide access to operating system primitives such as system calls.

One particular module deserves some attention: `sys`, which is built into every Python interpreter:

```python

>>> import sys
>>> sys.maxsize
9223372036854775807
```

---

## 5 The `dir()` Function

The built-in function `dir()` is used to find out which names a module defines:

```python
>>> import fibo, sys
>>> dir(fibo)
['__name__', 'fib', 'fib2']
>>> dir(sys)  
['__breakpointhook__', '__displayhook__', '__doc__', '__excepthook__',
 '__interactivehook__', '__loader__', '__name__', '__package__', '__spec__',
 '__stderr__', '__stdin__', '__stdout__', '__unraisablehook__',
 '_clear_type_cache', '_current_frames', '_debugmallocstats', '_framework',
 '_getframe', '_git', '_home', '_xoptions', 'abiflags', 'addaudithook',
 'api_version', 'argv', 'audit', 'base_exec_prefix', 'base_prefix',
 'breakpointhook', 'builtin_module_names', 'byteorder', 'call_tracing',
 'callstats', 'copyright', 'displayhook', 'dont_write_bytecode', 'exc_info',
 'excepthook', 'exec_prefix', 'executable', 'exit', 'flags', 'float_info',
 'float_repr_style', 'get_asyncgen_hooks', 'get_coroutine_origin_tracking_depth',
 'getallocatedblocks', 'getdefaultencoding', 'getdlopenflags',
 'getfilesystemencodeerrors', 'getfilesystemencoding', 'getprofile',
 'getrecursionlimit', 'getrefcount', 'getsizeof', 'getswitchinterval',
 'gettrace', 'hash_info', 'hexversion', 'implementation', 'int_info',
 'intern', 'is_finalizing', 'last_traceback', 'last_type', 'last_value',
 'maxsize', 'maxunicode', 'meta_path', 'modules', 'path', 'path_hooks',
 'path_importer_cache', 'platform', 'prefix', 'ps1', 'ps2', 'pycache_prefix',
 'set_asyncgen_hooks', 'set_coroutine_origin_tracking_depth', 'setdlopenflags',
 'setprofile', 'setrecursionlimit', 'setswitchinterval', 'settrace', 'stderr',
 'stdin', 'stdout', 'thread_info', 'unraisablehook', 'version', 'version_info',
 'warnoptions']
```

Without arguments, `dir()` lists the names you have defined currently:

```python
>>> a = [1, 2, 3, 4, 5]
>>> import fibo
>>> fib = fibo.fib
>>> dir()
['__builtins__', '__name__', 'a', 'fib', 'fibo', 'sys']
```

> Note that it lists all types of names: variables, modules, functions, etc.

---

## 6 Packages

Packages are a way of structuring Python's module namespace by using “dotted module names”. For example, the module name `A.B` designates a submodule named `B` in a package named `A`.

For example: if we create a directory named "my_package", then under it, we have two sub-directories "package1", and "package2", then we have two modules under each package:

```shell
my_package/                     Top-level package
├── package1                    Subpackage 1
│   ├── module1.py
│   └── module2.py
└── package2                    Subpackage 2
    ├── module1.py
    └── module2.py
```

If we define a "hello" function in package1.module1:

```python
def hello():
    print("Hello from package 1 module 1")
```

We can start the Python interpreter under the directory where my_package is defined:

```python
>>> from my_package.package1.module1 import hello
>>> hello()
Hello from package 1 module 1
>>>
```

### 6.1 Intra-package References

When packages are structured into sub-packages (as with the "package1" package in the example), you can use _absolute_ imports to refer to submodules of siblings packages. For example, if the code in module `package1.module1` needs to use the `package1.module2`, it can use `import module2`:

### 6.2 Packages in Multiple Directories

If the code in `package2.module1` wants to import `package1.module1`, write: `import package1.module1`.

---

## Summary

Packages, modules, `__main__`, `dir()`, `import`... many details today. Make sure you practice!

In the next chapter, we will try to learn a little bit about input/output and error handling.
