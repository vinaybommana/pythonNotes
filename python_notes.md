# python generator

A python generator is a function which returns a generator object *iterator* by calling over _yield_. `yield` may be called with a value, in which case that value is treated as "generated" value.
 
 The `next()` is called on the _generator iterator_.

 The generator resumes execution from where it called `yield`, not from the beginning of the function.

All of the state, like the values of local variables, is recovered and the generator continues to execute until the next call to `yield`.

There are times, though, when it's beneficial to have the ability to create a "function" which, instead of simply returning a single value, is able to yield a series of values.

To do so, such a function would need to be able to "save its work", so to speak.

`yield` however, implies that the transfer of control is temporary and voluntary, and our function expects to regains iit in the future.


# exceptions

* raise statement is used to throw an exception in python3
* use the most specific Exception constructor that semantically fits the issue

* exception chaining preserves the tracebacks.

```python3

raise RuntimeError('specific message') from error  

```


Deprecated methods

These can easily hide and even get into production code. if we want to raise an exception doing them will raise an error.

In python3 there are four different syntaxs for raising exceptions:

1. `raise exception`
2. `raise exception (args)`
3. `raise`
4. `raise exception (args) from original_exception`

4. is used to create exception chaining in which an exception that is raised to another exception can contain the details of the original exception