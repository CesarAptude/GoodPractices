# PEP 8 Style Guide

Python Enhancement Proposal 8 or PEP 8 is a comprehensive styling guide for your Python code. PEP 8’s aim is to bring all Python together under one styling guide. This increases the readability and overall understanding of Python code. PEP 8 is not always meant to be followed in every circumstance. You will run into code that just doesn’t apply and if so then you may need to break away from the style guide for a short instance. The key is the use the style guide whenever you can though. It will help you and everyone else that lay eyes on your code read it and work on it. I will cover the areas that I feel are most important. I will not be going over some areas and others, I may just go over skim over. I really recommend reading PEP 8 in full, as this guide is meant more as a quick overview. To really understand and get more in-depth explanations, as well as parts I have chosen to not include in this article. The sections of PEP 8 I will be going over are as follows:
- Code Lay-out
- Strings
- Whitespace
- Trailing Commas
- Comments
- Naming Conventions
- Recommendations

PEP 8 can be found here:
PEP 8 -- Style Guide for Python Code
The official home of the Python Programming Language
www.python.org

## Code Lay-out
### Indentation:
- 4 Spaces, although this is up to you on continuation lines, as long as there is some form of indentation.
- You can line up wrapped elements in parentheses vertically or with a hanging indent.

        # 4 space indent
        def hello(var):
            print(var)
        # vertical alignment
        example2 = function(first_var, second_var,
                            third_Var, fourth_var)
        # hanging indent
        example3 = function(
            first_var, second_var,
            third_var, fourth_var)

1. You can use similar workflows for conditionals that either go too long or you want to be a continuation line. You can use parenthesis after a two-character keyword will allow the indentation to be automatic when going to a new line. This can be useful for long conditional statements, such as an ```if``` statement. For nested statements you can choose to have no extra indentation, comment your indentation details, or add extra indentation.
2. You can line the closing punctuation (brace, bracket, or parenthesis) up with the first character of the last line or the first character that starts the multiline expression that is not whitespace.

        # last line, first character
        new_list = [
            'one', 'two', 'three',
            'four', 'five', 'six'
            ]
        # first line, first character
        new_list = [
            'one', 'two', 'three',
            'four', 'five', 'six'
        ]

### Tabs & Spaces
1. Spaces are recommended for indentation, whereas tabs are used to keep yourself uniform with code that is using tabs to indent.
2. Python will not allow you to use both in the same code. If you are converting Python 2 that has a mix of both, redo with spaces.

### Maximum Line Length
1. Max line length should be 79 characters long, although I find this restrictive sometimes and must go longer in those cases. In situations like this it is okay to go up to 99 characters.
2. For comments and docstrings you should use 72 characters and should not be increased.
3. This helps when reading Python code and keeping it in editor, review, and debugging tools.
4. To help you stay on track Python has a helper for this. You can wrap your lines in parentheses starting with everything past the first keyword and ending before the next keyword. This is advised by PEP 8 and will auto-wrap your lines according to correct Python line styling format.
5. Backslashes can also be used, only when the parentheses wrapping does not apply, such as ```assert``` statements.

### Line Breaks with Binary Operators
1. You should line break before binary operators for more readability, although this has been opposite in the past and both are acceptable if they are consistent.

### Blank Lines
1. Two blank lines should be both before and after class definitions.
2. One blank line should be both before and after method definitions.
3. You should use blank lines conservatively within your code to separate groups of functions.
4. You do not have to include blank lines between different lines if those lines are each only a line of code separate from each other.
5. Python uses the control-L (^L) form feed character for whitespace.

### Source File Encoding
1. Code should use UTF-8 for the core Python 3 distribution (ASCII for Python 2) and should not have declarations.
2. Encodings outside of these should only be used for test purposes.
3. Jump over to PEP 3131 for more info on this policy.
4. Identifiers should be ASCII-only and English words should be used when they can be.

### Imports
1. Imports usually do not have blank lines separating them.
2. Imports usually should be separated on different lines unless using the ```from``` keyword.
3. Imports belong at the top of your code after comments & docstrings and before your globals and constants.
4. Imports should be in this order.
   - Standard Library
   - Third Party
   - Local / Library Specific.
5. Absolute imports are recommended, but explicit relative imports are perfectly fine. Whichever is less verbose.
6. Import classes from separate class modules.
7. Wildcard imports (```*```) should not be used unless necessary.
8. Module level “dunders” are names with two trailing underscores. These names should be placed after the comments and docstrings, but before imports.
9. ```from __future__``` imports must be before any code other than comments and docstrings.

### Strings
1. Single quotes around your strings or double quotes around your string mean the same thing. You can choose what one you like more, but stick to it so you can use the alternative you didn’t choose instead of backslashes.
2. Triple quotes should use double quote characters. Check out PEP 257.

### Whitespace
Avoid Trailing Whitespace.

1. Do not use excessive whitespace in your expressions and statements. You should have blank spaces after commas, colons, and semi-colons if it isn’t trailing next to the end of a bracket, brace, or parentheses.
2. With any operators you should use a space in on both sides of the operator. Colons for slicing are considered a binary operator, and should not have any spaces between them.
3. You should have parentheses with no space, directly next to the function when calling functions ```function()```.
4. when indexing or slicing the brackets should be directly next to the collection with no space ```collection[‘index’]```.
5. Whitespace used to line up variable values is not recommended.
6. Make sure you are consistent with the formats you choose when optional choices are available.

### Trailing Commas
1. The only time a trailing comma is necessary is when you are making a single element Tuple.
2. If you do use trailing commas, use parenthesis to surround them.
3. Trailing commas are used often in Version Control to detail which areas are going to be expanded upon later.

