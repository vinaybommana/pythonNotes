Python look up loop holes
=========================

Late binding closures
---------------------

Another common source of confusion is the way Python binds its variables
(or in the surrounding global scope)

``` {.python}
def create_multipliers():
    return [lambda x: i * x for i in range(5)]

for multiplier in create_multipliers():
    print(multiplier(2), end="..")
print()
```

output:

``` {.example}
# not 0..2..4..6..8
8..8..8..8..8..
```

Five functions are created; instead all of them just multiply x by 4.
Why? Python\'s closures are *late* binding. This means that the values
of variables used in closures are looked up at the time the inner
function is called.

Here, whenever any of the returned functions are called, the value of
`i` is looked up in the surrounding scope at call time. By then, the
loop has completed, and `i` is left with its final value of 4
