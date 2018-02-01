# Regular Expressions
Regular expressions use the backslash character (`'\'`) to indicate special forms or to allow special characters to be used without invoking their special meaning. This collides with python's usage of literal backslash for pattern string.

The solution is to use python's raw string notation for regex patterns; backslashes are not handled in any special way in a string literal prefixed with `r`. so `r"\n"` is a two character string containing '\' and 'n', while `"\n"` is a one character string containing a newline.

Usually patterns will be expressed in Python code using this raw string notation.

## Regular Expression Syntax

A regular expression (or RE) specifies a set of strings that matches it; the functions in the `re` module check if a particular string matches a given regular expression. Regular expressions can be concatenated to form new regular expresssions; if *A* and *B* are both regular expressions, the *AB* is also a regular expression. Repitition qualifiers (`*, +, ?, {m, n}, etc`) cannot be directly nested. This avoids ambiguity with the non-greedy modifier suffix `?`, and with other modifiers in other implementations.

To apply a second repetition to an inner repitition, parentheses may be used. For example `(?:a{6})*` matches any multiple of six `a` characters.

The special characters are:

`.` --> (Dot) In the default mode, this matches any character except a newline. if the `DOTALL` flag has been specified, this matches any character including a new line.

`^` --> (Caret) Matches the start of the string, and in the `MULTILINE` mode also matches immediately after each newline.

`$` --> Matches the end of the string or just before the newline at the end of the string, and in the `MULTILINE` mode also matches before a newline.
`foo` matches both `foo` and `foobar`, while the regular expression `foo$` matches only `foo`.

More interestingly, searching for `foo.$` in `foo1\nfoo2\n` matches `foo2` normally, but `foo1` in `MULTILINE` mode; searching for a single `$` in `foo\n` will find two (empty) matches: one just before the newline, and one at the end of the string.

`*` --> Causes the resulting RE to match 0 or more repetitions of the preceding RE, as many repititions as are possible. `ab*` will match `a`, `ab` or `a` followed by any number of `b`s.

`+` --> Causes the resulting RE to match 1 or more repititions of the preceding RE. `ab+` will match `a` followed by any non-zero number of `b`s; it will not match just `a`.

`?` --> Causes the resulting RE to match 0 or 1 repetitions of the preceding RE. `ab?` will match either `a` or `ab`.


`*?, +?, ??`
	The `*`, `+`, and `?` qualifiers are all greedy; they match as much text as possible. Sometimes this behaviour is not desired; If the RE `<.*>` is matched against `<a> b <c>`, it will match the entire string, not just `<a>`. Adding `?` after the qualifier makes it perform the match in *non-greedy* or *minimal* fashion; as few characters as possible will be matched. Using the RE `<.*?>` will only match `<a>`.

## Regex Search and Match
Call `re.search(regex, subject)` to apply a regex pattern to a subject string. The function returns `None` if the matching attemp fails, and a `Match` object otherwise.

Since `None` evaluates to `False`, you can easily use `re.search()` in an `if` statement. The `Match` object stores details about the part of the string matched by the regular expression pattern.

### Matching modes inside the regular expression
Normally, matching modes are specified outside the regular expression. In a programming language, you can pass them as a flag to the regex constructor or append them to the regex literal.

`(?i)` makes the regex case insensitive `re.I`.

### match function

This function attempts to match RE **pattern** to string with optional flags.

```python
re.match(pattern, string, flags=0)

```

pattern --> This is the regular expression to be matched.

string --> This is the string, which would be searched to match the pattern at the beginning of string.

flags --> you can specify different flags using bitwise OR (|). These are modifiers

The `re.match` function returns a **match** object on success, None on failure. We usegroup(num) or groups() function of **match** object to get matched expression.

method object Method & description

group(num=0) --> This method returns entire match
(or specific subgroup num)

groups() --> This method returns all matching subgroups in a tuple
(empty if there weren't any.)

### Regular Expression Modifiers: Option Flags
Regular expression literals may include an optional modifier to control various aspects of matching. The modifiers are specified as an optional flag. You can provide multiple modifiers using exclusive OR(|)

`re.I`
performs case-insensitive matching.

`re.L`
Interprets words according to the current locale. This interpretatioin affects the alphabetic group (\w and \W), as well as word boundary behaviour (\b or \B).

`re.M`
Makes `$` match the end of the line (not the just the end of the string) and makes `^` match the start of any line (not just the start of the string.)

`re.S`
makes a period (dot) match any character, include newline.

`re.U`
Interprets letters according to the Unicode character set. This flag affects the behaviour \w, \W, \b, \B.

`re.X`
Permits "cuter" regular expression syntax. It ignores whitespace (except inside a set [] or when escaped by a backslash) and treats unescaped # as a comment marker.
