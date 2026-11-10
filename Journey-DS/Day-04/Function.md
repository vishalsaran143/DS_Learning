# Functions

A function is a reusable block of code that runs only when you call it.

```python
def is_even(num):
    """Return 'even' or 'odd' for a given integer."""
    if type(num) == int:
        if num % 2 == 0:
            return "even"
        else:
            return "odd"
    else:
        return "not a number"

for i in range(1, 4):
    print(is_even(i))     # odd, even, odd

print(is_even("hello"))   # not a number
print(is_even.__doc__)    # shows the docstring
```

Benefits: modularity, readability, reusability.

## Parameters vs Arguments

| Term | Meaning | Example |
|---|---|---|
| Parameter | Variable in the function definition | `def power(a, b)` -> `a`, `b` |
| Argument | Value you pass when calling | `power(2, 3)` -> `2`, `3` |

## Types of Arguments

```python
def power(a=1, b=1):      # default arguments
    return a ** b

power()            # 1        (defaults used)
power(2, 3)        # 8        positional (order matters)
power(b=3, a=2)    # 8        keyword (order does not matter)
```

## *args and **kwargs

| | Collects | Stored as |
|---|---|---|
| `*args` | Any number of positional arguments | tuple |
| `**kwargs` | Any number of keyword arguments | dict |

```python
def multiply(*args):
    product = 1
    for i in args:
        product = product * i
    print(args)          # (1, 2, 3, 4)
    return product

multiply(1, 2, 3, 4)     # 24
```

```python
def display(**kwargs):
    for key, value in kwargs.items():
        print(key, "->", value)

display(india="delhi", nepal="kathmandu")
# india -> delhi
# nepal -> kathmandu
```

Rules:

- Order: normal arguments -> `*args` -> `**kwargs`
- `args` and `kwargs` are only convention. `*numbers` works too, but stick to the standard names.

## Function without return

A function with no `return` gives back `None`.

```python
L = [1, 2, 3]
print(L.append(4))   # None   (append changes the list, returns nothing)
print(L)             # [1, 2, 3, 4]
```

Common bug: `L = L.append(4)` makes `L` equal to `None`.

## Variable Scope

Local variable = lives inside the function. Global variable = lives outside.

```python
# 1) Reading a global works
def g(y):
    print(x)
    print(x + 1)
x = 5
g(x)         # 5, 6
print(x)     # 5

# 2) Assigning inside creates a NEW local x
def f(y):
    x = 1
    x += 1
    print(x)
x = 5
f(x)         # 2
print(x)     # 5   (global x unchanged)

# 3) Changing a global without declaring it -> ERROR
def h(y):
    x += 1
x = 5
h(x)         # UnboundLocalError
```

Why #3 fails: `x += 1` makes `x` local for the whole function, but the local `x` has no value yet.

To really change the global, use the `global` keyword (use it rarely):

```python
def h():
    global x
    x += 1
```

```python
# 4) Parameter is also local
def f(x):
    x = x + 1
    print("in f(x): x =", x)    # 4
    return x

x = 3
z = f(x)
print(z)    # 4
print(x)    # 3   (unchanged)
```

## Nested Functions

A function defined inside another function.

```python
def g(x):
    def h(x):
        x = x + 1
        print("in h(x): x =", x)    # 5
    x = x + 1
    print("in g(x): x =", x)        # 4
    h(x)
    return x

x = 3
z = g(x)
print(x)    # 3
print(z)    # 4
```

Each function has its own `x`. Changing one does not change the others.

> Careful: if `g` calls `f` and `f` calls `g`, it never stops and you get `RecursionError`.

## Functions are First-Class Citizens

In Python a function is an object, like int or list. You can:

```python
def square(num):
    return num ** 2

type(square)     # <class 'function'>
id(square)       # address of the function object
```

**1. Assign to another name**

```python
x = square
x(3)       # 9    (x and square point to the same function)
```

**2. Store in a list / set**

```python
L = [1, 2, 3, 4, square]
L[-1](3)   # 9
s = {square}
```

**3. Return from a function**

```python
def f():
    def x(a, b):
        return a + b
    return x

print(f()(3, 4))    # 7
```

**4. Pass as an argument**

```python
def func_a():
    print("inside func_a")

def func_b(z):
    print("inside func_b")
    return z()

func_b(func_a)
```

**5. Delete**

```python
del square
square(3)    # NameError
```

## Lambda Function

A small **anonymous** function. Any number of arguments, but only **one expression**.

```python
lambda x: x ** 2           # x -> x squared

a = lambda x, y: x + y
a(5, 2)                    # 7

a = lambda s: "a" in s
a("hello")                 # False

a = lambda x: "even" if x % 2 == 0 else "odd"
a(6)                       # 'even'
```

| | Normal function | Lambda |
|---|---|---|
| Name | Yes | No (anonymous) |
| `return` keyword | Needed | Not needed (result is returned automatically) |
| Lines | Many | One expression |
| Reuse | Easy | Hard |

Main use: **with higher-order functions** (`map`, `filter`, `reduce`).

## Higher Order Functions (HOF)

A function that takes a function as an argument, or returns a function.

```python
def transform(f, L):
    output = []
    for i in L:
        output.append(f(i))
    print(output)

L = [1, 2, 3, 4, 5]
transform(lambda x: x ** 3, L)    # [1, 8, 27, 64, 125]
```

### map

Applies a function to **every** item.

```python
list(map(lambda x: x ** 2, [1, 2, 3, 4, 5]))
# [1, 4, 9, 16, 25]

list(map(lambda x: "even" if x % 2 == 0 else "odd", [1, 2, 3, 4, 5]))
# ['odd', 'even', 'odd', 'even', 'odd']

users = [
    {"name": "Rahul",  "age": 45, "gender": "male"},
    {"name": "Nitish", "age": 33, "gender": "male"},
    {"name": "Ankita", "age": 50, "gender": "female"},
]
list(map(lambda u: u["name"], users))
# ['Rahul', 'Nitish', 'Ankita']
```

### filter

Keeps only items where the function returns `True`.

```python
list(filter(lambda x: x > 5, [3, 4, 5, 6, 7]))
# [6, 7]

fruits = ["apple", "guava", "cherry"]
list(filter(lambda x: x.startswith("a"), fruits))
# ['apple']
```

### reduce

Combines all items into **one** value. It lives in `functools`.

```python
import functools

functools.reduce(lambda x, y: x + y, [1, 2, 3, 4, 5])
# 15

functools.reduce(lambda x, y: x if x > y else y, [23, 11, 45, 10, 1])
# 45   (this finds the MAX)
```

How reduce works on `[1, 2, 3, 4, 5]` with `x + y`:

```
(1, 2) -> 3
(3, 3) -> 6
(6, 4) -> 10
(10, 5) -> 15
```

### map vs filter vs reduce

| | Input | Output | Size of output |
|---|---|---|---|
| `map` | function + iterable | transformed items | Same as input |
| `filter` | function + iterable | selected items | Equal or smaller |
| `reduce` | function + iterable | one value | 1 |

`map` and `filter` return an iterator, so wrap them in `list()` to see the result.
