Decorators
==========

Functions in Python are first-class
-----------------------------------

Unlike other languages, python treats functions as first-class citizens.
That means that the language treats functions and data in the same way.
Like data, functions can be assigned to variables, copied, and used as
return values. They can also be passed into other functions as
parametets.

``` {.python}
def foo():
    print('foo!')

def bar(function):
    function()

bar(foo)
# prints 'foo!'
```

Decorators wrap existing functions
----------------------------------

A decorator is a callable that takes a callable as an argument and
returns another callable to replace it.

### The @ syntax

The `@` syntax, is used to specify that the function `bar` should be
wrapped or *decorated* by **foo**. The following statement is exactly
equivalent to using `@`.

``` {.python}
def foo(fn):
    def inner():
        print('About to call function.')
        fn()
        print('Finished calling function.')
    return inner

@foo
def bar():
    print('Calling function bar.')
```

``` {.python}
bar = foo(bar)
```
