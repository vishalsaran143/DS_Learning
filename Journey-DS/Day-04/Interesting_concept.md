# Python Memory: Interview Questions

All code below was run and the outputs are real. Addresses (`id`) and sizes (`getsizeof`) change between machines and Python versions.

## 1. What is aliasing?

Aliasing = two or more variables pointing to the **same object** in memory.

```python
a = 4
b = a
c = b
print(id(a) == id(b) == id(c))   # True  (one object, three names)
```

- Good: no copy is made, so memory is saved.
- Risky: if the object is mutable, a change through one name shows up in all names.

```python
a = [1, 2, 3]
b = a
a.append(99)
print(b)    # [1, 2, 3, 99]   <- b changed too
```

## 2. What is garbage collection?

Garbage collection = Python automatically frees the memory of objects that nobody uses anymore.

- Every object has a **reference count** (how many names point to it).
- When the count becomes **0**, the object is removed from memory.
- Python also has a **cyclic garbage collector** (`gc` module) for objects that point to each other and are never used again.

```python
import sys
x = [1, 2, 3]
print(sys.getrefcount(x))   # 2  (x + the temporary argument)
y = x
print(sys.getrefcount(x))   # 3
del y
print(sys.getrefcount(x))   # 2
```

`del` removes only the **name**, not the object:

```python
a = 4
b = a
del a
print(b)    # 4   (the object is still alive because b points to it)
```

## 3. What is mutability and why is it dangerous?

| | Mutable (can change in place) | Immutable (cannot change) |
|---|---|---|
| Types | `list`, `dict`, `set` | `int`, `float`, `str`, `tuple`, `bool` |

```python
L = [1, 2, 3]
i1 = id(L)
L.append(4)
print(i1 == id(L))    # True   (same object, changed in place)

t = (1, 2, 3)
i2 = id(t)
t = t + (4,)
print(i2 == id(t))    # False  (a NEW tuple was created)
```

**Danger = mutable + aliasing.** If many names share one mutable object, a change from one place silently changes it for all of them (see question 1).

## 4. What is cloning?

Cloning = making a copy of a list so it has a **different address**.

```python
a = [1, 2, 3]
b = a[:]              # cloning (same as a.copy() or list(a))
print(a is b)         # False  (different lists)
print(a == b)         # True   (same values)
```

Cloning with `[:]` is a **shallow copy** (see next question).

## 5. Deep copy vs shallow copy

| | Shallow copy | Deep copy |
|---|---|---|
| How | `a.copy()`, `a[:]`, `copy.copy(a)` | `copy.deepcopy(a)` |
| Outer list | New | New |
| Inner (nested) lists | **Shared** (same address) | **New copies** |
| Safe for | 1D lists | Nested lists |

**Shallow, 1D list: works fine**

```python
a = [1, 2, 3, 4]
b = a.copy()
b[-1] = 400
print(a)    # [1, 2, 3, 4]   (a is not changed)
```

**Shallow, 2D list: problem**

```python
a = [1, 2, 3, 4, [100, 200]]
b = a.copy()
b[-1][0] = 40
print(a)    # [1, 2, 3, 4, [40, 200]]   <- a changed too!
print(id(a[-1]) == id(b[-1]))   # True  (inner list is shared)
```

**Deep copy: fixes it**

```python
import copy
a = [1, 2, 3, 4, [100, 200]]
b = copy.deepcopy(a)
b[-1][0] = 40
print(a)    # [1, 2, 3, 4, [100, 200]]   (a is safe)
print(b)    # [1, 2, 3, 4, [40, 200]]
print(id(a[-1]) == id(b[-1]))   # False
```

## 6. How are nested lists stored in memory?

First, a normal list stores **addresses**, not values.

```python
L = [1, 2, 3]
```

```
  Address of slot:   10001      10002      10003
                   +---------+---------+---------+
  LIST (L)         |   101   |   102   |   103   |   <- slots store ADDRESSES
                   +---------+---------+---------+
                        |         |         |
                        v         v         v
  Address of value:    101       102       103
                   +---------+---------+---------+
  VALUES           |    1    |    2    |    3    |   <- real values
                   +---------+---------+---------+

  L[0] -> slot 10001 -> holds 101 -> go to 101 -> value 1
  L[1] -> slot 10002 -> holds 102 -> go to 102 -> value 2
  L[2] -> slot 10003 -> holds 103 -> go to 103 -> value 3
```

**Why addresses and not values?**
Every value has a different size (an int, a string and a list are all different).
An address always has the same size. So:

```
address of L[i] = start of list + i * (size of one slot)
```

Python can jump straight to any item, no matter its type. That is why indexing is fast and a list can hold mixed types.

Now a **nested list**: the slot for the inner list holds the **address of the inner list**, and the inner list has its own slots.

```python
L = [1, 2, 3, [4, 5]]
```

```
  Address of slot:      10001     10002     10003     10004
                     +---------+---------+---------+---------+
  LIST (L)           |   101   |   102   |   103   |   201   |
                     +---------+---------+---------+---------+
                          |         |         |         |
                          v         v         v         |
  Address of value:      101       102       103        |
                     +---------+---------+---------+    |
  VALUES             |    1    |    2    |    3    |    |
                     +---------+---------+---------+    |
                                                        |
                                                        v
  Address of inner list:                               201
  Address of slot:                               20001     20002
                                              +---------+---------+
  INNER LIST                                  |   104   |   105   |
                                              +---------+---------+
                                                   |         |
                                                   v         v
  Address of value:                               104       105
                                              +---------+---------+
  VALUES                                      |    4    |    5    |
                                              +---------+---------+
```

