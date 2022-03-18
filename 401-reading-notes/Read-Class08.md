## List Comprehensions in Python

Reading from [List Comprehensions in Python](https://www.pythonforbeginners.com/basics/list-comprehensions-in-python)

**Syntax**: 

my_new_list = [ expression for item in list ]

You can see from this example that three ingredients are necessary for a python list comprehension to work.

- First is the expression we’d like to carry out. expression inside the square brackets.
- Second is the object that the expression will work on. item inside the square brackets.
- Finally, we need an iterable list of objects to build our new list from. list inside the square brackets.
  
To understand the list comprehension, imagine it like this: you’re going to perform an expression on each item in the list. The expression will determine what item is eventually stored in the output list. 

**Notes about Lists Comprehensions**
List comprehension methods are an elegant way to create and manage lists. 
In Python, list comprehensions are a more compact way of creating lists. 
More flexible than for loops, list comprehension is usually faster than other methods.

## Create a List with range()

Example 1: Creating a list with list comprehensions
```
# construct a basic list using range() and list comprehensions
# syntax
# [ expression for item in list ]
digits = [x for x in range(10)]

print(digits)

Output
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

let’s break down this python example by starting with the first ‘x’. This is our expression. It doesn’t do anything because we’re simply recording the number. The second ‘x’ represents each item in the list created by the range() method.

In the python example above, we’re using the range() method to generate a list of numbers. Python iterates(or loops) through each item in that range, and saves a copy of the item in a new list called digits.

**Create a List Using Loops and List Comprehension in Python**
```
# create a list using a for loop
squares = []

for x in range(10):
    # raise x to the power of 2
    squares.append(x**2)

print(squares)
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```
OR

```
# create a list using list comprehension
squares = [x**2 for x in range(10)]

print(squares)
```

**Multiplying Parts of a List**
```
# create a list with list comprehensions
multiples_of_three = [ x*3 for x in range(10) ]

print(multiples_of_three)
Output

[0, 3, 6, 9, 12, 15, 18, 21, 24, 27]
```

```
# a list of the names of popular authors
authors = ["Ernest Hemingway","Langston Hughes","Frank Herbert","Toni Morrison",
    "Emily Dickson","Stephen King"]

# create an acronym from the first letter of the author's names
letters = [ name[0] for name in authors ]
print(letters)
Output


['E', 'L', 'F', 'T', 'E', 'S']
```

List comprehensions can make solving issues involving strings much easier using simplified expressions. These methods can save time and precious lines of code.

```
# use list comprehension to print the letters in a string
letters = [ letter for letter in "20,000 Leagues Under The Sea"]

print(letters)
Output

['2', '0', ',', '0', '0', '0', ' ', 'L', 'e', 'a', 'g', 'u', 'e', 's', ' ', 'U', 'n', 'd', 'e', 'r', ' ', 'T', 'h', 'e', ' ', 'S', 'e', 'a']
```

**Lower/Upper case converter using Python**
```
lower_case = [ letter.lower() for letter in ['A','B','C'] ]
upper_case = [ letter.upper() for letter in ['a','b','c'] ]

print(lower_case, upper_case)
Output

['a', 'b', 'c'] ['A', 'B', 'C']
```

```
# user data entered as name and phone number
user_data = "Elvis Presley 987-654-3210"
phone_number = [ x for x in user_data if x.isdigit()]

print(phone_number)
Output

['9', '8', '7', '6', '5', '4', '3', '2', '1', '0']

```

**Parsing a file using list comprehension**

```
# open the file in read-only mode
file = open("dreams.txt", 'r')
poem = [ line for line in file ]

for line in poem:
    print(line)

Output

Hold fast to dreams

For if dreams die

Life is a broken-winged bird

That cannot fly.

-Langston Hughs
```
**Using functions in list comprehensions**

```
# list comprehension with functions
# create a function that returns a number doubled
def double(x):
    return x*2

nums = [double(x) for x in range(1,10)]
print(nums)
Output

[2, 4, 6, 8, 10, 12, 14, 16, 18]
```

Filtering elements from the list can be done using additional arguments. In the following example, only even numbers are selected.
```
# add a filter so we only double even numbers
even_nums = [double(x) for x in range(1,10) if x%2 == 0]
print(even_nums)
Output


[4, 8, 12, 16]
```
Additional arguments can be added to create more complex logic:
```

nums = [x+y for x in [1,2,3] for y in [10,20,30]]
print(nums)
Output

[11, 21, 31, 12, 22, 32, 13, 23, 33]
```
------------------------------------------------------

## First-Class Objects

Reading from [Primer on Decorators](https://realpython.com/primer-on-python-decorators/)

In Python, functions are first-class objects. This means that functions can be passed around and used as arguments, just like any other object (string, int, float, list, and so on). Consider the following three functions:
```
def say_hello(name):
    return f"Hello {name}"

def be_awesome(name):
    return f"Yo {name}, together we are the awesomest!"

def greet_bob(greeter_func):
    return greeter_func("Bob")
```
Here, say_hello() and be_awesome() are regular functions that expect a name given as a string. The greet_bob() function however, expects a function as its argument. We can, for instance, pass it the say_hello() or the be_awesome() function:
```
>>> greet_bob(say_hello)
'Hello Bob'

>>> greet_bob(be_awesome)
'Yo Bob, together we are the awesomest!'
```
Note that greet_bob(say_hello) refers to two functions, but in different ways: greet_bob() and say_hello. The say_hello function is named without parentheses. This means that only a reference to the function is passed. The function is not executed. The greet_bob() function, on the other hand, is written with parentheses, so it will be called as usual.

## Inner Functions

It’s possible to define functions inside other functions. Such functions are called inner functions. Here’s an example of a function with two inner functions:
```
def parent():
    print("Printing from the parent() function")

    def first_child():
        print("Printing from the first_child() function")

    def second_child():
        print("Printing from the second_child() function")

    second_child()
    first_child()
```

## Reusing Decorators
Recall that a decorator is just a regular Python function. All the usual tools for easy reusability are available. Let’s move the decorator to its own module that can be used in many other functions.

Create a file called decorators.py with the following content:
```
def do_twice(func):
    def wrapper_do_twice():
        func()
        func()
    return wrapper_do_twice
```

**Note**: You can name your inner function whatever you want, and a generic name like wrapper() is usually okay. You’ll see a lot of decorators in this article. To keep them apart, we’ll name the inner function with the same name as the decorator but with a wrapper_ prefix.

You can now use this new decorator in other files by doing a regular import:

from decorators import do_twice
```
@do_twice
def say_whee():
    print("Whee!")
```
When you run this example, you should see that the original say_whee() is executed twice:
```
>>> say_whee()
Whee!
Whee!
```

**Decorating Functions With Arguments**

Say that you have a function that accepts some arguments. Can you still decorate it? Let’s try:

from decorators import do_twice
```
@do_twice
def greet(name):
    print(f"Hello {name}")
```
Unfortunately, running this code raises an error:
```
>>> greet("World")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: wrapper_do_twice() takes 0 positional arguments but 1 was given
```
The problem is that the inner function wrapper_do_twice() does not take any arguments, but name="World" was passed to it. You could fix this by letting wrapper_do_twice() accept one argument, but then it would not work for the say_whee() function you created earlier.

The solution is to use *args and **kwargs in the inner wrapper function. Then it will accept an arbitrary number of positional and keyword arguments. Rewrite decorators.py as follows:
```
def do_twice(func):
    def wrapper_do_twice(*args, **kwargs):
        func(*args, **kwargs)
        func(*args, **kwargs)
    return wrapper_do_twice
```
The wrapper_do_twice() inner function now accepts any number of arguments and passes them on to the function it decorates. Now both your say_whee() and greet() examples works:
```
>>> say_whee()
Whee!
Whee!

>>> greet("World")
Hello World
Hello World
```