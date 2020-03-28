Global, Local and non local variables
=====================================

Variables in python are implicitly declared by defining them.

The way python uses global and local variables is maverick. While in
many or most other programming languages variables are treated as global
if not otherwise declared, Python deals with variables the other way
around. They are local, if not otherwise declared. The driving reason
behind this approach is that global variables are generally a **bad
practice** and should be avoided.

In most cases where we are tempted to use a global variable, it is
better to utilize a parameter for getting a value into a function or
return a value to get it out.

So when we define variables inside a function definition, they are local
to this function by default. This means that anything you will do to
such a variable in the body of the function will have no effect on other
variables outside of the function, even if they have the same name.

This means that the function body is the scope of the block, where they
are declared and defined in. They can only be used after the point of
their declaration.

Non local variables
-------------------

python3 introduces non local variables as a new kind of variables. Non
local variables have a lot in common with global variables.

One difference to global variables lies in the fact that it is not
possible to change variables from the module scope i.e. variables which
are not defined inside of a function, by using the nonlocal statement.

for example:

``` {.python}
def f():
    global x
    print(x)

x = 3
f()
```

The program will return number `3` as output.

When we change \"global\" to \"nonlocal\":

$~$

``` {.python}
def f():
    nonlocal x
    print(x)
x = 3
f()
```

the program gives an error

``` {.python}
File "local.py", line 2
    nonlocal x
SyntaxError: no binding for nonlocal 'x' found
```

This means that nonlocal bindings can only be used inside of nested
functions. A nonlocal variable has to be defined in the enclosing
function scope. If the variable is not defined in the enclosing function
scope, the variable cannot be defined in the nested scope. This is
another difference to the \"global\" semantics.

``` {.python}
def f():
    x = 42
    def g():
        nonlocal x
        x = 43
    print("Before calling g: " + str(x))
    print("Calling g now:")
    g()
    print("After calling g: " + str(x))

x = 3
f()

print("x in main: " + str(x))
```

------------------------------------------------------------------------

`nonlocal` keyword that allows you to assign to variables in an outer,
but non-global scope.

``` {.python}
def outside():
    msg = "Outside!"
    def inside():
        msg = "Inside!"
        print(msg)
    inside()
    print(msg)

outside()
```

This will print

$~$

``` {.python}
Inside!
Outside!
```

`msg` is declared in the `outside` function and assigned the value
`"Outside!"`. Then in the `inside` function, the value `"Inside!"` is
assigned to it. When we run `outside`, `msg` has the value `"Inside!"`
in the `inside` function, but retains the old value in the `outside`
function.

It is because python didn\'t actually assigned to the existing `msg`
variable, but has created a new variable called `msg` in the local scope
of the `inside` that shadows the nae of the variable in the outer scope.

Preventing that behaviour is where the `nonlocal` keyword comes in.

``` {.python}
def outside():
    msg = "Outside!"
    def inside():
        nonlocal msg
        msg = "Inside!"
        print(msg)
    inside()
    print(msg)

outside()
```

Now, by adding `nonlocal msg` to the top of the `inside`, Python know
that when it sees an assignment to `msg`, it should assign to the
variable from the outer scope instead of declaring a new variable that
shadows its name.

The usage of `nonlocal` is very similar to that of `global`, except that
the former is used for variables in outer function scopes and the latter
is used for variable in the global scope.

Some confusion might arise about when `nonlocal` should be used. Take
the following example,

$~$

``` {.python}
def outside():
    d = {"outside": 1}
    def inside():
        d["inside"] = 2
        print(d)
    inside()
    print(d)

outside()
```

It would be reasonable to expect that without using `nonlocal` the
insertion of the `"inside": 2` key-value pair in the dictionary would
not be reflected in `outside`.

``` {.python}
{'inside': 2, 'outside': 1}
{'inside': 2, 'outside': 1}
```

But It is not so, because the dictionary insertion is not an
*assignment*, but a method call. In fact, inserting a key-value pair
into a dictionary is equivalen to calling the `__setitem__` method on
the dictionary object.

``` {.python}
d = {}
d.__setitem__("inside", 2)
d
```

gives

`{'inside': 2}`
