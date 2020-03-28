-   Never pass mutable datatypes to a functions as arguments

-   Instance variables and class variables

-   static, public and protected variables in python

-   decorators \# annotations ??

### classmethods

-   `@classmethod`
-   class methods as alternative constructors
-   take cls as default argument, so mandatory for usage.
-   different from static methods

### static methods

-   `@staticmethod`
-   static methods don\'t take cls or instance arguments as default
    argument

```{=html}
<!-- -->
```
-   Method resolution order
-   Every class inherits from `builtins.object` like `Object()` class in
    java

Inheriting from super class
---------------------------

-   `super().__init__(first, last, pay)`
-   `Employee.__init__(self, first, last, pay)`
-   `isinstance()` and `issubclass()`
-   `threading.Thread.__init__(self)`

First class functions
---------------------

``` {.python}
def yell(text):
    return text.upper() + '!'
```

``` {.bash org-language="sh"}
>>> yell('hello')
'HELLO!'
```

all data in python programs is represented by objects or relations
between objects

``` {.bash org-language="sh"}
>>> bark = yell
>>> bark('woof')
'WOOF!'
```

-   function objects and their names are two seperate concerns. we can
    delete the function\'s original name `yell`
-   But another name `bark` still points to the underlying function

``` {.bash org-language="sh"}
>>> del yell
>>> yell('hello?')
# will give a NameError

>>> bark('hey')
'HEY!'
```
