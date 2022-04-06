# Toolset

## venv

### Create virtual env

```bash
$ python3 -m venv ./<venv-name>
# Ex: python3 -m venv ./venv
```

### start venv
```bash
$ source ./<venv-name>/bin/activate # you don't need the './' before the command, but the tutorial used it
```

### exit venv
```bash
$ deactivate
```

## pip

1. Run pip show on every package that you want to uninstall so you know that it doesn't depend on any package that you plan to uninstall
2. pip uninstall <package-name> -y

### Commands
```bash
$ pip list
$ pip show <package-name>
$ pip uninstall <package-name>
```

## requirements.txt

Requirements file lists all of the program's dependencies. You can pass this program to pip.

1. To get all of the program's dependencies, enter pip freeze > requirements.txt
2. Verify with cat requirements.txt
3. Go to your new venv enter pip install -r requirements.txt to install every package listed in tthe file. 

Manually change requirements.txt to update package version requirements.

```
== means the exact version
>= means version greater than or equal to 
, != 1.0.1 means there is a restriction. Put those after a comma in the version
Ex: pyvim>=3.0.2, <= 4.0.0 or , != 3.0.6
```

To upgrade new requirements, enter pip install --upgrade -r requirements.txt

### Dev requirements files

requirements_dev.txt

```bash
$ -r requirements.txt # copies regular requirements.txt files into this 
prod-packageName>=5.3.5
```

requirements_locked.txt is a copy of requirements.txt
	- special version that has locked down, known good dependencies

### Types of req files
	requirements.txt	base level file
	requirements_dev.txt	dev env
	requirements_locked.txt	prod env

# Basics

## Operators

```python
=       # assignment
==      # equality (not memory)

# Identity
is      # same object with same memory location
is not  # different objects with same memory location

# Membership
in      # True if x in y
not in  # True if x not in y

# Logical
and
or
not

# Boolean
True
False
```

To test equality, use `==`.

## if, elif, else

```python
name = 'Smith'

if name == 'Nelson':
    print('This is wrong')
elif name == 'Douglas':
    print('This is wrong')
elif name == 'Smith':
    print('This is right')
else:
    print('No answer')
```

# Strings

```python
# Use three single or double quotes for multi-line strings
song = '''Happy birthday to you,
Happy birthday to you,
Happy birthday dear person,
Happy birthday to you!'''

# create a string out of another data type
str(9.87)
song.startswith('Happy')    # True
song.endswith('everyone!')  # False

# Find the offset of the first occurrence (returns -1 if not found)
word = 'to'
song.find(word)
15

# last occurrence (returns -1 if not found)
song.rfind(word)
89

# number of occurrences
song.count(word)
3

# all chars letters or numbers?
song.isalnum()
False

# string case funcs
phrase.strip(' .')
'you win some'
phrase = 'you win some ...'
phrase.capitalize()
'You win some ...'
phrase.title()
'You Win Some ...'
phrase.upper()
'YOU WIN SOME ...'
phrase.lower()
'you win some ...'
phrase.swapcase()
'YOU WIN SOME ...'

# multiply strings
name = 'Jack'
name * 4

# 'a', get char from string
name[1]
```
## Substring with a slice

```python
offsets = '0123456789'

# [:] extracts the entire sequence from start to end
offsets[:]  # 0123456789

# [start:] from the start offset to the end, inclusive
offsets[5:]     # 56789

# [:end] from the beginning to the end offset -1 (non-inclusive)
offsets[:5]     # 01234

# [start:end] from the start offset to the end offset - 1 (end is non-inclusive)
offsets[2:7]    # 23456

# [start:end:step] from the start offset to the end offset - 1 (end is non-inclusive), skipping characters by step
offsets[2:7:2]  # 246
```
## Built-in functions

```python
offsets = '0123456789'

len(offsets)        # 10
```
### split()

```python
tasks = 'one,two,three,four'
# if you don't provide a separator, split() uses anything that makes sense
tasks.split(',')    # ['one', 'two', 'three', 'four']
tasks.split()       # ['one,two,three,four']
```

### join()
join() collapses a list of strings into a single string. Use the 
following syntax:
<separator>.join(list_of_strings)

```python
str_list = ['one', 'two', 'three', 'four']
'\n'.join(str_list)
'one\ntwo\nthree\nfour'

' '.join(str_list)
'one two three four'
```

### replace() 

replace() does simple substring substitution

```python
sub = 'This is the dumbest string ever'
sub.replace('dumb', 'cool')
'This is the coolest string ever'
```
### Formatting strings

```python

animal = 'dog'
place = 'house'

# {} and format()
'The {} is in the {}.'.format(animal, place)
'The dog is in the house.'
'The {a} is in the {b}.'.format(a='cat', b='litter box')
'The cat is in the litter box.'

# f-strings
f'The {animal} is in the {place}'
'The dog is in the house'
f'The {animal.capitalize()} is in the {place.rjust(20)}'
'The Dog is in the                house'
```

