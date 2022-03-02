
# Reading and Writing Files in Python (Guide)

Reading from [Reading and Writing Files in Python](https://realpython.com/read-write-files-python/#what-is-a-file)

## What is a file
A file is a contiguous set of bytes used to store data. This data is organized in a specific format and can be anything as simple as a text file or as complicated as a program executable. In the end, these byte files are then translated into binary 1 and 0 for easier processing by the computer.

Files on most modern file systems are composed of three main parts:

Header: metadata about the contents of the file (file name, size, type, and so on)
Data: contents of the file as written by the creator or editor
End of file (EOF): special character that indicates the end of the file

## Opening and Closing a File in Python

open() has a single required argument that is the path to the file. open() has a single return, the file object:
```
 file = open('dog_breeds.txt')

```
### ways to close the file:

- The try-finally block
  
```
  reader = open('dog_breeds.txt')
  try:
     Further file processing goes here
   finally:
    reader.close()
 ```

- Use the with statement:

 ```
with open('dog_breeds.txt') as reader:

    Further file processing goes here

```

The with statement automatically takes care of closing the file once it leaves the with block, even in cases of error. I highly recommend that you use the with statement as much as possible, as it allows for cleaner code and makes handling any unexpected errors easier for you.

Most likely, you’ll also want to use the second positional argument, mode. This argument is a string that contains multiple characters to represent how you want to open the file. The default and most common is 'r', which represents opening the file in read-only mode as a text file:

```
with open('dog_breeds.txt', 'r') as reader:
    # Further file processing goes here

```


Character---------->Meaning <br>
'r'	---------->Open for reading (default) <br>
'w'	---------->Open for writing, truncating (overwriting) the file first <br>
'rb' or 'wb'---------->	Open in binary mode (read/write using byte data) <br>


There are three different categories of file objects:

- Text files
- Buffered binary files
- Raw binary files


### Reading and Writing Opened Files

Method: 
- .read(size=-1) ----> This reads from the file based on the number of size bytes. If no argument is passed or None or -1 is passed, then the entire file is read.
- .readline(size=-1)  ----> This reads at most size number of characters from the line. This continues to the end of the line and then wraps back around. If no argument is passed or None or -1 is passed, then the entire line (or rest of the line) is read.
- .readlines()  ----> This reads the remaining lines from the file object and returns them as a list.

---------------------------------------

# Python Exceptions: An Introduction

### Exceptions versus Syntax Errors

Reading from [Python Exceptions: An Introduction](https://realpython.com/python-exceptions/)

Syntax errors are errors where the program cant run if they exist and the programmer has to delete and fix that error to proceed 

Exceptions errors occurs when the code is run but face an error like typeerror, valueerror... etc
where it can be cought and dealt with and made it output something when something like that happens again and wont break python code.

```
print( 0 / 0 ))
  File "<stdin>", line 1
    print( 0 / 0 ))
                  ^
SyntaxError: invalid syntax

```

```
>>> print( 0 / 0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: integer division or modulo by zero

```

### Raising an Exception
We can use raise to throw an exception if a condition occurs. The statement can be complemented with a custom exception.


```
x = 10
if x > 5:
    raise Exception('x should not exceed 5. The value of x was: {}'.format(x))
```

When you run this code, the output will be the following:

```
Traceback (most recent call last):
  File "<input>", line 4, in <module>
Exception: x should not exceed 5. The value of x was: 10
```


### The try and except Block: Handling Exceptions

The try and except block in Python is used to catch and handle exceptions. Python executes code following the try statement as a “normal” part of the program. The code that follows the except statement is the program’s response to any exceptions in the preceding try clause.

```
try:
    linux_interaction()
except:
    print('Linux function was not executed')
```

When an exception occurs in a program running this function, the program will continue as well as inform you about the fact that the function call was not successful.

What you did not get to see was the type of error that was thrown as a result of the function call. In order to see exactly what went wrong, you would need to catch the error that the function threw.

The following code is an example where you capture the AssertionError and output that message to screen:
```
try:
    linux_interaction()
except AssertionError as error:
    print(error)
    print('The linux_interaction() function was not executed')
```
```
Shell
Function can only run on Linux systems.
The linux_interaction() function was not executed
```

Here’s another example where you open a file and use a built-in exception:
```
try:
    with open('file.log') as file:
        read_data = file.read()
except:
    print('Could not open file.log')
```
If file.log does not exist, this block of code will output the following:
```
Could not open file.log
```

You can have more than one function call in your try clause and anticipate catching various exceptions. A thing to note here is that the code in the try clause will stop as soon as an exception is encountered.
```
try:
    linux_interaction()
    with open('file.log') as file:
        read_data = file.read()
except FileNotFoundError as fnf_error:
    print(fnf_error)
except AssertionError as error:
    print(error)
    print('Linux linux_interaction() function was not executed')

```

If the file does not exist, running this code on a Windows machine will output the following:
```
Function can only run on Linux systems.
Linux linux_interaction() function was not executed
```

Here are the key takeaways:

- A try clause is executed up until the point where the first exception is encountered.
- Inside the except clause, or the exception handler, you determine how the program responds to the exception.
- You can anticipate multiple exceptions and differentiate how the program should respond to them.
- Avoid using bare except clauses.

### The else Clause

In Python, using the else statement, you can instruct a program to execute a certain block of code only in the absence of exceptions.

```
try:
    linux_interaction()
except AssertionError as error:
    print(error)
else:
    print('Executing the else clause.')
```
If you were to run this code on a Linux system, the output would be the following:
```
Doing something.
Executing the else clause.
```
Because the program did not run into any exceptions, the else clause was executed.

You can also try to run code inside the else clause and catch possible exceptions there as well:
```
try:
    linux_interaction()
except AssertionError as error:
    print(error)
else:
    try:
        with open('file.log') as file:
            read_data = file.read()
    except FileNotFoundError as fnf_error:
        print(fnf_error)
```
If you were to execute this code on a Linux machine, you would get the following result:
```
Doing something.
[Errno 2] No such file or directory: 'file.log'
```
From the output, you can see that the linux_interaction() function ran. Because no exceptions were encountered, an attempt to open file.log was made. That file did not exist, and instead of opening the file, you caught the FileNotFoundError exception.

### Cleaning Up After Using finally

Imagine that you always had to implement some sort of action to clean up after executing your code. Python enables you to do so using the finally clause.

```
try:
    linux_interaction()
except AssertionError as error:
    print(error)
else:
    try:
        with open('file.log') as file:
            read_data = file.read()
    except FileNotFoundError as fnf_error:
        print(fnf_error)
finally:
    print('Cleaning up, irrespective of any exceptions.')
```
In the this code, everything in the finally clause will be executed. It does not matter if you encounter an exception somewhere in the try or else clauses. Running the ths code on a Windows machine would output the following:

```
Function can only run on Linux systems.
Cleaning up, irrespective of any exception
```

### Summing Up

After seeing the difference between syntax errors and exceptions, i have learned about how  to raise, catch, and handle exceptions in Python, such as:

- raise allows you to throw an exception at any time.
- assert enables you to verify if a certain condition is met and throw an exception if it isn’t.
- In the try clause, all statements are executed until an exception is encountered.
- except is used to catch and handle the exception(s) that are encountered in the try clause.
- else lets you code sections that should run only when no exceptions are encountered in the try clause.
- finally enables you to execute sections of code that should always run, with or without any previously encountered exceptions.