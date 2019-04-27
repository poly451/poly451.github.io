---
layout: post
title: "Iterating Over a Class in Python"
date: 2019-04-26
---
# Iteration and Custom Classes
Today, I'm going to talk about iteration.
SO MANY TIMES I've had to examine every element of a list. Usually I do something like:

```python
for a_car in a_list_of_cars:
    if a_car == Mustang:
        Ford = True
```

Or something marginally more useful ...

For a_character in all_characters:
    if a_character.name == "Guenda"
        a_character.charisma += 5
        
... but you get the idea.

OKAY. But let's say you're writing an RPG and you have a class, Swords, and within that class one of your instance variables is implemented as a list.

Let's say that it's a list of swords and you want to select the one called 'Old Glory.'

Within the class this is simple, just do something like:

```python
my_sword.name = "Rusty Wonder"
    for a_sword in all_swords:
        if a_sword.name = "Old Glory":
            my_sword = a_sword
```

So far, go good. But let's not stop there. Let's say your class, Swords, is used in another class: Weapons, and let's say your character wants to select a weapon. You might write:

```python
for a_weapon in all_weapons:
    if a_weapon.quality == 3 and a_weapon == sword:
        return a_weapon
```

But if you run this, you'll get the error. 

>TypeError: 'Swords' object is not iterable

## The Problem:
As we've seen, Python will throw up an error if you try to iterate over one of your classes (Swords) from somewhere outside that class.

## The Solution:
Write your own `__iter__` and `__next__` functions. It's easy! Here's the code:


```python
class Someclass
    def __init__(self, a_list):
        self.i = 0
        self.a_list = a_list
        
    def __iter__(self):
        return self

    def __next__(self):
        if self.i < len(self.a_lost):
            self.i = self.i + 1
            return self.a_list[self.i-1]
        else:
            raise StopIteration
```
Also, add `self.i = 0` to `__init__`.

Now run the program. It *should* be error free.

## Another Problem: `len()` doesn't work

We're not finished! Let's look at `len()`. Let's say that we want to know how many swords we have as weapons so we write something like this (by the way, if you want to look at the tutorial program I've written for this article, here's a [link to my github repo](https://github.com/poly451/Tutorials)):


```python
class Weapons
....
def number_of_weapons(self):
    return len(self.swords) + len(self.daggers) + len(self.flamethrowers)
```

You'll get the error:

> TypeError: object of type 'Swords' has no len()

Well, good news! The fix is easy. In class Swords just include:

```python
def __len__(self):
    return len(self.a_list)
```

It works!! But we're not done yet.

## Indexing: It's a good thing
Let's say you're debugging and you want a function in class Swords to return a sword, any sword, so you write:

```python
def return_first_sword(self):
    return self.swords[0]
```

When you run this you get the error:

> TypeError: 'Swords' object does not support indexing

## The Solution
Write code for the functions:

```python
__getitem__

__setitem__

__delitem__
```

```python
    def __getitem__(self, item):
        if item >= 0 and item < len(self.all_swords):
            return self.all_swords[item]
        else:
            raise ValueError

    def __setitem__(self, key, value):
        if key >= 0 and key < len(self.all_swords):
            self.all_swords[key] = value
        else:
            raise ValueError

    def __delitem__(self, key):
        new_list = []
        counter = 0
        if key >= 0 and key < len(self.all_swords):
            for each_sword in self.all_swords:
                if counter == key:
                    pass
                else:
                    new_list.append(each_sword)
                counter += 1
            self.all_swords = new_list
        else:
            raise ValueError    
```

That's it!

I know my code isn't the most elegant, so if anyone would like to suggest a revision--or an addition!--please leave a comment or email: c (dot) strange (dot) 451 (at) gmail.com.

## References:
* Thanks to [alecxe](https://stackoverflow.com/users/771848/alecxe) and [Martin Pieters](https://stackoverflow.com/users/100297/martijn-pieters) for their comments on the post: ["Object is not iterable" error on my python implementation of iterable](https://stackoverflow.com/questions/18506144/object-is-not-iterable-error-on-my-python-implementation-of-iterable).

* Thanks to Omkar Pathak and his article, [Using Python __getitem__ and __setitem__](https://www.omkarpathak.in/2018/04/11/python-getitem-and-setitem/).