## Loops

### while loop

```python
count = 0
while count < 5:
     print(count)
     count += 1 
0
1
2
3
4
```

### for and in with iterators

Iterators allow you to traverse a data structure without knowing how loarge they are or how they are implemented. They include:
- strings
- lists
- tuples
- dictionaries

```python
# for element in interable:
#   do something

sentence = 'A string is an iterable'
for letter in sentence:
     print(letter)
 
A
 
s
t
r
i
n
g
 
i
...
```

### range() to generate numbers

`range()` returns a stream of numbers within a specified range without having to use memory on a data structure. `range()` returns in iterable object that you can step through with a `for ... in` loop or convert to a sequence, such as a list.

`range(start: stop: step)`

```python

# standard usage
for x in range(0, 5):
     print(x) 
0
1
2
3
4

# create a list
list(range(0, 5))
[0, 1, 2, 3, 4]

# count down with a step
for x in range(5, -1, -1):
     print(x)
 
5
4
3
2
1
0

# create a list
list((5, -1, -1))
[5, -1, -1]
```

## Tuples

Tuples and lists can both contain zero or more Python objects of any type. 

### Creating a tuple 

Use parentheses or a ',':

```python
# parens
> empty_tuple = ()
> empty_tuple
()

# string followed by ','
> one_stooge = 'Larry',
> one_stooge
('Larry',)

# for multiple items, do not add a ',' after the last one
> all_stooges = 'Larry', 'Curly', 'Moe'
> all_stooges
('Larry', 'Curly', 'Moe')

# parens make it easier to read
> parens_stooges = ('Larry', 'Curly', 'Moe')
> parens_stooges
('Larry', 'Curly', 'Moe')
```


### Tuple actions

When you assign more than one tuple value at the same time:

```python
> parens_stooges = ('Larry', 'Curly', 'Moe')
> parens_stooges
('Larry', 'Curly', 'Moe')
> a, b, c = all_stooges
> a
'Larry'
> b
'Curly'
> c
'Moe'

# swap vals without creating a temp var
> one = 'one'
> two = 'two'
> one, two = two, one
> one
'two'
> two
'one'

# Tuple from a list
> stooge_list = ['Larry', 'Curly', 'Moe']
> tuple(stooge_list)
('Larry', 'Curly', 'Moe')

# Combine tuples with '+'
# Combine with a '+'. Note the ',' after the item in the single-value tuple:

> ('Larry',) + ('Curly', 'Moe')
('Larry', 'Curly', 'Moe')

# Duplicate items in tuple 
> ('howdy',) * 5
('howdy', 'howdy', 'howdy', 'howdy', 'howdy')

# Compare tuples
> x = (1, 2, 3)
> y = (2, 3, 4)
> x == y
False
> x < y
True
> x <= y
True

# Modify a tuple
# When you concatenate a tuple with another tuple, it creates a new Python object
> first = ('one', 'two', 'three')
> second = ('four',)
> third = first + second
> third
('one', 'two', 'three', 'four')
> id(first)
2049613520640
> id(second)
2049618746960
> id(third)
2049614519888
```
### Iterate through a tuple

Use for and in to iterate through a tuple:

```python 
> nums
('one', 'two', 'three', 'four')
> for n in nums:
...     print(n)
...
one
two
three
four
```

## Lists

Use lists to keep track of ordered items, especially when the order might change. Lists are mutable.

### Creating a list

```python

# Create an empty list with brackets
> empty_list = []
> empty_list
[]

# Empty list with list() func
> empty_too = list()
> empty_too
[]

# List with values
> beatles = ['John', 'Paul', 'George', 'Ringo']
> beatles
['John', 'Paul', 'George', 'Ringo']


# Create list out of items in an iterable
> list('individual')
['i', 'n', 'd', 'i', 'v', 'i', 'd', 'u', 'a', 'l']

# List from a tuple with list()
> tup = ('one', 'two', 'three')
> list(tup)
['one', 'two', 'three']

# list using string.split() func
> adj = 'once-in-a-lifetime'
> adj.split('-')
['once', 'in', 'a', 'lifetime']
```

### Getting list items

```python
> turtles = ['Leonardo', 'Donatello', 'Michaelangelo', 'Raphael']

# Get with an offset
> turtles[2]
'Michaelangelo'

# Get with a slice
> turtles[0:2]
['Leonardo', 'Donatello']
```

### List functions