> The numbers are examples. Real addresses are much bigger.

This is why a shallow copy shares the inner list: it copies the slot, which holds the same address `201`.

**Common bug:**

```python
L = [[0] * 2] * 2
L[0][0] = 99
print(L)    # [[99, 0], [99, 0]]   <- both rows changed
```

`* 2` copies the same address `201` twice, so both rows are one inner list.

```python
L = [[0] * 2 for _ in range(2)]   # correct
```

## 7. How are strings stored in memory?

A string is an **immutable** sequence of Unicode characters.

```
s = "hello"

   +---+---+---+---+---+
   | h | e | l | l | o |    <- one object, characters stored together
   +---+---+---+---+---+
     0   1   2   3   4
```

- Unlike a list, a string stores the **characters themselves**, not addresses of them.
- Each character takes 1, 2 or 4 bytes. The size depends on the "widest" character in the string (PEP 393). An English-only string uses 1 byte per character.
- Immutable: you cannot change a character. Any change creates a **new** string.

```python
s = "hello"
s[0] = "H"      # TypeError: 'str' object does not support item assignment
s = "H" + s[1:] # creates a new string
```

**String interning:** Python reuses the same object for some strings to save memory.

```python
s = "hello"
t = "hello"
print(s is t)                       # True   (same object reused)
print(s is "hel" + "lo")            # True   (joined while compiling)
print(s is "".join(["hel", "lo"]))  # False  (created while running)
```

Never compare strings with `is`. Use `==`.

## 8. Why do tuples take less memory than lists?

A list is a **dynamic array**, a tuple is a **static (fixed) array**.

- A tuple's size is fixed, so Python allocates exactly the space it needs, once.
- A list can grow (`append`), so Python keeps **extra empty slots** in advance and stores extra information (current size and capacity).

```python
import sys
print(sys.getsizeof([1, 2, 3]))   # 88
print(sys.getsizeof((1, 2, 3)))   # 64
```

See how a list grows in jumps (it adds spare room each time):

```python
L = []
last = -1
for i in range(20):
    L.append(i)
    size = sys.getsizeof(L)
    if size != last:
        print(len(L), size)       # size changes only at 1, 5, 9, 17 items
        last = size
```

Output: `1 88`, `5 120`, `9 184`, `17 248`.

Tuple = less memory and slightly faster. List = more flexible.

## 9. How is the index position of a set item decided?

A set is a **hash table**. The position is decided by the item's **hash value**.

```
position = hash(item) % table size
```

```python
print(hash(10), hash(3), hash(7))   # 10 3 7   (an int's hash is the int itself)
```

For a table with 8 slots:

```
 10 % 8 = 2      3 % 8 = 3      7 % 8 = 7

 slot:   0   1   2   3   4   5   6   7
                 10   3               7
```

- If two items land on the same slot (collision), Python finds another free slot.
- When the table gets too full, it grows and the items are placed again.
- You do not choose the position, so a set has **no indexing** (`s[0]` is a `TypeError`).
- Order depends on the hash values, not on the order you added the items.

```python
print({7, 3, 10})    # {10, 3, 7}
```

- Strings get a **different hash on every run** of Python, so a set of strings can print in a different order each time you run the program.

Lookups (`x in s`) are fast because Python computes the slot directly. It does not search the whole set.

## 10. Why are mutable types not allowed in sets / dict keys?

A set or dict finds an item using its **hash**. For this to work, the hash must **never change** while the item is stored.

- Mutable object (list) -> its content can change -> its hash would change -> Python would look in the wrong slot and could not find it again.
- So mutable types have no hash. They are **unhashable**.

```python
hash([1, 2])        # TypeError: unhashable type: 'list'
{1, [2, 3]}         # TypeError: unhashable type: 'list'
{[1, 2]: "a"}       # TypeError: unhashable type: 'list'
```

A tuple is allowed only if everything **inside** it is also hashable:

```python
hash((1, 2))        # works
hash((1, [2]))      # TypeError: unhashable type: 'list'
```

Only dict **keys** must be hashable. Dict **values** can be anything:

```python
d = {"a": [1, 2]}   # fine
```

Need a set that can sit inside another set? Use `frozenset` (immutable set).

## Short answers (for interview)

| Question | One-line answer |
|---|---|
| Aliasing | Many names, one object |
| Garbage collection | Memory of unused objects (count = 0) is freed automatically |
| Why mutability is dangerous | Mutable object + aliasing = silent changes everywhere |
| Cloning | New list with a different address (`a[:]`), shallow |
| Shallow vs deep | Shallow shares inner objects, deep copies everything |
| Nested list in memory | Slot holds the address of the inner list, which has its own slots |
| Strings in memory | Immutable, characters stored together, some strings interned |
| Tuple vs list memory | Tuple is fixed size, list keeps spare slots to grow |
| Set position | `hash(item) % table size` |
| Mutable in set/dict key | Hash must not change, mutable objects are unhashable |
