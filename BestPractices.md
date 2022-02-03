# BestPractices
A guide for the best practices for Aptude team

# Table of Contents

  - [Explicit code](#explicit-code)
  - [Iterating over Sequences and Mappings](#iterating-over-sequences-and-mappings)
  - [Use enumerate when you need the element and its index at the same time](#use-enumerate-when-you-need-the-element-and-its-index-at-the-same-time)
  - [Use zip to iterate over pairs of lists](#use-zip-to-iterate-over-pairs-of-lists)
  - [Access a Dictionary Element](#access-a-dictionary-element)
  - [Short Ways to Manipulate Lists](#short-ways-to-manipulate-lists)
  - [Filtering a list](#filtering-a-list)
  - [Modifying the values in a list](#modifying-the-values-in-a-list)
  - [Comparing to Zero](#comparing-to-zero)
  - [Use explicit variable names](#use-explicit-variable-names)
  - [Using non-explicit variable names](#using-non-explicit-variable-names)
  - [Read a file in Python](#read-a-file-in-python)
  - [Line Continuations](#line-continuations)
  - [Use "set" to check if an element is contained in a (large) list](#use-set-to-check-if-an-element-is-contained-in-a-large-list)
  - [Passing mutable default arguments to functions (i.e. an empty list)](#passing-mutable-default-arguments-to-functions-ie-an-empty-list)
  - [Using stacked and nested if statements](#using-stacked-and-nested-if-statements)
  - [Use get() to return default values from a dictionary](#use-get-to-return-default-values-from-a-dictionary)
  - [Use try/except blocks that handle exceptions meaningfully](#use-tryexcept-blocks-that-handle-exceptions-meaningfully)
  - [from module import *](#from-module-import-)
  - [Over-engineering everything](#over-engineering-everything)


## Explicit code

While any kind of black magic is possible with Python, the most explicit and straightforward manner is preferred.

#### Anti-pattern

    def make_complex(*args):
        x, y = args
        return dict(**locals())

#### Best practice

    def make_complex(x, y):
        return {'x': x, 'y': y}

In the good code above, x and y are explicitly received from the caller, and an explicit dictionary is returned. The developer using this function knows exactly what to do by reading the first and last lines, which is not the case with the bad example.

## One statement per line

While some compound statements such as list comprehensions are allowed and appreciated for their brevity and their expressiveness, it is bad practice to have two disjointed statements on the same line of code.

#### Anti-pattern

    print('one'); print('two')

    if x == 1: print('one')

    if <complex comparison> and <other complex comparison>:
        # do something

#### Best practice

    print('one')
    print('two')

    if x == 1:
        print('one')

    cond1 = <complex comparison>
    cond2 = <other complex comparison>
    if cond1 and cond2:
        # do something

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

## Access a Dictionary Element

Don’t use the __dict.has_key()__ method. Instead, use ```x in d``` syntax, or pass a default argument to __dict.get()__.

#### Anti-pattern

    d = {'hello': 'world'}
    if d.has_key('hello'):
        print(d['hello'])    # prints 'world'
    else:
        print('default_value')

#### Best practice

    d = {'hello': 'world'}

    print(d.get('hello', 'default_value')) # prints 'world'
    print(d.get('thingy', 'default_value')) # prints 'default_value'

    # Or:
    if 'hello' in d:
        print(d['hello'])

## Short Ways to Manipulate Lists

List comprehensions provides a powerful, concise way to work with lists.

Generator expressions follows almost the same syntax as list comprehensions but return a generator instead of a list.

Creating a new list requires more work and uses more memory. If you are just going to loop through the new list, prefer using an iterator instead.

#### Anti-pattern

    # needlessly allocates a list of all (gpa, name) entires in memory
    valedictorian = max([(student.gpa, student.name) for student in graduates])

#### Best practice

    valedictorian = max((student.gpa, student.name) for student in graduates)

Use list comprehensions when you really need to create a second list, for example if you need to use the result multiple times.

If your logic is too complicated for a short list comprehension or generator expression, consider using a generator function instead of returning a list.

#### Best practice

    def make_batches(items, batch_size):
        """
        >>> list(make_batches([1, 2, 3, 4, 5], batch_size=3))
        [[1, 2, 3], [4, 5]]
        """
        current_batch = []
        for item in items:
            current_batch.append(item)
            if len(current_batch) == batch_size:
                yield current_batch
                current_batch = []
        yield current_batch

Never use a list comprehension just for its side effects.

#### Anti-pattern

    [print(x) for x in sequence]

#### Best practice

    for x in sequence:
        print(x)

## Filtering a list

#### Anti-pattern
Never remove items from a list while you are iterating through it.

    # Filter elements greater than 4
    a = [3, 4, 5]
    for i in a:
        if i > 4:
            a.remove(i)

Don’t make multiple passes through the list.

    while i in a:
        a.remove(i)

#### Best practice

Use a list comprehension or generator expression.

    # comprehensions create a new list object
    filtered_values = [value for value in sequence if value != x]

    # generators don't create another list
    filtered_values = (value for value in sequence if value != x)

### Possible side effects of modifying the original list
Modifying the original list can be risky if there are other variables referencing it. But you can use slice assignment if you really want to do that.

    # replace the contents of the original list
    sequence[::] = [value for value in sequence if value != x]

## Modifying the values in a list

#### Anti-pattern
Remember that assignment never creates a new object. If two or more variables refer to the same list, changing one of them changes them all.

    # Add three to all list members.
    a = [3, 4, 5]
    b = a                     # a and b refer to the same list object

    for i in range(len(a)):
        a[i] += 3             # b[i] also changes

#### Best practice
It’s safer to create a new list object and leave the original alone.

    a = [3, 4, 5]
    b = a

    # assign the variable "a" to a new list without changing "b"
    a = [i + 3 for i in a]

Use __enumerate()__ keep a count of your place in the list.

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

## Read a file in Python

### 1. Using open() function

A simple solution is to open the file in reading mode ```'r'``` using the built-in ```open()``` function. Since the mode in which the file is opened defaults to ```'r'```, you can skip it.

    f = open('file.txt')
    text = f.read()
    print(text)
    f.close()

The above syntax requires you to explicitly close the file using the close() function. This is not considered Pythonic, and you should use the with keyword, which automatically closes the file once it is done with, even when an exception is raised. Here’s an equivalent code using the with statement:

    with open('file.txt') as f:
        text = f.read()
        print(text)

### 2. Using pathlib module

You can also use the pathlib module with Python 3.4. The Path.read_text() function opens the file in text mode, reads it, and close the file.

    import pathlib
    text = pathlib.Path('file.txt').read_text()
    print(text)

### 3. Using io module

Finally, you can call the io.open() function, which is an alias for the built-in open() function.

    import io
    
    with io.open("file.txt", mode='r', encoding='utf-8') as f:
        text = f.read()
        print(text)

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

## Line Continuations

When a logical line of code is longer than the accepted limit, you need to split it over multiple physical lines. The Python interpreter will join consecutive lines if the last character of the line is a backslash. This is helpful in some cases, but should usually be avoided because of its fragility: a white space added to the end of the line, after the backslash, will break the code and may have unexpected results.

A better solution is to use parentheses around your elements. Left with an unclosed parenthesis on an end-of-line, the Python interpreter will join the next line until the parentheses are closed. The same behavior holds for curly and square braces.

    my_very_big_string = """For a long time I used to go to bed early. Sometimes, \
    when I had put out my candle, my eyes would close so quickly that I had not even \
    time to say “I’m going to sleep.”"""

    from some.deep.module.inside.a.module import a_nice_function, another_nice_function, \
    yet_another_nice_function

    my_very_big_string = (
        "For a long time I used to go to bed early. Sometimes, "
        "when I had put out my candle, my eyes would close so quickly "
        "that I had not even time to say “I’m going to sleep.”"
    )

    from some.deep.module.inside.a.module import (
        a_nice_function, another_nice_function, yet_another_nice_function)

However, more often than not, having to split a long logical line is a sign that you are trying to do too many things at the same time, which may hinder readability.

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

