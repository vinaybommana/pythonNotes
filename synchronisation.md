Synchronization in Python
=========================

synchronization primitives
--------------------------

-   synchronization primitives are used to tell the program to keep the
    threads in synchrony.
-   blocking methods are the methods which block execution of a
    particular thread until some condition is met.

Locks
-----

-   A `Lock` has only two states:

    -   locked
    -   unlocked

-   It is created in the unlocked state and has two principal methods.

    -   `acquire()`
    -   `release()`

The `acquire()` method locks the `Lock` and blocks the execution until
the `release()` method in some other coroutine sets it to unlocked.

Then it locks the `Lock` again and returns `True` The `release()` method
should only be called in locked state, it sets the state to unlocked and
returns immediately. If `release()` is called in unlocked state, a
`RunTimeError` is raised.
