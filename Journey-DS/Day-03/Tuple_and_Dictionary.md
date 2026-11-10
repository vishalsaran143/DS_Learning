# Tuple

A tuple is like a list, but **immutable** (cannot be changed after creation).

- Ordered
- Immutable
- Allows duplicates

## Creating a Tuple

```python
t1 = ()                      # empty
t2 = ("hello",)              # single item -> comma is a MUST
t3 = (1, 2, 3, 4)
t4 = (1, 2.5, True, [1, 2, 3])   # mixed types
t5 = (1, 2, 3, (4, 5))           # nested
t6 = tuple("hello")              # ('h', 'e', 'l', 'l', 'o')

print(type(("hello",)))   # <class 'tuple'>
print(type(("hello")))    # <class 'str'>  <- no comma = not a tuple
```

## Accessing Items

```python
t3 = (1, 2, 3, 4)
print(t3[0])      # 1
print(t3[-1])     # 4
print(t3[-1:-4:-1])   # (4, 3, 2)

t5 = (1, 2, 3, (4, 5))
print(t5[-1][0])  # 4
```

## Edit / Add / Delete

```python
t3[0] = 100     # TypeError  (cannot edit)
# no add, no remove
del t3          # works: deletes the WHOLE tuple
del t5[-1]      # TypeError  (cannot delete one item)
```

## Operations

```python
t1 = (1, 2, 3, 4)
t2 = (5, 6, 7, 8)

print(t1 + t2)    # (1, 2, 3, 4, 5, 6, 7, 8)
print(t1 * 3)     # (1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4)
print(1 in t1)    # True

for i in t1:
    print(i)
```

## Tuple Functions

```python
t = (1, 2, 3, 4)
len(t)                     # 4
sum(t)                     # 10
min(t), max(t)             # 1, 4
sorted(t, reverse=True)    # [4, 3, 2, 1]  <- returns a LIST

t = (1, 2, 3, 4, 5)
t.count(50)    # 0
t.index(50)    # ValueError (not found)
```

## List vs Tuple

| Point | List | Tuple |
|---|---|---|
| Syntax | `[ ]` | `( )` |
| Mutable | Yes | No |
| Speed | Slower | Faster |
| Memory | More | Less |
| Built-in methods | Many | Only `count`, `index` |
| Error prone | More | Less (cannot change by mistake) |
| Use when | Data changes | Data is fixed |

```python
import sys
L = list(range(1000))
T = tuple(range(1000))
print(sys.getsizeof(L))   # bigger
print(sys.getsizeof(T))   # smaller
```

### Mutable vs immutable behavior

```python
a = [1, 2, 3]
b = a
a.append(4)
print(a)   # [1, 2, 3, 4]
print(b)   # [1, 2, 3, 4]   <- same object, both changed

a = (1, 2, 3)
b = a
a = a + (4,)    # creates a NEW tuple
print(a)   # (1, 2, 3, 4)
print(b)   # (1, 2, 3)      <- unchanged
```

## Special Syntax

### Unpacking

```python
a, b, c = (1, 2, 3)         # a=1, b=2, c=3
a, b = (1, 2, 3)            # ValueError (count must match)

a, b = 1, 2
a, b = b, a                 # swap -> a=2, b=1

a, b, *others = (1, 2, 3, 4)
print(a, b)       # 1 2
print(others)     # [3, 4]   <- a LIST
```

### zip

```python
a = (1, 2, 3, 4)
b = (5, 6, 7, 8)
tuple(zip(a, b))   # ((1, 5), (2, 6), (3, 7), (4, 8))
```

---

# Set

A collection of **unique** items with **no order**.

- Unordered (no indexing)
- Mutable (add / remove items)
- No duplicates
- Items must be immutable (no list, dict, set inside)

## Creating a Set

```python
s = set()            # empty set  ({} makes a DICT, not a set)
s1 = {1, 2, 3}
s3 = {1, "hello", 4.5, (1, 2, 3)}   # tuple is OK
s4 = set([1, 2, 3])
s5 = {1, 1, 2, 2, 3, 3}             # {1, 2, 3}  (duplicates removed)

s6 = {1, 2, [3, 4]}      # TypeError: list is mutable
print({1, 2, 3} == {3, 2, 1})   # True  (order does not matter)
```

## Accessing / Editing

```python
s1 = {1, 2, 3, 4}
s1[0:3]       # TypeError (no indexing, no slicing)
s1[0] = 100   # TypeError
```

## Adding Items

```python
S = {1, 2, 3, 4}
S.add(5)              # {1, 2, 3, 4, 5}
S.update([5, 6, 7])   # {1, 2, 3, 4, 5, 6, 7}  (adds many)
```

## Deleting Items

| Method | If item is missing |
|---|---|
| `discard(x)` | Does nothing |
| `remove(x)` | KeyError |
| `pop()` | Removes a RANDOM item |
| `clear()` | Empties the set |

```python
s = {1, 2, 3, 4, 5}
s.discard(50)   # no error
s.remove(50)    # KeyError
del s[0]        # TypeError (no indexing)
s.clear()       # set()
```

## Set Operations

```
 s1 = {1, 2, 3, 4, 5}       s2 = {4, 5, 6, 7, 8}

 Union          s1 | s2     {1, 2, 3, 4, 5, 6, 7, 8}
 Intersection   s1 & s2     {4, 5}
 Difference     s1 - s2     {1, 2, 3}
                s2 - s1     {6, 7, 8}
 Symmetric diff s1 ^ s2     {1, 2, 3, 6, 7, 8}   (in one, not both)
```

```python
1 not in s1    # False

for i in s1:
    print(i)
```

## Set Functions

