Exceptions in python
====================

Python has many built-in exceptions which forces your program to output
an error when something in it goes wrong.

When these exceptions occur, it causes the current process to stop and
passes it to the calling process until it is handled. If not handled,
our program will crash.

For example, if function `A` calls function `B` which in turn calls
function `C` and an exception occurs in function `C`. If it is not
handled in `C`, the exception passes to `B` and then to `A`.

If never handled, an error message is thrown out and our program comes
to a sudden unexpected fault.

``` {.python}
try:
    # do something
    pass
except ValueError:
    # handle ValueError exception
    pass
except (TypeError, ZeroDivisionError):
    # handle multiple exceptions
    # TypeError and ZeroDivisionError
    pass
except:
    # handle all other exceptions
    pass

```

-   If an exception occurs during the execution of the `try` clause, the
    rest of the clause is skipped. Then if its type matches the
    exception named after the `except` keyword, the except clause is
    executed, and then execution continues after `try` statement.

Raising Exceptions
------------------

In Python Programming, exceptions are raised when corresponding errors
occur at run time, but we can forcefully raise it using keyword raise.

``` {.python}
try:
    a = int(input("Enter positive integer: "))
    if a <= 0:
        raise ValueError("Not a positive number.")
except ValueError as ve:
    print(ve)
```

try ... finally
---------------

The try statement in Python can have an optional `finally` clause. This
clause is executed no matter what, and is generally used to release
external resources.

for example, we may be connected to a remote data center through the
network or working with a file or with a Graphical User Interface (GUI).

In all these circumstances, we must clean up the resources once used,
whether it was successful or not. These actions (closing a file, GUI or
disconnecting from network) are performed in the finally clause to
guarantee execution.

``` {.python}
try:
    f = open("test.txt", encoding='utf-8')
    # perform file operations
finally:
    f.close()
```

finally makes a difference if we return early

``` {.python}
try:
    run_code_one()
except TypeError:
    run_code_two()
    return None
finally:
    other_code()
```

-   finally block is run before the method returns in the above
    construct compared to :

``` {.python}
try:
    run_code_one()
except TypeError:
    run_code_two()
    return None

other_code()
```

-   the `other_code()` doesn\'t run if there\'s an exception.

other situations that can cause differences:

-   If an exception is thrown inside the except block.
-   If an exception is thrown in `run_code_one()` but it\'s not a
    `TypeError`.
-   Other control flow statements such as `continue` and `break`
    statements.

Custom Exceptions
-----------------

we may need to create custom exceptions that serves your purpose.

In python, users can define such exceptions by creating a new class.
This exception class has to be derived, either directly or indirectly,
from `Exception` class. Most of the built-in exceptions are also derived
from this class.

``` {.python}
class CustomError(Exception):
    pass

raise CustomError

raise CustomError("An Error occured")
```

In development, It is a good practice to place all the user-defined
exceptions that our program raises in a seperate file. Many standard
modules do this. They define their exceptions seperately as
`exceptions.py` or `errors.py`.

------------------------------------------------------------------------

A class in an `except` clause is compatible with an exception if it is
the same class or a base class thereof (but not the other way around --
an except clause listing a derived class is not compatible with a base
class). For example consider the following code.

``` {.python}
class B(Exception):
    pass

class C(B):
    pass

class D(C):
    pass

for cls in [B, C, D]:
    try:
        raise cls()
    except D:
        print("D")
    except C:
        print("C")
    except B:
        print("B")
```

the following code will print B, C, D in that order.

Note that if the except clauses were reversed (with `except B` first),
it would have printed B, B, B -- the first matching except clause is
triggered.
