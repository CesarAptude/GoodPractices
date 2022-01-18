# BestPractices
A guide for the best practices for Aptude team

# Table of Contents

  - [Iterating over Sequences and Mappings](#iterating-over-sequences-and-mappings)
      - [Anti-pattern](#anti-pattern)
      - [Best practice](#best-practice)
  - [Use enumerate when you need the element and its index at the same time](#use-enumerate-when-you-need-the-element-and-its-index-at-the-same-time)
      - [Bad practice](#bad-practice)
      - [Best practice](#best-practice-1)
  - [Use zip to iterate over pairs of lists](#use-zip-to-iterate-over-pairs-of-lists)
      - [Anti-pattern](#anti-pattern-1)
      - [Best practice](#best-practice-2)
  - [Comparing to Zero](#comparing-to-zero)
      - [Anti-pattern](#anti-pattern-2)
      - [Best practice](#best-practice-3)
  - [Use explicit variable names](#use-explicit-variable-names)
      - [Anti-pattern](#anti-pattern-3)
      - [Best practice](#best-practice-4)
  - [Using non-explicit variable names](#using-non-explicit-variable-names)
      - [Anti-pattern](#anti-pattern-5)
      - [Best practice](#best-practice-6)
  - [Use "set" to check if an element is contained in a (large) list](#use-set-to-check-if-an-element-is-contained-in-a-large-list)
      - [Anti-pattern](#anti-pattern-6)
      - [Best practice](#best-practice-7)
  - [Passing mutable default arguments to functions (i.e. an empty list)](#passing-mutable-default-arguments-to-functions-ie-an-empty-list)
      - [Anti-pattern](#anti-pattern-7)
      - [Best practice](#best-practice-8)
  - [Using stacked and nested if statements](#using-stacked-and-nested-if-statements)
      - [Bad practice](#bad-practice-1)
      - [Best practice](#best-practice-9)
  - [Use get() to return default values from a dictionary](#use-get-to-return-default-values-from-a-dictionary)
      - [Bad practice](#bad-practice-2)
      - [Best practice](#best-practice-10)
  - [Use try/except blocks that handle exceptions meaningfully](#use-tryexcept-blocks-that-handle-exceptions-meaningfully)
      - [Bad practice](#bad-practice-3)
      - [Best practice](#best-practice-11)
  - [from module import *](#from-module-import-)
      - [Bad practice](#bad-practice-4)
      - [Best practice](#best-practice-12)
  - [Over-engineering everything](#over-engineering-everything)
      - [Bad practice](#bad-practice-5)
      - [Best practice: a simple function is enough](#best-practice-a-simple-function-is-enough)

## Iterating over Sequences and Mappings

#### Anti-pattern
Use of range to iterate over a sequence

    >>> x = [1, 2, 4, 8, 16]
    >>> for i in range(len(x)):
    ...     print(x[i])
    ... 
    1
    2
    4
    8
    16

#### Best practice
A better way to iterate over a sequence

    >>> for item in x:
    ...     print(item)
    ... 
    1
    2
    4
    8
    16

## Use enumerate when you need the element and its index at the same time

#### Bad practice

    for i in range(len(list_of_fruits)):
        fruit = list_of_fruits[i]
        print(f"fruit number {i+1}: {fruit}")

#### Best practice

    for i, fruit in enumerate(list_of_fruits):
        print(f"fruit number {i+1}: {fruit}")

## Use zip to iterate over pairs of lists

#### Anti-pattern

    for i in range(len(list_of_letters)):
        letter = list_of_letters[i]
        id_ = list_of_ids[i]
        process_letters(letter, id_)
		
#### Best practice

    list(zip(list_of_letters, list_of_ids)) = [("A", 1), ("B", 2), ("C", 3)]

    for letter, id_ in zip(list_of_letters, list_of_ids):
        process_letters(letter, id_)

## Comparing to Zero
When you have numeric data, and you need to check if the numbers are equal to zero, you can but don’t have to use the comparison operators == and !=:

#### Anti-pattern

    >>> x = (1, 2, 0, 3, 0, 4)
    >>> for item in x:
    ...     if item != 0:
    ...         print(item)
    ... 
    1
    2
    3
    4
The Pythonic way is to exploit the fact that zero is interpreted as False in a Boolean context, while all other numbers are considered as True:

    >>> bool(0)
    False
    >>> bool(-1), bool(1), bool(20), bool(28.4)
    (True, True, True, True)
Having this in mind you can just use if item instead of if item != 0:
#### Best practice
    >>> for item in x:
    ...     if item:
    ...         print(item)
    ... 
    1
    2
    3
    4
You can follow the same logic and use if not item instead of if item == 0.

## Use explicit variable names

Your variables should always be descriptive to provide a minumum of context

#### Anti-pattern

    x = data[["f1", "f2", "f3"]]
    y = data["target"]

#### Best practice

    features = data[["f1", "f2", "f3"]]
    target = data["target"]

## Using non-explicit variable names

d = {"foo": 1}

#### Anti-pattern

    f = open("./data.csv", "wb")
    f.write("some data")

    v = d["bar"] # KeyError
f.close() never executes which leads to memory issues

    f.close()

#### Best practice

    with open("./data.csv", "wb") as f:
        f.write("some data")
        v = d["bar"]
python still executes f.close() even if the KeyError exception occurs

## Use "set" to check if an element is contained in a (large) list

Checking if an element is contained in a list using the in statement might be slow for large lists. Consider using set or bisect instead.

#### Anti-pattern
    list_of_letters = ["A", "B", "C", "A", "D", "B"]
    check = "A" in list_of_letters

#### Best practice
    set_of_letters = {"A", "B", "C", "D"}
    check = "A" in set_of_letters

## Passing mutable default arguments to functions (i.e. an empty list)

There is a thing in python that may result in silent errors and obscure bugs: default arguments are evaluated once when the function is defined, not each time the function is called.
This means that if you use a mutable default argument (such as a list) and mutate it, you will and have mutated that object for all future calls to the function as well.

#### Anti-pattern

    def append_to(element, to=[]):
        to.append(element)
        return to

    >>> my_list = append_to("a") 
    >>> print(my_list)
    >>> ["a"]

    >>> my_second_list = append_to("b") 
    >>> print(my_second_list)
    >>> ["a", "b"]

#### Best practice

    def append_to(element, to=None):
        if to is None:
            to = []
        to.append(element)
        return to

To avoid this issue, you can set the default argument toto None:
- if the function with called multiple times with to set to None, create a new empty list and append the element to it each time
- when you pass a list to to, you append an element to it. Since it's not the default function argument, this works well.

## Using stacked and nested if statements

Stacked and nested if statements make it hard to follow the code logic.

    user = "Emilio"
    age = 30
    job = "data scientist"

#### Bad practice

    if age > 30:
        if user == "Emilio":
            if job == "data scientist":
                access = True
            else:
                access = False

Instead of nesting conditions, you can combine them with Boolean operators.

#### Best practice

    access = age > 30 and user == "ahmed" and job == "data scientist"

## Use get() to return default values from a dictionary

When you use get, python checks if the specified key exists in the dictionary. If it does, then get() returns the value of that key. If the key doesn't exist, get() returns the value specified in the second argument.

    user_ids = {
        "John": 12,
        "Anna": 2,
        "Jack": 10
    }

#### Bad practice

    name = "Paul"

    if name in user_ids:
        user_id = user_ids[name]
    else:
        user_id = None

#### Best practice

    user_id = user_ids.get(name, None)

## Use try/except blocks that handle exceptions meaningfully

    user_ids = {"John": 12, "Anna": 2, "Jack": 10}
    user = "Paul"

Using a try/except block and ignoring the exception by passing it (for instance) should be avoided.

#### Bad practice

    try:
        user_id = user_ids[user]
    except:
        pass

#### Best practice

    try:
        user_id = user_ids[user]
    except KeyError:
        print("user id not found")

## from module import *

Imports should always be specific. Importing * from a module is a very bad practice that pollutes the namespace.

#### Bad practice

    from math import *
    x = ceil(x)

#### Best practice

    from math import ceil   
    x = ceil(x) # we know where ceil comes from

## Over-engineering everything

Essentially, a class is a way of grouping functions (as methods) and data (as properties) into a logical unit revolving around a certain kind of thing. If you don’t need that grouping, there’s no need to make a class.

#### Bad practice

    class Rectangle:
        def __init__(self, height, width):
            self.height = height
            self.width = width
        
        def area(self):
            return self.height * self.width

#### Best practice: a simple function is enough

    def area(height, width):
        return height * width

