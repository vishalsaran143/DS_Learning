# List

A list is a data type that stores multiple items under one name.

```python
my_list = [10, "hello", 3.5, True]
```

- Ordered (items keep their position)
- Mutable (you can change items after creating the list)
- Allows duplicate items
- Dynamic (you can add or remove items on the fly)

## List vs Array (C/C++)

| Point | C/C++ Array | Python List |
|---|---|---|
| Size | Fixed | Dynamic |
| Data type | Only one type | Mixed types allowed |
| Speed | Faster | Slower |
| Memory | Less | More |

> Note: Python's `array` module and NumPy arrays are also single-type and fast, like C arrays.

## How a list is stored in memory

```python
my_list = [10, "hello", 3.5]
```

```
                 LIST  (address: 3376)
        +---------+---------+---------+
        |   680   |   720   |   750   |   <- slots store ADDRESSES, not values
        +---------+---------+---------+
             |         |         |
             v         v         v
        +---------+---------+---------+
        |   10    | "hello" |   3.5   |   <- real values live here
        +---------+---------+---------+
         addr 680   addr 720   addr 750

  Mixed types work   -> slot holds only an address, any type is fine
  List is slower     -> 2 steps: slot -> address -> value
                        (array = 1 step: value directly)
  List uses more memory -> addresses + values are both stored
  List grows         -> when full, Python makes a bigger space,
                        copies the addresses, adds extra empty room
```

## Characteristics of a List
 
- Ordered (position matters)
- Mutable (can be changed)
- Heterogeneous (mixed types allowed)
- Allows duplicates
- Dynamic (grows and shrinks)
- Can be nested (list inside a list)
- Items are accessed by index
- Can hold any Python object (even functions)
```python
L  = [1, 2, 3, 1]
L1 = [3, 2, 1]
print(L == L1)   # False  (order matters, and values differ)
L2 = [1, print, type, input]   # functions are objects too
```
 
## Creating a List
 
```python
[]                          # empty
[1, 2, 3, 4, 5]             # 1D
[1, 2, 3, [4, 5]]           # 2D (nested)
[[[1, 2], [3, 4]], [[5, 6], [7, 8]]]   # 3D
[1, True, 5.6, 5+6j, "Hello"]          # mixed types
list("hello")               # ['h', 'e', 'l', 'l', 'o']  (type conversion)
```
 
## Accessing Items
 
### Indexing
 
```
 L = [10, 20, 30, 40]
 index    0   1   2   3
 negative -4  -3  -2  -1
```
 
```python
L = [[[1, 2], [3, 4]], [[5, 6], [7, 8]]]
print(L[0][0][1])   # 2
```
 
### Slicing
 
`L[start : stop : step]` (stop is not included)
 
```python
L = [1, 2, 3, 4, 5, 6]
print(L[1:4])     # [2, 3, 4]
print(L[::-1])    # [6, 5, 4, 3, 2, 1]  (reverse)
```
 
## Adding Items
 
| Method | What it does |
|---|---|
| `append(x)` | Adds ONE item at the end |
| `extend(iterable)` | Adds EACH item of the iterable at the end |
| `insert(i, x)` | Adds item at index `i` |
 
```python
L = [1, 2, 3, 4, 5]
L.append(True)         # [1, 2, 3, 4, 5, True]
 
L = [1, 2, 3, 4, 5]
L.append([6, 7, 8])    # [1, 2, 3, 4, 5, [6, 7, 8]]   <- one nested item
 
L = [1, 2, 3, 4, 5]
L.extend([6, 7, 8])    # [1, 2, 3, 4, 5, 6, 7, 8]
 
L = [1, 2, 3, 4, 5]
L.extend("delhi")      # [1, 2, 3, 4, 5, 'd', 'e', 'l', 'h', 'i']  <- string splits into letters
 
L = [1, 2, 3, 4, 5]
L.insert(1, 100)       # [1, 100, 2, 3, 4, 5]
```
 
## Editing Items
 
```python
L = [1, 2, 3, 4, 5]
 
L[-1] = 500            # by index   -> [1, 2, 3, 4, 500]
L[1:4] = [200, 300, 400]   # by slice -> [1, 200, 300, 400, 500]
```
 
## Deleting Items
 
| Method | What it does |
|---|---|
| `del L[i]` / `del L[a:b]` | Delete by index or slice |
| `remove(x)` | Delete the FIRST item with value `x` |
| `pop()` / `pop(i)` | Delete and RETURN the last item (or item at `i`) |
| `clear()` | Remove everything |
 
```python
L = [1, 2, 3, 4, 5]
del L[-1]      # [1, 2, 3, 4]
del L[1:3]     # [1, 4]
 
L = [1, 2, 3, 4, 5]
L.remove(5)    # [1, 2, 3, 4]
 
L = [1, 2, 3, 4, 5]
L.pop()        # [1, 2, 3, 4]   (returns 5)
 
L = [1, 2, 3, 4, 5]
L.clear()      # []
```
 
## Operations on Lists
 
### Arithmetic
 
