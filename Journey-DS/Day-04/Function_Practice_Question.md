# Functions: Practice Problems (My Code)

Outputs below are from actually running each cell on its own.

## Problem 1: Unique elements of a list

Write a Python function that takes a list and returns a new list with unique elements of the first list.

```
Input:  [1, 2, 3, 3, 3, 3, 4, 5]
Output: [1, 2, 3, 4, 5]
```

```python
def unique_element(list):
  new_list = set(list)
  print(list[new_list])
list=[1,2,3,3,3,3,4,5]
unique_element(list)
```

Output:

```text
TypeError: list indices must be integers or slices, not set
```

```python
def unique_element(list):
  new_list = []
  for i in list:
    if i not in new_list:
      new_list.append(i)
  print(new_list)
list=[1,2,3,3,3,3,4,5]
unique_element(list)
```

Output:

```text
[1, 2, 3, 4, 5]
```

## Problem 2: Sort hyphen-separated words

Write a Python function that accepts a hyphen-separated sequence of words as parameter and returns the words in a hyphen-separated sequence after sorting them alphabetically.

```
Input:  green-red-yellow-black-white
Output: black-green-red-white-yellow
```

```python
def para(s):
  s = s.split('-')
  return '-'.join(sorted(s))
s = "green-red-yellow-black-white"
para(s)
```

Output:

```text
'black-green-red-white-yellow'
```

## Problem 3: Count upper and lower case letters

Write a Python function that accepts a string and calculate the number of upper case letters and lower case letters.

```
Sample String : 'CampusX is an Online Mentorship Program fOr EnginEering studentS.'
Expected Output :
No. of Upper case characters :  9
No. of Lower case Characters :  47
```

```python
def cal(s):
  print("No. of Upper case characters : ", len([i for i in s if i.isupper()]))
  print("No. of Upper case characters : ", len([i for i in s if i.islower()]))

s = "CampusX is an Online Mentorship Program fOr EnginEering studentS."
cal(s)
```

Output:

```text
No. of Upper case characters :  9
No. of Upper case characters :  47
```

## Problem 4: Even numbers from a list

Write a Python program to print the even numbers from a given list.

```
Sample List : [1, 2, 3, 4, 5, 6, 7, 8, 9]
Expected Result : [2, 4, 6, 8]
```

```python
def even(list):
  l = [i for i in list if i%2==0]
  return l
list = [1,2,3,4,5,6,7,8,9]
even(list)
```

Output:

```text
[2, 4, 6, 8]
```

## Problem 5: Perfect number

Write a Python function to check whether a number is perfect or not.

A perfect number is a number that is half the sum of all of its positive divisors (including itself).

```
The first perfect number is 6, because 1, 2, and 3 are its proper positive divisors, and 1 + 2 + 3 = 6.
Equivalently, the number 6 is equal to half the sum of all its positive divisors: ( 1 + 2 + 3 + 6 ) / 2 = 6.

The next perfect number is 28 = 1 + 2 + 4 + 7 + 14. This is followed by the perfect numbers 496 and 8128.
```

```python
n = 496
l = [i for i in range(1,n) if n%i==0]
if n == sum(l):
  print(l)
  print(sum(l))
  print("Perfect square")
else:
  print("NO")
```

Output:

```text
[1, 2, 4, 8, 16, 31, 62, 124, 248]
496
Perfect square
```

## Problem 6: Merge any number of dictionaries

Write a Python function to concatenate any no of dictionaries to create a new one.

```
Sample Dictionary :
dic1={1:10, 2:20}
dic2={3:30, 4:40}
dic3={5:50,6:60}
Expected Result : {1: 10, 2: 20, 3: 30, 4: 40, 5: 50, 6: 60}
```

```python
dic1={1:10, 2:20}
dic2={3:30, 4:40}
dic3={5:50,6:60}
def merge(*dic4):
  d = {}
  for i in range(len(dic4)):
    d.update(dic4[i])
  return d
print(merge(dic1,dic2,dic3))
```

Output:

```text
{1: 10, 2: 20, 3: 30, 4: 40, 5: 50, 6: 60}
```

## Problem 7: Word with the most occurrences

Write a python function that accepts a string as input and returns the word with most occurence.

```
Input:
hello how are you i am fine thank you

Output:
you -> 2
```

```python
def occurence(s,Input_user):
  count = s.count(Input_user)
  return count
s = "hello hello hello hello how are you i am fine thank you"
Input_user = input("Enter thr word")
occurence(s,Input_user)
```

Output (typed `hello` when asked):

```text
Enter thr wordhello
4
```

## Problem 8: Histogram with bin size 10

Write a python function that receives a list of integers and prints out a histogram of bin size 10.

```
Input:
[13,42,15,37,22,39,41,50]

Output:
{11-20:2,21-30:1,31-40:2,41-50:3}
```

