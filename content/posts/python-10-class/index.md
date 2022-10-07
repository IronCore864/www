---
title: "Python Tutorial: 10. Class"
author: "IronCore"
authorLink: https://www.guotiexin.com/
tags: ["python"]
categories: ["Python Tutorial"]
date: 2022-07-20
cover:
  image: "1200px-Python-logo.png"
  alt: "Python Tutorial"
---

## 0 OOP and Classes

To talk about class, we need to talk about Object-oriented programming (OOP) first.

OOP is a programming paradigm based on the concept of "objects", which can contain data and code: data in the form of _fields_ (often known as _attributes_ or _properties_), and code, in the form of _procedures_ (often known as _methods_).

The class provides a way of bundling data and functionality together. Creating a new class creates a new _type_ of object, allowing new _instances_ of that type to be made.

Each class instance can have attributes attached to it for maintaining its state. Class instances can also have methods (defined by their class) for modifying their state.

---

## 1 A First Look at Classes

Classes introduce something new in Python: a little bit of new syntax,
some new object types, and some new semantics.

Let's go over them meticulously:

### 1.1 Class Definition Syntax

The simplest form of class definition looks like this:

```python
class ClassName:
    <statement-1>
    ...
    <statement-N>
```

Class definitions, like function definitions (`def` statements,) must be executed before they have any effect.

In practice, the statements inside a class definition will usually be function definitions, but other statements are allowed, and sometimes useful — we'll come back to this later.

The function definitions inside a class normally have a peculiar form of the argument list, dictated by the calling conventions for methods — again, this will be explained later.

### 1.2 Class Objects

Class objects support two kinds of operations:
- attribute references
- instantiation

_Attribute references_ use the standard syntax used for all attribute references in Python: `obj.name`. So, if the class definition looked like this:

```python
class MyClass:
    """A simple example class"""
    i = 12345

    def f(self):
        return 'hello world'
```

then `MyClass.i` and `MyClass.f` are valid attribute references, returning an integer and a function object, respectively.

_Class instantiation_ uses function notation.

_Pretend that the class object is a parameterless function that returns a new instance of the class_.

For example (assuming the above class):

```python
x = MyClass()
```

creates a new instance of the class and assigns this object to the local variable `x`.

The instantiation operation (“calling” a class object) creates an empty object.

Many classes like to create objects with instances customized to a specific initial state. Therefore, a class may define a special method named `__init__()`, like this:

```python
def __init__(self):
    self.data = []
```

When a class defines an `__init__()` method, class instantiation automatically invokes `__init__()` for the newly created class instance. So in this example, a new, initialized instance can be obtained by:

```python
x = MyClass()
```

Of course, the `__init__()` method may have arguments for greater flexibility. In that case, arguments given to the class instantiation operator are passed on to `__init__()`. For example,

```python
>>> class Complex:
...     def __init__(self, realpart, imagpart):
...         self.r = realpart
...         self.i = imagpart
...
>>> x = Complex(3.0, -4.5)
>>> x.r, x.i
(3.0, -4.5)
```

### 1.3 Instance Objects

What can we do with instance objects? The only operations understood by instance objects are attribute references.

There are two kinds of valid attribute names:

- data attributes
- methods

Data attributes need not be declared; like local variables, they spring into existence when they are first assigned to.

For example, if `x` is the instance of `MyClass` created above, the following piece of code will print the value 16, without leaving a trace:

```python
x.counter = 1
while x.counter < 10:
    x.counter = x.counter * 2
print(x.counter)
del x.counter
```

The other kind of instance attribute reference is a method. _A method is a function that “belongs to” an object_.

In our example, `x.f` is a valid method reference, since `MyClass.f` is a function; but `x.i` is not, since `MyClass.i` is not. But `x.f` is not the same thing as `MyClass.f` — which is a method object, not a function object.

### 1.4 Method Objects

Calling a method:

```python
x.f()
```

In the `MyClass` example, this will return the string 'hello world'.

