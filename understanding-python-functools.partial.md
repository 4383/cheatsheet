# Mastering `functools.partial` in Python

When coding in Python, you’ll often run into functions that do a lot, but you only ever use them in one or two common ways. You end up repeating arguments, or you write small wrapper functions that feel redundant.

[`functools.partial`](https://docs.python.org/3/library/functools.html#functools.partial) is the clean solution. It allows you to **freeze some arguments of a function** and return a new function with those values locked in. Think of it as pre-filling defaults and creating tailor-made versions of your functions.

---

## Squaring and cubing numbers

Let’s start simple. Suppose you have a function that raises a number to a given exponent:

```python
def power(base, *, exp=2):
    return base ** exp
```

Instead of calling `power(5, exp=2)` every time, you can freeze those arguments once and create new functions:

```python
from functools import partial

square = partial(power, exp=2)
cube   = partial(power, exp=3)

print(square(5))  # 25
print(cube(2))    # 8
```

One general function instantly becomes two specialized helpers, without repeating code.

---

## Freezing keyword arguments

Partial isn’t limited to math. Imagine a function that takes several parameters:

```python
def foo(a, b, *, c, d=10):
    print(a, b, c, d)
```

If you always use the same value for one of them, just lock it in:

```python
from functools import partial

only_d = partial(foo, d=999)
only_b = partial(foo, b=42)

only_d(1, 2, c=3)   # 1 2 3 999
only_b(1, c=3, d=4) # 1 42 3 4
```

No more repetition, and the intent is clearer.

---

## Making code more readable

This shines in everyday tasks. For example, converting strings to numbers in different bases usually looks like this:

```python
int("1100011", base=2)
```

With `partial`, you can define helpers:

```python
from functools import partial

from_bin = partial(int, base=2)
from_hex = partial(int, base=16)

print(from_bin("1100011"))  # 99
print(from_hex("63"))       # 99
```

Now your code literally says “from binary” or “from hex,” making it much easier to read.

---

## Why not just use a lambda?

You could write something like:

```python
from_bin = lambda x: int(x, base=2)
```

But `partial` is usually better. It’s shorter, preserves function metadata like the name and docstring, and scales better when functions have many parameters.

---

## A quick challenge

Try this: create a helper with `partial` that finds the longest word in a list of strings:

```python
from functools import partial

longest = partial(max, key=len)

words = ["python", "functools", "partial", "awesome"]
print(longest(words))  # functools
```

With just one line, you’ve turned a general-purpose function into a specialized one.

---

## Wrapping up

`functools.partial` is one of those small tools that can make a big difference. It helps reduce repetition, makes code more expressive, and encourages readability. The next time you find yourself passing the same arguments over and over, remember that you can “pre-fill the blanks” and create your own ready-to-use functions.

---

✨ If you enjoyed this tutorial, don’t forget to **star this GitHub repo**, [subscribe to my YouTube channel](https://www.youtube.com/@herveberaud/), and follow me on [GitHub](https://github.com/4383) and [LinkedIn](https://www.linkedin.com/in/herv%C3%A9-beraud-a5ba55165/) to keep learning and growing with Python.