```python
> nums = ['one', 'two', 'three', 'four']
> nums
['one', 'two', 'three', 'four']

# append to the end
> nums.append('five')
> nums
['one', 'two', 'three', 'four', 'five']

# insert at an index
> nums.insert(0, 'zero')
> nums
['zero', 'one', 'two', 'three', 'four', 'five']

# multiply a list
> ['blah'] * 3
['blah', 'blah', 'blah']

# combine lists
> numeros = ['uno', 'dos', 'tres']
> nums.extend(numeros)
> nums
['zero', 'one', 'two', 'three', 'four', 'five', 'uno', 'dos', 'tres']

# edit by index
> nums[2] = 'too'
> nums
['zero', 'one', 'too', 'three', 'four', 'five', 'uno', 'dos', 'tres']

# edit by slice
> nums[6:] = ['six', 'seven', 'eight']
> nums
['zero', 'one', 'too', 'three', 'four', 'five', 'six', 'seven', 'eight']

# delete by index
> del nums[0]
> nums
['one', 'too', 'three', 'four', 'five', 'six', 'seven', 'eight']

# delete by value
> nums.remove('seven')
> nums
['one', 'too', 'three', 'four', 'five', 'six', 'eight']

# remove from end of list
> nums.pop()
'eight'
> nums
['one', 'too', 'three', 'four', 'five', 'six']

# remove by index
> nums.pop(1)
'too'
> nums
['one', 'three', 'four', 'five', 'six']

# delete every item in the list
> nums.clear()
> nums
[]

# get index by value
> nums.index('two')
1

# use 'in' to check if in list
> 'three' in nums
True
> 'four' in nums
True
> 'nine' in nums
False


# get number of occurences by value
> nums
['one', 'two', 'three', 'four', 'two']
> nums.count('two')
2

# convert to string with a delimiter
> ', '.join(nums)
'one, two, three, four, two'

# get the length
> len(nums)
5

# sort with sorted(list)
> alpha_nums = sorted(nums)
> alpha_nums
['four', 'one', 'three', 'two', 'two']

# sort with .sort()
> nums
['one', 'two', 'three', 'four', 'two']
> nums.sort()
> nums
['four', 'one', 'three', 'two', 'two']

# copy and compare lists
> a = nums
> a
['four', 'one', 'three', 'two', 'two']

# not a copy, assigned same object to two different variables
> b = a
> b
['four', 'one', 'three', 'two', 'two']
> id(b)
2660463301888
> id(a)
2660463301888
> c = a.copy()
> id(c)
2660462605824
> d = list(c)
> id(d)
2660463342336
> e = d[:]
> id(d)
2660463342336
> a = b
> a == b
True
> a == c
True
> a == d
True
> a == e
True
```

### Iterating through lists 

```python

# for and in to iterate through a list
> ls = ['one', 'two', 'three', 'four', 'five']
> for i in ls:
...     print(i)
...
one
two
three
four
five
> es = ['uno', 'dos', 'tres', 'quatro', 'cinco']
> es
['uno', 'dos', 'tres', 'quatro', 'cinco']

# zip to iterate through multiple lists simultaneously
> for english, spanish in zip(ls, es):
...     print(english, ":\t", spanish)
...
one :    uno
two :    dos
three :  tres
four :   quatro
five :   cinco
```

### List comprehensions

List comprehensions are a way to build a list. It uses the following format:

[`expression` for `item` in `iterable`]

It moves the loop into the brackets to create a list out of what the expression returns for each item in the list. This would otherwise be written as follows:

for `item` in `iterable`:
    `expression`

```python
> ls = ['one', 'two', 'three']

# basic list comprehensions
> upper = [item.capitalize() for item in ls]
> upper
['One', 'Two', 'Three']

> num_ls = [n for n in range(0, 10)]
> num_ls
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

# expression
> index_adjusted = [n + 1 for n in num_ls]
> index_adjusted
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

Conditional list comprehensions add a condition after the iterable:

[`expression` for `item` in `iterable` if `condition`]

This is equal to the following:

for `item` in `iterable`:
    if (`condition`):
        `expression`

```python
> animals = ['cat', 'dog', 'mouse', 'rat', 'bird']
> three = [a for a in animals if len(a) == 3]
> three
['cat', 'dog', 'rat']
> Caps = [a.capitalize() for a in animals if len(a) != 3]
> Caps
['Mouse', 'Bird']
```

Create nested list comprehensions by listing the conditions one after the other:

```python

# standard nested loop
> nums = range(1, 4)
> nums
range(1, 4)
> alpha = ['x', 'y']
> for num in nums:
...     for a in alpha:
...             print(num, a)
...
1 x
1 y
2 x
2 y
3 x
3 y

# same loop as a list comprehension
> ls_comp = [(num, a) for num in nums for a in alpha]
> for x in ls_comp:
...     print(x)
...
(1, 'x')
(1, 'y')
(2, 'x')
(2, 'y')
(3, 'x')
(3, 'y')

# tuple unpacking
> for (num, a) in ls_comp:
...     print(num, a)
...
1 x
1 y
2 x
2 y
3 x
3 y
```

### Lists of lists 

Exactly what it sounds like:

```python
> evens = [2, 4, 6, 8, 10]
> odds = [1, 3, 5, 7, 9]
> prime = [1, 7, 13, 19, 23]
> nums = [evens, odds, prime]
> nums
[[2, 4, 6, 8, 10], [1, 3, 5, 7, 9], [1, 7, 13, 19, 23]]

```