What exactly happens when a method is called? You may have noticed that `x.f()` was called without an argument above, even though the function definition for `f()` specified an argument. What happened to the argument? You may have guessed the answer: the special thing about methods is that the _instance object_ is passed as the first argument of the function automatically. (In general, calling a method with a list of `n` arguments is equivalent to calling the corresponding function with an argument list that is created by inserting the method's instance object before the first argument.)

### 1.5 Class and Instance Variables

Instance variables are for data unique to each instance, and class variables are for attributes and methods shared by all instances of the class.

```python
class Dog:
    kind = 'canine'         # class variable shared by all instances

    def __init__(self, name):
        self.name = name    # instance variable unique to each instance
```

```python
>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.kind                  # shared by all dogs
'canine'
>>> e.kind                  # shared by all dogs
'canine'
>>> d.name                  # unique to d
'Fido'
>>> e.name                  # unique to e
'Buddy'
```

Shared data (class variables) can have possibly surprising effects involving mutable objects such as lists and dictionaries. For example, the `tricks` list in the following code should not be used as a class variable because just a single list would be shared by all Dog instances:

```python
class Dog:
    tricks = []             # mistaken use of a class variable

    def __init__(self, name):
        self.name = name

    def add_trick(self, trick):
        self.tricks.append(trick)
```

```python
>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.add_trick('roll over')
>>> e.add_trick('play dead')
>>> d.tricks                # unexpectedly shared by all dogs
['roll over', 'play dead']
```

The correct design of the class should use an instance variable instead:

```python
class Dog:
    def __init__(self, name):
        self.name = name
        self.tricks = []    # creates a new empty list for each dog

    def add_trick(self, trick):
        self.tricks.append(trick)
```

```python
>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.add_trick('roll over')
>>> e.add_trick('play dead')
>>> d.tricks
['roll over']
>>> e.tricks
['play dead']
```

---

## 2 Inheritance

One of the OOP programming paradigms is inheritance.

The syntax for a derived class definition looks like this:

```python
class DerivedClassName(BaseClassName):
    <statement-1>
    ...
    <statement-N>
```

Derived classes may override the methods of their base classes. An overriding method in a derived class may in fact want to extend rather than simply replace the base class method of the same name. There is a simple way to call the base class method directly: `BaseClassName.methodname(self, arguments)`.

---

## 3 Abstract Class

An abstract class can be considered a "blueprint" for other classes. It allows you to create a set of methods that must be created within any child classes built from the abstract class.

A class that contains one or more abstract methods is called an abstract class. An abstract method is a method that has a declaration but does not have an implementation.
  
Why use Abstract Base Classes?

By defining an abstract base class, you can define a common _Application Program Interface_ (API) for a set of subclasses. This capability is especially useful in situations where other people/a third-party is going to provide implementations, but can also help you when working in a large team or with a large code-base where keeping all classes in your mind is difficult or not possible. 
  
Here is an example of how to create abstract classes:

```python
from abc import ABC, abstractmethod


class Polygon(ABC):
    @abstractmethod
    def number_of_sides(self):
        pass


class Triangle(Polygon):
    def number_of_sides(self):
        print("I have 3 sides")


class Pentagon(Polygon):
    def number_of_sides(self):
        print("I have 5 sides")


class Hexagon(Polygon):
    def number_of_sides(self):
        print("I have 6 sides")


a = Triangle()
a.number_of_sides()


b = Pentagon()
b.number_of_sides()

c = Hexagon()
c.number_of_sides()
```

Notes:
- To create an abstract class, we first need to import `ABC` and `abstractmethod` from module `abc`.
- An abstract class needs to extend `ABC`.
- An abstract method should have an annotation `@abstractmethod`.
- The abstract method doesn't need to be implemented, so putting a statement `pass` in the method's body is enough.
- Child classes that inherit the abstract base class need to implement those methods which are annotated as `@abstractmethod`.

---

## 4 Putting It All Together

This is a simplified version of the written test for DevStream junior engineers:

> Write a program of "animals", which does the following:
> 
> - Each animal has a name(unique) and can only be either a `cow`, `bird`, or `snake`.
> - The user can request information about an animal (see the example and expected output below.)
> 
> The following table contains the three types of animals and their associated data:
> 
> | Animal Type | Eat   | Move    | Speak |
> |-------------|-------|---------|-------|
> | cow         | grass | walk    | moo   |
> | bird        | worms | fly     | peep  |
> | snake       | mice  | slither | hsss  |

Now, let's solve it.

It seems we should have a class "Animal", which has three methods:
- eat
- move
- speak

And there are three types of animals:
- cow
- bird
- snake

Each type can have multiple "instances", and each instance has its name.

All animals should have the eat, move, and speak methods.

Based on this description, it seems we need:

- an abstract class for "Animal", which has three abstract methods: eat, move, speak;
- three classes for three types: cow, bird, and snake, and they should all inherit the abstract class "Animal" and implement the abstract classes;
- class cow/bird/snake should have a name for each of its instances.

First, let's define the abstract class:

```python
from abc import ABC, abstractmethod


class Animal(ABC):
    def __init__(self, name):
        self.name = name

    @abstractmethod
    def eat(self):
        pass

    @abstractmethod
    def move(self):
        pass

    @abstractmethod
    def speak(self):
        pass
```

Then, let's implement the three classes for each type of animal:

```python

class Cow(Animal):
    def eat(self):
        print("grass")

    def move(self):
        print("walk")

    def speak(self):
        print("moo")


class Bird(Animal):
    def eat(self):
        print("worms")

    def move(self):
        print("fly")

    def speak(self):
        print("peep")


class Snake(Animal):
    def eat(self):
        print("mice")

    def move(self):
        print("slither")

    def speak(self):
        print("hsss")
```

With these definitions, let's try it out:

```python
a = Bird("tweety")
print(a.name) # tweety
a.eat()       # worms
a.move()      # fly
a.speak()     # peep

b = Snake("snakey")
print(b.name) # snakey
b.eat()       # mice
b.move()      # slither
b.speak()     # hsss
```

---

## 5 Iterators

By now, you have probably noticed that most _container_ objects can be looped over using a for statement:

```python
for element in [1, 2, 3]:
    print(element)
for element in (1, 2, 3):
    print(element)
for key in {'one':1, 'two':2}:
    print(key)
for char in "123":
    print(char)
for line in open("myfile.txt"):
    print(line, end='')
```

This style of access is clear, concise, and convenient. The use of iterators pervades and unifies Python.

Behind the scenes, the for statement calls `iter()` on the container object. The function returns an iterator object that defines the method `__next__()` which accesses elements in the container one at a time. When there are no more elements, `__next__()` raises a `StopIteration` exception which tells the for loop to terminate. You can call the `__next__()` method using the `next()` built-in function; this example shows how it all works:

```python
>>> s = 'abc'
>>> it = iter(s)
>>> it
<str_iterator object at 0x10c90e650>
>>> next(it)
'a'
>>> next(it)
'b'
>>> next(it)
'c'
>>> next(it)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
    next(it)
StopIteration
```

Having seen the mechanics behind the iterator protocol, it is easy to add iterator behavior to your classes. Define an `__iter__()` method which returns an object with a `__next__()` method. If the class defines `__next__()`, then `__iter__()` can just return self:

```python
class Reverse:
    """Iterator for looping over a sequence backwards."""
    def __init__(self, data):
        self.data = data
        self.index = len(data)

    def __iter__(self):
        return self

    def __next__(self):
        if self.index == 0:
            raise StopIteration
        self.index = self.index - 1
        return self.data[self.index]
```

```python
>>> rev = Reverse('spam')
>>> iter(rev)
<__main__.Reverse object at 0x00A1DB50>
>>> for char in rev:
...     print(char)
...
m
a
p
s
```

---

## 6 Generators

Generators are a simple and powerful tool for creating iterators.

To create a generator, you write it like a regular function but use the `yield` statement whenever you want to return data. Each time `next()` is called on it, the generator resumes where it left off (it remembers all the data values and which statement was last executed).

An example shows that generators are easy to create:

```python
def reverse(data):
    for index in range(len(data)-1, -1, -1):
        yield data[index]
```

```python
>>> for char in reverse('golf'):
...     print(char)
...
f
l
o
g
```

Anything that can be done with generators can also be done with class-based iterators as described in the previous section. What makes generators so compact is that the `__iter__()` and `__next__()` methods are created automatically.

---

## 7 Generator Expressions

Some simple generators can be coded succinctly as expressions using a syntax similar to list comprehensions but with parentheses `()` instead of square brackets `[]`. We have mentioned it a little bit in the previous sections.

Generator expressions are more compact but less versatile than full generator definitions and tend to be more memory friendly than equivalent list comprehensions.

Examples:

```python
>>> sum(i*i for i in range(10))                 # sum of squares
285
>>> xvec = [10, 20, 30]
>>> yvec = [7, 5, 3]
>>> sum(x*y for x,y in zip(xvec, yvec))         # dot product
260

>>> unique_words = set(word for line in page for word in line.split())

>>> valedictorian = max((student.gpa, student.name) for student in graduates)

>>> data = 'golf'
>>> list(data[i] for i in range(len(data)-1, -1, -1))
['f', 'l', 'o', 'g']
```

---

## Summary

Today is all about classes: inheritance, abstract classes.

We also looked at a concrete example to demo the usage of classes.

We also introduced iterators and generators so that you can create a class which can be iterated using a `for` loop.

In the next chapter, we will go over virtual environments (again) and packages, so that you can work on multiple projects on your laptop and write programs at a larger scale.
