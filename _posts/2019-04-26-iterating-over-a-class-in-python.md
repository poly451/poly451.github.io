---
layout: post
title: "Iterating Over a Class in Python"
date: 2019-04-26
---

Today, I'm going to talk about iteration.
SO MANY TIMES I've had to examine every element of a list. Usually I do something like this:

>for a_car in a_list_of_cars:
    >>if a_car == Mustang:
        >>>Ford = True
        
Or something marginally more useful ...

For a_character in all_characters:
    if a_character.name == "Guenda"
        a_character.charisma += 5
        
... but you get the idea.

OKAY. But let's say you're writing an RPG and you have a class, Swords, and within that class one of your instance variables is implemented as a list.

Let's say that it's a list of swords and you want to select the one called 'Old Glory.'

Within the class this is simple, just do something like:

my_sword.name = "Rusty Wonder"
    for a_sword in all_swords:
        if a_sword.name = "Old Glory":
            my_sword = a_sword

But let's say that your class, Swords, is used in another class: Weapons. Le's say your character wants to select a weapon. You might write:

for a_weapon in all_weapons:
    if a_weapon.quality == 3 and a_weapon == sword:
        return a_weapon

But if you run this, you'll get an error. Something like:

[Error]

The Problem:
As we've seen, Python will throw up an error if you try to iterate over one of your classes (Swords) from another class (Weapons).


The Solution:
Write your own __iter__ and __next__ functions.[1] It's easy! Here's the code:



class Someclass
    def __init__(self, a_list):
        self.i = 0
        self.a_list = a_list
        
    def __iter__(self):
        return self

    def ____next____(self):
        if self.i < len(self.a_lost):
            self.i = self.i + 1
            return self.a_list[self.i-1]
        else:
            raise StopIteration

Now run the program again. No errors!

Another Problem: Len() [List error that happens, use that as the header.]


But we're not finished! There's more we could do. Let's look at len(). Let's say that we want to know how many swords we have as weapons. So we want to do something like this:



class Weapons

....

def number_of_weapons(self):

    return len(self.swords) + len(self.daggers) + len(self.flamethrowers)



You'll get the error:



[list error]



Good news! The fix is easy. In class Swords just include:



def __len__(self):

    return len(self.a_list)

It works!! But, wait! We're not done yet.

Indexing: It's a good thing
Let's say you're debugging and you want a function in class Swords to return a sword, any sword, so you write:



def return_first_sword(self):

    return self.swords[0]



When you run this you get the error:



[list error]



The Solution
Write code for the functions:[2]



__getitem__

__setitem__

__delitem__



def __getitem__(self)



def __delitem__(self, i):

    new_list = []

    for counter, item in enumerate(self.a_list):

        if counter==i:

            pass

        else:

            new_list.append(item)

    self.a_list = new_list



That's it!



I know my code isn't the most elegant, so if anyone would like to suggest a revision--or an addition!--please leave a comment or email me at: c (dot) strange (dot) 451 (at) gmail.com.

References:


1. Thanks to alecxe [https://stackoverflow.com/users/771848/alecxe] and Martin Pieters [https://stackoverflow.com/users/100297/martijn-pieters] for their comments on the post: "Object is not iterable" error on my python implementation of iterable" over at stackoverflow.com. [https://stackoverflow.com/questions/18506144/object-is-not-iterable-error-on-my-python-implementation-of-iterable]



2. Thanks to Omkar Pathak and his article, "Using Python __getitem__ and __setitem__" [https://www.omkarpathak.in/2018/04/11/python-getitem-and-setitem/].








Well. Finally got around to putting this old website together. Neat thing about it - powered by [Jekyll](http://jekyllrb.com) and I can use Markdown to author my posts. It actually is a lot easier than I thought it was going to be.
