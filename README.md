# GoodPractices
A guide for good practices for Aptude team

### Iterating over Sequences and Mappings

Use of range to iterate over a sequence ![Screenshot](bad.png)

    >>> x = [1, 2, 4, 8, 16]
    >>> for i in range(len(x)):
    ...     print(x[i])
    ... 
    1
    2
    4
    8
    16

A better way to iterate over a sequence ![Screenshot](good.png)

    >>> for item in x:
    ...     print(item)
    ... 
    1
    2
    4
    8
    16
