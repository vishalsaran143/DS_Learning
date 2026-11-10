# Day 1 - Python Basics

Today is my first day of learning from scratch. It is difficult, and I feel a bit lonely and regretful about starting over, but never mind. Let's begin and keep going.

**Topics covered:** Operators, Strings and their functions (loops are still pending).

---

## 1. Operators in Python

- Arithmetic
- Relational
- Logical
- Bitwise
- Assignment
- Membership

### Arithmetic Operators

```python
print(5 + 6)
print(5 - 6)
print(5 * 6)
print(5 / 2)
print(5 // 2)
print(5 % 2)
print(5 ** 2)
```

```
11
-1
30
2.5
2
1
25
```

`/` gives a float, `//` is floor division, `%` is the remainder, `**` is the power.

### Relational Operators

```python
print(4 > 5)
print(4 < 5)
print(4 >= 4)
print(4 <= 4)
print(4 == 4)
print(4 != 4)
```

```
False
True
True
True
True
False
```

### Logical Operators

```python
print(1 and 0)
print(1 or 0)
print(not 1)
```

```
0
1
False
```

### Bitwise Operators

```python
print(2 & 3)    # bitwise AND
print(2 | 3)    # bitwise OR
print(2 ^ 3)    # bitwise XOR
print(~3)       # bitwise NOT
print(4 >> 2)   # right shift
print(5 << 2)   # left shift
```

```
2
3
1
-4
1
20
```

### Assignment Operators

```python
a = 2
a += 2      # same as a = a + 2
print(a)
```

```
4
```

Note: Python has no `a++` or `++a`. Use `a += 1`.

### Membership Operators

`in` / `not in`

```python
print('D' not in 'Delhi')
print(1 in [2, 3, 4, 5, 6])
```

```
False
False
```

---

## 2. Strings

A string is a sequence of characters. In Python it is a sequence of Unicode characters.

### Creating Strings

```python
s = 'hello'
s = "hello"
s = '''hello'''      # multiline
s = """hello"""      # multiline
s = str('hello')
print(s)
```

Single vs double quotes: `'it's raining outside'` gives an error because Python thinks the string ends at the second `'`. Use double quotes instead:

```python
s = "it's raining outside"
```

### Accessing Strings

**Positive indexing**

```python
s = 'hello world'
print(s[4])
```

```
o
```

**Negative indexing**

```python
s = 'hello world'
print(s[-3])
```

```
r
```

**Slicing**

```python
s = 'hello world'
print(s[6:0:-2])
```

```
wol
```

**Reverse a string**

```python
print(s[::-1])
```

```
dlrow olleh
```

### Editing Strings

```python
s = 'hello world'
s[0] = 'H'      # TypeError
```

Python strings are **immutable**. We cannot change, add to or delete from a string in place.

### Deleting Strings

```python
s = 'hello world'
del s
print(s)        # NameError: s is not defined
```

We can delete the whole variable, but not part of a string:

```python
s = 'hello world'
del s[-1:-5:2]  # TypeError: strings do not support item deletion
```

### Operations on Strings

**Arithmetic**

```python
print('delhi' + ' ' + 'mumbai')
print('delhi' * 5)
```

```
delhi mumbai
delhidelhidelhidelhidelhi
```

**Relational** (compared lexicographically, by ASCII code)

```python
print('delhi' != 'delhi')
print('mumbai' > 'pune')
print('Pune' > 'pune')
```

```
False
False
False
```

**Logical** (an empty string `''` counts as False)

```python
print('' and 'world')
print('' or 'world')
print('hello' and 'world')
print('hello' or 'world')
```

```
(empty string)
world
world
hello
```

- `and`: if the first value is false, it returns the first; otherwise it returns the second.
- `or`: if the first value is true, it returns the first; otherwise it returns the second.

### Common Functions

```python
print(len('hello world'))
print(max('hello world'))
print(min('hello world'))
print(sorted('hello world', reverse=True))
```

```
11
w
 
['w', 'r', 'o', 'o', 'l', 'l', 'l', 'h', 'e', 'd', ' ']
```

`min()` returns a space here, because a space has a lower ASCII value than any letter.

### Capitalize / Title / Upper / Lower / Swapcase

```python
s = 'hello world'
print(s.capitalize())
print(s.title())
print(s.upper())
print('Hello World'.lower())
print('HeLlO WorLD'.swapcase())
```

```
Hello world
Hello World
HELLO WORLD
hello world
hElLo wORLd
```

### Count / Find / Index

```python
print('my name is nitish'.count('i'))
print('my name is nitish'.find('m'))
print('my name is nitish'.index('m'))
```

```
3
0
0
```

`find()` returns -1 if the value is not found, while `index()` raises an error.

### Startswith / Endswith

```python
print('my name is nitish'.endswith('sho'))
print('my name is nitish'.startswith('1my'))
```

```
False
False
```

### Format

```python
name = 'vishal'
gender = 'male'
print('Hi my name is {1} and I am a {0}'.format(gender, name))
```

```
Hi my name is vishal and I am a male
```

### isalnum / isalpha / isdigit / isidentifier

```python
print('nitish1234%'.isalnum())
print('nitish'.isalpha())
print('123abc'.isdigit())
print('first-name'.isidentifier())
```

```
False
True
False
False
```

### Split / Join

```python
print('hi my name is nitish'.split())
print(" ".join(['hi', 'my', 'name', 'is', 'nitish']))
```

```
['hi', 'my', 'name', 'is', 'nitish']
hi my name is nitish
```

### Replace

```python
print('hi my name is nitish'.replace('nitisrgewrhgh', 'campusx'))
```

```
hi my name is nitish
```

The old text was not found, so nothing changed.

### Strip

```python
print('nitish                           '.strip())
```

```
nitish
```

---
