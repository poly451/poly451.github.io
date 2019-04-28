---
layout: exp01
title: "Experimenting with css sheets"
date: 2019-04-26
---
## Iteration and Custom Classes
Today, I'm going to talk about iteration.
SO MANY TIMES I've had to examine every element of a list. Usually I do something like:

```python
for a_car in a_list_of_cars:
    if a_car == Mustang:
        Ford = True
```

Or something marginally more useful ...

```python
For a_character in all_characters:
    if a_character.name == "Guenda"
        a_character.charisma += 5
```

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