```python
L1 = [1, 2, 3, 4]
L2 = [5, 6, 7, 8]
 
print(L1 + L2)   # [1, 2, 3, 4, 5, 6, 7, 8]   (merge)
print(L1 * 3)    # [1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4]   (repeat)
```
 
### Membership
 
```python
L1 = [1, 2, 3, 4, 5]
L2 = [1, 2, 3, 4, [5, 6]]
 
print(5 not in L1)    # False
print([5, 6] in L2)   # True
```
 
### Loop
 
```python
L3 = [[[1, 2], [3, 4]], [[5, 6], [7, 8]]]
for i in L3:
    print(i)
# [[1, 2], [3, 4]]
# [[5, 6], [7, 8]]
```
 
## 2 Ways to Traverse a List
 
```python
L = [1, 2, 3, 4]
 
for i in L:                  # itemwise
    print(i)
 
for i in range(len(L)):      # indexwise
    print(L[i])
```
 
## List Functions
 
| Function | Result |
|---|---|
| `len(L)` | Number of items |
| `min(L)` / `max(L)` | Smallest / largest |
| `sorted(L)` | NEW sorted list, original unchanged |
| `L.sort()` | Sorts the SAME list (permanent) |
| `L.reverse()` | Reverses the SAME list (permanent) |
| `L.count(x)` | How many times `x` appears |
| `L.index(x)` | Index of the FIRST `x` |
| `L.copy()` | Shallow copy |
 
```python
L = [2, 1, 5, 7, 0]
print(len(L), min(L), max(L))      # 5 0 7
print(sorted(L, reverse=True))     # [7, 5, 2, 1, 0]
 
L = [1, 2, 1, 3, 4, 1, 5]
print(L.count(1))    # 3
print(L.index(1))    # 0
 
L = [2, 1, 5, 7, 0]
print(sorted(L))     # [0, 1, 2, 5, 7]   <- new list
print(L)             # [2, 1, 5, 7, 0]   <- unchanged
L.sort()
print(L)             # [0, 1, 2, 5, 7]   <- changed
```
 
### copy() is shallow
 
```python
L = [2, 1, 5, 7, 0]
L1 = L.copy()
print(id(L) == id(L1))   # False  (different list objects)
```
 
`copy()` copies only the outer list. Nested lists are still shared:
 
```python
a = [1, [2, 3]]
b = a.copy()
a[1].append(9)
print(b)    # [1, [2, 3, 9]]   <- b changed too
```
 
For nested lists use `copy.deepcopy(a)`.
 
## List Comprehension
 
A short way to create a list.
 
```python
new_list = [expression for item in iterable if condition]
```
 
Why use it: fewer lines, and usually faster than a loop with `append`.
 
```python
# loop way
L = []
for i in range(1, 11):
    L.append(i)
 
# comprehension way
L = [i for i in range(1, 11)]
```
 
### Examples
 
```python
# scalar multiplication
v = [2, 3, 4]
s = -3
[s * i for i in v]                          # [-6, -9, -12]
 
# squares
[i**2 for i in [1, 2, 3, 4, 5]]             # [1, 4, 9, 16, 25]
 
# numbers divisible by 5 from 1 to 50
[i for i in range(1, 51) if i % 5 == 0]     # [5, 10, ..., 50]
 
# languages starting with "p"
languages = ["java", "python", "php", "c", "javascript"]
[l for l in languages if l.startswith("p")]   # ['python', 'php']
 
# two ifs
basket    = ["apple", "guava", "cherry", "banana"]
my_fruits = ["apple", "kiwi", "grapes", "banana"]
[f for f in my_fruits if f in basket if f.startswith("a")]   # ['apple']
 
# 3x3 table (nested comprehension)
[[i * j for i in range(1, 4)] for j in range(1, 4)]
# [[1, 2, 3], [2, 4, 6], [3, 6, 9]]
 
# cartesian product (2 loops)
L1 = [1, 2, 3, 4]
L2 = [5, 6, 7, 8]
[i * j for i in L1 for j in L2]
# [5, 6, 7, 8, 10, 12, 14, 16, 15, 18, 21, 24, 20, 24, 28, 32]
```
 
## zip()
 
Pairs items of two lists by position. If lengths differ, the shortest list decides the length.
 
```python
L1 = [1, 2, 3, 4]
L2 = [-1, -2, -3, -4]
 
list(zip(L1, L2))              # [(1, -1), (2, -2), (3, -3), (4, -4)]
[i + j for i, j in zip(L1, L2)]   # [0, 0, 0, 0]  (add indexwise)
```
 
## Disadvantages of Python Lists
 
- Slow (compared to arrays)
- Uses more memory
- Risky because lists are mutable
```python
a = [1, 2, 3]
b = a.copy()
a.append(4)
print(a)   # [1, 2, 3, 4]
print(b)   # [1, 2, 3]
```
 
Risk with `b = a` (no copy): both names point to the SAME list.
 
```python
a = [1, 2, 3]
b = a
a.append(4)
print(b)   # [1, 2, 3, 4]   <- b changed too
```