```python
l = [13,42,15,37,22,39,41,50]
dict ={f"{i}-{i+10-1}" : 0 for i in range(1,max(l),10)}
for i in l:
```

Output:

```text
IndentationError: expected an indented block after 'for' statement on line 3
```

## Problem 9: Nearest coordinate to a query point

Write a python function that accepts a list of 2D co-ordinates and a query point, and then finds the co-ordinate which is closest in terms of distance from the query point.

```
List of Coordinates
[(1,1),(2,2),(3,3),(4,4)]
Query Point
(0,0)

Output
Nearest to (0,0) is (1,1)
```

```python
Query = (0,0)
Query[0]
```

Output:

```text
0
```

```python
Query = (0,0)
x = {}
l = [(1,1),(2,2),(3,3),(4,4)]
for i in range(len(l)):
  x[i] = l[i][0]-Query[0]
x
```

Output:

```text
{0: 1, 1: 2, 2: 3, 3: 4}
```

## Problem 10: Bag of Words

Write a python program that receives a list of strings and performs bag of word operation on those strings.

https://en.wikipedia.org/wiki/Bag-of-words_model

```python
s =  "John likes to watch movies. Mary likes movies too"
s = s.split(" ")
count = 0
d = {}
for i in s:
  if i not in d:
    d[i] = 1
  else:
    d[i]+=1
print(d)
```

Output:

```text
{'John': 1, 'likes': 2, 'to': 1, 'watch': 1, 'movies.': 1, 'Mary': 1, 'movies': 1, 'too': 1}
```

## Problem 11: Add three lists with map and lambda

Write a Python program to add three given lists using Python map and lambda.

```python
L1 = [1,2,3]
L2 = [4,5,6]
L3 = [7,8,9]
list(map(lambda x,y,z : x+y+z,L1,L2,L3))
```

Output:

```text
[12, 15, 18]
```

## Problem 12: Power of each number with its index

Write a Python program to create a list containing the power of said number in bases raised to the corresponding number in the index using Python map.

```
Input:
list1 = [1,2,3,4,5,6]

Output:
[1,2,9,64,625,-]
```

```python
list1 = [1,2,3,4,5,6]
list(map(lambda x,i:x**i, list1, range(len(list1))))
```

Output:

```text
[1, 2, 9, 64, 625, 7776]
```

## Problem 13: Filter vowels with filter() and .lower()

Using filter() and list() functions and .lower() method filter all the vowels in a given string.

```python
s = "Hello World, Python Is Fun"
  vowels = "aeiou"
  print(ch(s,vowels))
  def ch(s,vowels):
    l = []
    s = s.lower()
    for i in s:
      if i in vowels:
        l.append(i)
    return l
```

Output:

```text
IndentationError: unexpected indent
```

```python
s = "Hello World, Python Is Fun"
vowels = "aeiou"
list(filter(lambda ch : ch.lower() in vowels,s))
```

Output:

```text
['e', 'o', 'o', 'o', 'I', 'u']
```

## Problem 14: Convert 2D list to 1D with reduce

Use reduce to convert a 2D list to 1D.

```python
l = [[1,2,3],[4,5,6]]
import functools
functools.reduce(lambda x, y: x + y, l)
```

Output:

```text
[1, 2, 3, 4, 5, 6]
```

## Problem 15: Highly skilled employees

A dictionary contains following information about 5 employees:

- First name
- Last name
- Age
- Grade (Skilled, Semi-skilled, Highly skilled)

Write a program using map/filter/reduce to get a list of employees (first name + last name) who are highly skilled.

```python
list(map(lambda x: x['fname'] + ' ' + x['lname'], list(filter(lambda x: True if x['grade'] == "highly-skilled" else False, employees))))
```

Output (if run before `employees` is defined):

```text
NameError: name 'employees' is not defined
```

```python
employees = [
    {
        'fname':'Nitish',
        'lname':'Singh',
        'age' : 33,
        'grade':'skilled'
    },
    {
        'fname':'Ankit',
        'lname':'Verma',
        'age' : 34,
        'grade':'semi-skilled'
    },
    {
        'fname':'Neha',
        'lname':'Singh',
        'age' : 35,
        'grade':'highly-skilled'
    },
    {
        'fname':'Anurag',
        'lname':'Kumar',
        'age' : 30,
        'grade':'skilled'
    },
    {
        'fname':'Abhinav',
        'lname':'Sharma',
        'age' : 37,
        'grade':'highly-skilled'
    }

]

list(map(lambda x:x['fname'] + ' ' + x['lname'],list(filter(lambda x:True if x['grade'] == 'highly-skilled' else False,employees))))
```

Output:

```text
['Neha Singh', 'Abhinav Sharma']
```
