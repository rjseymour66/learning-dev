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
```
```python

# create a string out of another data type
str(9.87)

# multiply strings
name = 'Jack'
name * 4

# 'a', get char from string
name[1]



```






















