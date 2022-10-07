---
title: "Python Tutorial: 11. Virtual Environments and Managing Packages with Pip"
author: "IronCore"
authorLink: https://www.guotiexin.com/
tags: ["python"]
categories: ["Python Tutorial"]
date: 2022-07-21
cover:
  image: "1200px-Python-logo.png"
  alt: "Python Tutorial"
---

Python apps and programs will often use packages and modules that don't come as part of the standard library (stuff that is included in Python).

Apps will sometimes need a specific version of a library, because the app may require that a particular bug has been fixed or the app may be written using an obsolete version of the library's interface.

This means it may not be possible for one Python installation to meet the requirements of every project. If project A needs version 1.0 of a particular module but project B needs version 2.0, the requirements conflict, and installing either version 1.0 or 2.0 will leave one app unable to run.

The solution for this problem is to create a _virtual environment_: a self-contained directory tree that contains a Python installation for a particular version of Python, plus several additional packages.

Different projects and apps and programs can then use different virtual environments.

To resolve the earlier example of conflicting requirements, project A can have its virtual environment with version 1.0 installed while project B has another virtual environment with version 2.0. If project B requires a library to be upgraded to version 3.0, this will not affect project A's environment.

## 1 Creating a Virtual ENV


There are multiple choices for creating a virtual environment in Python.

The most famous ones probably are:

- `virtualenv`
- `venv`

We choose `venv` here because it's shipped with Python 3 already.

To create a virtual environment, decide upon a directory where you want to place it, and run the `venv` module as a script with the directory path:

```bash
python3 -m venv .venv
```

This will create the `.venv` (doesn't have to be this name, usually people would use `venv` or `.venv` or `virtualenv` or something similar) directory if it doesn't exist, and also create directories inside it containing a copy of the Python interpreter and various supporting files.

`.venv` is a common directory location for a virtual environment because this name keeps the directory hidden.

Once you've created a virtual environment, you may activate it.

```bash
source .venv/bin/activate
# or
. .venv/bin/activate
# the first dot works as the source command
```

Activating the virtual environment will change your shell's prompt to show what virtual environment you're using, and modify the environment so that running python will get you that particular version and installation of Python. For example:

```bash
tiexin@mbp ~/work/test $ . .venv/bin/activate
(.venv) tiexin@mbp ~/work/test $
```

---

## 2 Managing Packages and Dependencies with Pip

You can install, upgrade, and remove packages using a program called `pip`.

`pip` has many subcommands: “install”, “uninstall”, “freeze”, etc.

You can install the latest version of a package by specifying a package's name:

```bash
(.venv) tiexin@mbp ~/work/test $ pip install novas
Collecting novas
  Downloading novas-3.1.1.5.tar.gz (135 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 135.3/135.3 kB 1.3 MB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
Using legacy 'setup.py install' for novas, since package 'wheel' is not installed.
Installing collected packages: novas
  Running setup.py install for novas ... done
Successfully installed novas-3.1.1.5
```

If you re-run this command, `pip` will notice that the requested version is already installed and do nothing.

Some useful commands of `pip`:

- `pip uninstall` followed by one or more package names will remove the packages from the virtual environment.
- `pip show` will display information about a particular package:
- `pip list` will display all of the packages installed in the virtual environment:
- `pip freeze` will produce a similar list of the installed packages, but the output uses the format that pip install expects. A common convention is to put this list in a `requirements.txt` file:

```bash
(.venv) tiexin@mbp ~/work/test $ pip freeze > requiremenets.txt
(.venv) tiexin@mbp ~/work/test $ cat requiremenets.txt
novas==3.1.1.5
(.venv) tiexin@mbp ~/work/test $ pip install -r requiremenets.txt
Requirement already satisfied: novas==3.1.1.5 in ./.venv/lib/python3.9/site-packages (from -r requiremenets.txt (line 1)) (3.1.1.5).
```

Conventionally, we name the file `requirements.txt`. Other users can use your `requirements.txt` file to install all necessary packages:

```
(.venv) $ python -m pip install -r requirements.txt
```

---

## Summary

This section is useful when you create multiple projects and don't want them to interfere with each other. It's also a good practice to always use a virtual environment (instead of the default Python interpreter that comes with your macOS by default.)

In the next chapter, we will look at a real-world example to put all we learned together.
