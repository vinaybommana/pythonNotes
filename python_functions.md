function\'s `__name__` won\'t affect how you can access it from your
code. This identifier is merely a debugging aid. A *variable pointing*
to a *function* and the *function* itself are two seperate concerns

there\'s also `__qualname__` which serves a similar purpose and provides
a qualified name string to disambiguate function and class names

Functions can be stored in data structures
==========================================

Functions can be passed to other functions
==========================================

Functions can be nested
=======================

Higher order functions
======================

-   Functions that can accept other functionss as arguments are also
    called *higher-order functions*. They are a necessity for the
    functional programming style.

-   The classical example for higher-order functions in python is the
    built-in `map` function.

-   it takes a function and an iterable and calls the function on each
    element in the iterable yielding the results as it goes along.

``` {.python}
def yell(text):
    return text.upper() + '!'

>>> list(map(yell, ['hello', 'hey', 'hi']))
['HELLO!', 'HEY!', 'HI!']
```

-   map has gone through the entire list and applied the `yell` function
    to each element
