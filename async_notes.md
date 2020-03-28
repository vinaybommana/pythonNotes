Asynchronous Programming
========================

-   a style of concurrent programming
-   doing many things at once

How does python do multiple things at once
------------------------------------------

### Multiple Processes

-   The OS does all the multi-tasking work
-   Only option for multi-core concurrency

### Multiple Threads

-   The OS does all the multi-tasking work
-   In CPython, the GIL(Global Interpreter Lock) prevents multi-core
    concurrency

Asynchronous Programming
------------------------

-   No OS intervention
-   One Process, one thread

A style of concurrent programming in which tasks release the CPU during
*waiting periods*, so that other *tasks* can use it.

How is async is implemented
===========================

-   Async functions need the ability to suspend and resume

-   A function that enters a waiting period is suspended, and only
    resumed when the wait is over

-   Four ways to implement suspend/resume in Python

    -   Call back function
    -   Generator functions
    -   Async/await (Python 3.5)
    -   Greenlets(require greenlet packages)
