---
title: "Python Tutorial: How to Learn Everything"
author: "Tiexin Guo | 郭铁心"
authorLink: https://www.guotiexin.com
tags: ["python"]
categories: ["Python Tutorial"]
date: 2022-06-27
cover:
  image: "1200px-Python-logo.png"
  alt: "Python Tutorial"
---

## 0 How to Learn Everything

No matter what you've already known, chances are, there are still things that you don't know.

Learning Python isn't drastically different.

We've already learned quite a few basics in Python, but there is a lot of stuff we don't know yet.

Until now.

Because today, we will learn "how to learn everything," and we will learn by an example, which is to read Excel files with Python.

Without further adieu, let's dive right into it.

---

## 1 Manipulating Excel with Python

To be completely honest, I might have done this before, but I don't remember how. To you, maybe you've never done this in your entire life. But hey, that's completely fine.

Let's google it up: "[python read excel file](https://www.google.com/search?q=python+read+excel+file)".

Based on the [first result](https://pythonbasics.org/read-excel/), it seems we need something named `xlrd` and `pandas`.

Based on the [second result](https://pandas.pydata.org/docs/reference/api/pandas.read_excel.html), it seems `pandas` explicitly has a function named "read_excel". Excellent, just what we need.

## 2 Experimenting with Pandas

Let's give this `pandas` thing a try first; after all, it appears in the first two search results, although at this point we've got absolutely no idea what it is and what it can do.

The aforementioned two results aren't newbie-friendly, though: they don't have code that I can copy-paste directly.

Let's open up the third and the [fourth one](https://datagy.io/pandas-read-excel/), OK, there we can find complete code that we can copy. Let's do this in an [Virtual ENV](../python-code-organization#1-virtual-env):

```sh
python3 -m venv venv
. ./venv/bin/activate
pip install pandas
```

Then we copy-paste the code we found:

`main.py`:

```python
import pandas as pd

df = pd.read_excel('test.xlsx')

print(df)
```

(Of course, you need to prepare an Excel file named test.xlsx.)

Easy. Let's run it now:

```sh
python main.py
```

But we got an error:

```sh
ImportError: Missing optional dependency 'openpyxl'.  Use pip or conda to install openpyxl.
```

OK, it seems we need the `openpyxl` dependency but we don't have it. No idea what it is, but let's install it:

```sh
pip install openpyxl
```

Run it again, and now we can read the Excel. Easy as that.

To sum up, we need the following to handle Excel files with Python:

- pandas
- openpyxl

---

## 3 Digging Deeper: What's "pandas", Anyway?

Now that we've seem `pandas` in action, it's time to know what's `pandas`. At this time, we don't know what it is yet, but we do know that a simple [google search](https://www.google.com/search?q=python+pandas) will yield thousands of results, and you would most likely find the [official website](https://pandas.pydata.org/) as the first result.

According to the official introduction, it seems "pandas is a fast, powerful, flexible and easy to use open-source data analysis and manipulation tool, built on top of the Python programming language." TL;DR: it handles data. And based on the experiment we did above, it's safe to infer that `pandas` can handle data in Excel format, too.

It seems we have solved our problem, Right? Except we haven't. Let's take a minute and examine the example above: we printed the whole Excel file content out, which is utterly useless. We might as well open it with Microsoft Excel. Our program isn't extremely useful, is it.

OK, let's try to do something cool with it.

Let's say, I want to read the whole excel into a dictionary, each row being a record in the dict, the first cell of which being the key and the remaining cells being the value.

Why? Because putting the entire data into a dictionary would definitley be useful. I know that! Think of a payroll Excel table: if we can get a person's base salary, bonus, vacations this month, etc., by his name (or employee ID, for that matter,) we can write a simple piece of program to calculate his monthly pay, automate human resource processes and fire all those HRs, right? (No.)

But how the heck can we do that?

Let's google the same: "[python pandas to dict](https://www.google.com/search?q=python+pandas+to+dict)" and the first two results showed us exactly how to do this: `pd.to_dict()`. After reading more examples and documentation in the search results, we can easily update our `main.py` in an copy-paste fashion to the following:

```python
from operator import index
from typing import Hashable
import pandas as pd

df = pd.read_excel('test.xlsx')

print(df.to_dict("data"))
```

If we read the `pandas` `read_excel` and `to_dict` documentation, we would find a lot of interesting quirks and features. Maybe you can give it a glance so that you have a vague idea of what it can do. Or not. When you need to achieve another functionality, google again. Why remember things if they are only one google search away?

---

## 4 Too Easy for Me

If you think this article is too easy, think again.

Yes, we didn't have a clue of what we can do in the beginning, and after merely a few searches, we copy-pasted some code and made it work. Seems easy, right? But the hard part is how you decide to do the whole thing:

- know what you need
- know what keywords you want to search
- identify useful results quickly from this [datageddon](https://www.youtube.com/watch?v=YPgkSH2050k)
- learn from those results and put'em into action

This, my friend, is [the analytic knife of Phaedrus](https://en.wikipedia.org/wiki/Zen_and_the_Art_of_Motorcycle_Maintenance): "classical thinking," I.E., thinking like a scientist, systematically and analytically, and making decisions based on that.