### Comments
1. Make sure your comments make sense and are useful for reading the code. Comments that are counter-productive may hurt code readability.
2. Make sure to update your comments when you update your code.
3. Make sure your comments are easy to understand for other Python programmers.
4. Block comments are a paragraph or more of single line comments ending in an end punctuation for each line. They should start with a # and then a space. Also, block comments should be indented to the same amount that the code they are going to is indented. Separate paragraphs by a single comment line with nothing in it.
5. In multi-line comments use two spaces after the sentence period, except only use one space after the final sentence.
6. Inline comments are comments that follow your code on the same line. Inline comments are to be used conservatively. They should be separated by at least two spaces following your code. They are to be used only when necessary.
7. Docstrings or Documentation Strings do exactly what they state. They give documentation to modules, functions, classes, and methods. You should have Docstrings for all the following. Docstrings are created by using triple ```“””``` quotations at the beginning and end of the Docstring. To learn more about Docstrings look at PEP 257.

### Naming Conventions
Although Python has some inconsistencies in the Python library with naming conventions, it is still recommended to use current naming conventions, unless what you are working with has a different convention already, then use that format.
Overriding Principle is where you should reflect usage rather than implementation for your public aspects of your APIs.
There are multiple Naming Styles you can choose from. Remember to be descriptive. You can also use prefixes to group names together.

        b  
        B  
        lowercase  
        lower_case_underscore
        UPPERCASE
        UPPER_CASE_UNDERSCORE
        CamelCase
        mixedCase
        Cap_words_Underscore # not recommended 

### Prescriptive Naming Conventions
- Single leading underscore: weak and not recommended unless for internal use.
- Single ending underscore: used to avoid issues with Python keywords.
- Double leading underscore: for naming class attributes.
- Double leading and trailing underscores are “magic" objects or attributes in the user’s namespace.
#### Names to avoid:

        # try not to use.
        l  # lowercase L
        O  # uppercase o
        I  # uppercase i

### ASCII Compatibility:
- Identifiers are required to be ASCII compatible for the standard library.
### Package and Module Names:
- Packages and Modules should have lowercase and short names if possible.
- Modules can have underscores.
- Packages should not have underscores.
- If a module is in C or C++ and is associated to a Python module, that creates a higher interface and can be named with a leading underscore.

### Class Names:
Use Capital Words Convention ```WordExample```.
You may use function naming conventions if it is well documented and is mainly used to be a callable.
Built-in names are usually a single word or two words long. They also only use the Capital Words Convention for exceptions and built-in constants.

### Type Variable Names:
- Type variables should use Capital Words Convention and short names.
- Suffix ```_co``` for variables with covariant behavior.
- Suffix ```_contra``` for variables with contravariant behavior.

### Exception Names:
- Use Class naming conventions.
- Suffix ```Error``` used for exception names that error.

### Global Variable Names:
- Follow Function naming conventions.
- ```__all__``` mechanism should be used to prevent globals caused by ```from M import *``` or use like the prefix ```globals```.

### Function & Variable Names:
- Functions and Variables should be lowercase with underscores.
- You can adobe a mixedCase tyle if it is already what is being used.

### Function & Method Arguments:
- Include ```self``` as a first argument to instant methods.
- Include ```cls``` or the first argument to class methods.
- Better to use trailing underscore if needed then abbreviations.

### Method Names & Instance Variables:
- Use Function naming conventions.
- Use leading underscores for non-public methods and instance variables.
- You can use two leading underscores if necessary, to use Python’s name mangling.

### Constants:
- UPPERCASE Naming Convention with underscores.

### Inheritance:
- Make sure your class’s attributes are either public or non-public.
- Non-public attributes are ones not designed for third parties.
- “private” is a term used in Python.
- “subclass API” (aka. “protected”). Designed to be inherited from. Base classes.
- Public attributes = no leading underscores, unless keyword conflicts.
- Expose only attribute names for public data attributes.
- subclassed classes can be named with double leading underscores, to use Python’s name mangler.

## Public and Internal Interfaces
- Users should be able to tell the difference between public and internal interfaces.
- If an interface is documented it is considered public, unless stated otherwise in the docs.
- Undocumented interfaces are internal.
- Modules should use ```__all__``` to declare the public API. if ```__all__``` is set to a blank list, it says there is no public API.
- Single leading underscore for internal interfaces.
- If any namespace is internal, then the interface is internal.
- Imports are an implementation detail.

### Recommendations
1. Write code so it doesn’t negatively affect other implementations of Python.
2. ```is``` or ```is not``` to compare singletons.
3. ```is``` not and not ```not is```.
4. Use ```def``` as opposed to assignment when binding lambda expressions to identifiers.
5. For exceptions use ```Exception``` instead of ```BaseException```.
6. Make sure your exception chaining is being used correctly.
7. Be specific ```with``` exceptions when you can.
8. Use explicit name binding syntax.
9. Use explicit exception hierarchy on operating system errors.
10. When using ```try``` and ```except```, keep your code as tight around the area that needs to be wrapped in the try block.
11. Use with statements on local resources.
12. Make sure you use ```return``` statements correctly. Either have ```return``` expressions or don’t.
13. String methods as opposed to the string module.
14. Use methods ```.startswith()``` and ```.endswith()``` for string prefix and suffix slicing.
15. Use ```isinstance(<item>, <item>)``` as opposed to ```if type(<item>) is type(<item>)```.
16. Empty sequences are considered ```False```.
17. Don’t use ```==``` for ```True``` ```False``` comparisons.
18. Flow control statements should be inside ```finally``` code blocks.