```python
s = {3, 1, 4, 5, 2, 7}
len(s)                    # 6
sum(s)                    # 22
min(s), max(s)            # 1, 7
sorted(s, reverse=True)   # [7, 5, 4, 3, 2, 1]  <- LIST
```

| Method | Returns new set | Changes same set |
|---|---|---|
| union | `s1.union(s2)` | `s1.update(s2)` |
| intersection | `s1.intersection(s2)` | `s1.intersection_update(s2)` |
| difference | `s1.difference(s2)` | `s1.difference_update(s2)` |
| symmetric difference | `s1.symmetric_difference(s2)` | `s1.symmetric_difference_update(s2)` |

```python
s1 = {1, 2, 3, 4}
s2 = {7, 8, 5, 6}
s1.isdisjoint(s2)     # True   (nothing in common)

s1 = {1, 2, 3, 4, 5}
s2 = {3, 4, 5}
s1.issuperset(s2)     # True
s2.issubset(s1)       # True

s3 = s1.copy()
```

## Frozenset

An **immutable** set. Read operations work, write operations do not.

```python
fs1 = frozenset([1, 2, 3])
fs2 = frozenset([3, 4, 5])
fs1 | fs2     # frozenset({1, 2, 3, 4, 5})
fs1.add(9)    # AttributeError
```

Use it for a set inside a set (2D set):

```python
fs = frozenset([1, 2, frozenset([3, 4])])
```

## Set Comprehension

```python
{i**2 for i in range(1, 11) if i > 5}   # {36, 49, 64, 81, 100}
```

---

# Dictionary

Stores data as **key : value** pairs.

```python
d = {"name": "nitish", "age": 33, "gender": "male"}
```

- Mutable
- No indexing (access by key, not position)
- Keys must be unique
- Keys must be immutable (str, int, tuple OK. list not OK)

> Since Python 3.7, a dict remembers insertion order. But you still cannot use `d[0]` to get the first item.

## Creating a Dictionary

```python
d  = {}                                   # empty dict
d1 = {"name": "nitish", "gender": "male"}
d2 = {(1, 2, 3): 1, "hello": "world"}     # tuple as key is OK

# nested (like JSON)
s = {
    "name": "nitish",
    "college": "bit",
    "sem": 4,
    "subjects": {"dsa": 50, "maths": 67, "english": 34}
}

d4 = dict([("name", "nitish"), ("age", 32), (3, 3)])

d5 = {"name": "nitish", "name": "rahul"}
print(d5)   # {'name': 'rahul'}  <- duplicate key: last value wins

d6 = {"name": "nitish", [1, 2, 3]: 2}   # TypeError: list cannot be a key
```

## Accessing Items

```python
my_dict = {"name": "Jack", "age": 26}
my_dict["age"]        # 26
my_dict["city"]       # KeyError
my_dict.get("age")    # 26
my_dict.get("city")   # None  (no error)

s["subjects"]["maths"]   # 67
```

## Adding / Editing

Same syntax: if the key exists it edits, if not it adds.

```python
d4["gender"] = "male"       # adds
d4["weight"] = 72           # adds
s["subjects"]["ds"] = 75    # adds in nested dict
s["subjects"]["dsa"] = 80   # edits
```

## Removing Items

```python
d = {"name": "nitish", "age": 32, 3: 3, "gender": "male", "weight": 72}

d.pop(3)          # removes key 3, returns its value
d.popitem()       # removes the LAST added pair
del d["name"]     # removes by key
d.clear()         # {}

del s["subjects"]["maths"]   # nested
```

## Operations

```python
d = {"name": "nitish", "gender": "male", "age": 33}

"name" in d       # True   (checks KEYS only)
"nitish" in d     # False

for i in d:
    print(i, d[i])    # loop gives keys
```

## Dictionary Functions

```python
len(d)                    # 3
sorted(d, reverse=True)   # ['name', 'gender', 'age']   <- sorts KEYS, returns list
max(d)                    # 'name'                       <- max KEY

d.items()    # dict_items([('name', 'nitish'), ('gender', 'male'), ('age', 33)])
d.keys()     # dict_keys(['name', 'gender', 'age'])
d.values()   # dict_values(['nitish', 'male', 33])

d1 = {1: 2, 3: 4, 4: 5}
d2 = {4: 7, 6: 8}
d1.update(d2)
print(d1)    # {1: 2, 3: 4, 4: 7, 6: 8}   <- key 4 got the new value
```

## Dictionary Comprehension

```python
{key: value for key, value in iterable if condition}
```

```python
# numbers and their squares
{i: i**2 for i in range(1, 11)}

# from an existing dict
distances = {"delhi": 1000, "mumbai": 2000, "bangalore": 3000}
{k: v * 0.62 for k, v in distances.items()}
# {'delhi': 620.0, 'mumbai': 1240.0, 'bangalore': 1860.0}

# using zip
days   = ["Sunday", "Monday", "Tuesday"]
temp_C = [30.5, 32.6, 31.8]
{d: t for d, t in zip(days, temp_C)}
# {'Sunday': 30.5, 'Monday': 32.6, 'Tuesday': 31.8}

# with if
products = {"phone": 10, "laptop": 0, "charger": 32, "tablet": 0}
{k: v for k, v in products.items() if v > 0}
# {'phone': 10, 'charger': 32}

# nested: tables of 2 to 4
{i: {j: i * j for j in range(1, 11)} for i in range(2, 5)}
```

---

# Quick Comparison

| | List | Tuple | Set | Dict |
|---|---|---|---|---|
| Syntax | `[ ]` | `( )` | `{ }` | `{k: v}` |
| Ordered | Yes | Yes | No | Insertion order |
| Mutable | Yes | No | Yes | Yes |
| Duplicates | Yes | Yes | No | Keys: No |
| Indexing | Yes | Yes | No | By key |
