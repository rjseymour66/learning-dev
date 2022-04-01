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












