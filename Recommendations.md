## Recommendations of Python Coding Practices for Python Developers
So, here come some important best practices for Python Coding that you should always keep in mind.

### 1. Create a Code Repository and Implement Version Control
If you have ever been on GitHub, you must have noticed that a regular project’s structure looks like this:

        docs/conf.py
        docs/index.rst
        module/__init__.py
        module/core.py
        tests/core.py
        LICENSE
        README.rst
        requirements.txt
        setup.py

When you start a new python project, you can create a code repository and implement version control.

GitHub is one provider of this, but you can use any other.

#### Structure of the Python Project:

#### License

This is in the root directory and is where you should add a license for your project. Some licenses are:

GNU AGPLv3
GNU GPLv3
Mozilla Public License 2.0
GNU LGPLv3
Apache License 2.0
MIT License
The Unlicense

#### README
This is in the root directory too and is where you describe your project and what it does.

You can write this in Markdown, reStructuredText, or plain text.

#### Module Code
This holds your actual code that may be inside a subdirectory or inside root.

#### requirements.txt
This is not mandatory, but if you use this, you put it in the root directory.

Here, you mention the modules and dependencies of the project- the things it will not run without.

#### setup.py
This script in the root lets distutils build and distribute modules needed by the project.

#### Documentation
Readable documentation is essential. This is placed in the docs directory.

#### Tests
Most projects have tests- keep these in the tests directory.

### 2. Create Readable Documentation
So, next in python best practices is readable documentation. You may find it burdensome, but it creates clean code.

For this, you can use Markdown, reStructuredText, Sphinx, or docstrings.

- __Markdown and reStructuredText__ are markup languages with plain text formatting syntax to make it easier to mark up text and convert it to a format like HTML or PDF.
- __reStructuredText__ lets you create in-line documentation.
- __Sphinx__ is a tool to easily create intelligent and beautiful documentation. It lets you generate Python documentation from existing reStructuredText and export documentation in formats like HTML.
- __Docstrings__ are documentation strings at the beginning of each module, class, or method.

### 3. Follow Style Guidelines
The PEP8 holds some great community-generated proposals.

PEP stands for Python Enhancement Proposals- these are guidelines and standards for development. This is to make sure all Python code looks and feels the same.

One such guideline is to name classes with the CapWords convention.

- Use proper naming conventions for variables, functions, methods, and more.
- Variables, functions, methods, packages, modules: this_is_a_variable
- Classes and exceptions: CapWords
- Protected methods and internal functions: _single_leading_underscore
- Private methods: __double_leading_underscore
- Constants: CAPS_WITH_UNDERSCORES
- Use 4 spaces for indentation. For more conventions, refer to PEP8.

### 4. Correct Broken Code Immediately
Like with the broken code theory, correct your broken code immediately. If you let it be while you work on something else, it can lead to worse problems later.

This is what Microsoft does. It once had a terrible production cycle with MS Word’s first version.

So now, it follows a ‘zero defects methodology’, and always corrects bugs and defects before proceeding.

### 5. Use the PyPI Instead of Doing it Yourself
One of the reasons behind Python’s popularity is the PyPI- this is the Python Package Index; it has more than 198,190 projects at the time of writing.

You should use code from this instead of writing it yourself- this saves time and lets you focus on the more important things.

Install these using pip. You can also create and upload your own package here.

### 6. The Zen of Python
Tim Peters wrote this short poem to express what values you should follow while coding in Python.

You can get this by running “import this” in the IDLE:

#### The Zen of Python, by Tim Peters

##### Beautiful is better than ugly.
##### Explicit is better than implicit.
##### Simple is better than complex.
##### Complex is better than complicated.
##### Flat is better than nested.
##### Sparse is better than dense.
##### Readability counts.
##### Special cases aren’t special enough to break the rules.
##### Although practicality beats purity.
##### Errors should never pass silently.
##### Unless explicitly silenced.
##### In the face of ambiguity, refuse the temptation to guess.
##### There should be one– and preferably only one –obvious way to do it.
##### Although that way may not be obvious at first unless you’re Dutch.
##### Now is better than never.
##### Although never is often better than *right* now.
##### If the implementation is hard to explain, it’s a bad idea.
##### If the implementation is easy to explain, it may be a good idea.
##### Namespaces are one honking great idea — let’s do more of those!

### 7. Use the Right Data Structures
Know the benefits and limitations of different __data structures__, and choose the right one while Coding in Python.

### 8. Write Readable Code
- You should use line breaks and indent your code.
- Use naming conventions for identifiers- this makes it easier to understand the code.
- Use comments, and whitespaces around operators and assignments.
- Keep the maximum line length 79 characters.
### 9. Use Virtual Environments
You should create a virtual environment for each project you create.

This will avoid any library clashes, since different projects may need different versions of a certain library.

### 10. Write Object-Oriented Code
Python is an object-oriented language, and everything in Python is an object. You should use the object-oriented paradigm if writing code for Python.

This has the advantages of data hiding and modularity. It allows reusability, modularity, polymorphism, data encapsulation, and inheritance.

### 11. What Not to Do while Programming in Python
- Avoid importing everything from a package- this pollutes the global namespace and can cause clashes.
- Don’t implement best practices from other languages.
- Do not turn off error reporting during development- turn it off after it.
- Don’t alter sys.path, use distutils for that.
- Python Interview Questions on Best Practices for Python Coding
- What is the use of PyPI?
- What is the best way to write Variables in Python?
- Why writing Readable code is Important?
- What are some of the things you should avoid while Programming in Python?
- Why should you create a separate virtual environment for every project?