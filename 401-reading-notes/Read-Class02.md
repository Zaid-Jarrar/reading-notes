## Unit tests and TDD?
Reading from [In Tests We Trust — TDD with Python](https://code.likeagirl.io/in-tests-we-trust-tdd-with-python-af69f47e6932)

Unit tests are some pieces of code to exercise the input, the output and the behaviour of your code. You can write them anytime you want.

But Test-Driven Development is a strategy to think (and write!) tests first.

### Important aspects about the unit test

-  The test file name should follow the same name of module name. For instance, if our module is gender.py, our test name should be test_gender.py. It’s ideal to separate the tests folder from production code (the implementation) and to have something like this: 

> mymodule/
 — module.py
 — another_folder/
 — — another_module.py
tests/
 — test_module.py
 — another_folder/
 — — test_another_module.py

- Other thing to care about is the structure. A convention widely used is the AAA: **Arrange**, **Act** and **Assert**.
Arrange: you need to organize the data needed to execute that piece of code (input);
Act: here you will execute the code being tested (exercise the behaviour);
Assert: after executing the code, you will check if the result (output) is the same as you were expecting.

## The Cycle

The cycle is made by three steps:

- 🆘 Write a unit test and make it fail 
- ✅ Write the feature and make the test pass! 
- 🔵 Refactor the code — the first version doesn’t need to be the beautiful one

Using baby steps you can go through this cycle every time you add or modify a new feature in your code.
 what is needed to make this test pass? Don’t think about the whole feature, just about the test.

**Note:**
 > When we are writing tests we are forced to think about the design first and how we can break it into small pieces.

**My conclusion:**
so my take away from this is, write a unit test and don't be afraid if it fails then think of the design of the code so i can break it into small pieces and refactor my code even it doesnt look good at first then make it work and pass, while mantaining the 3 As Arrange, Act, Assert.

-----------------------------------------------------------



## What does the if __name__ == “__main__”: do?  

Reading from [If name equals main](https://www.geeksforgeeks.org/what-does-the-if-__name__-__main__-do/)

firstly, a module is a file containing Python definitions and statements. The file name is the module name with the suffix .py appended.

if __name__ == “__main__” only gets executed if it is called directly and not imported. so it can be used to stop unnecessaray code from running when importing to over files.

Also has the following advantages:

- > Every Python module has it’s __name__ defined and if this is ‘__main__’, it implies that the module is being run standalone by the user and we can do corresponding appropriate actions.
-  >If you import this script as a module in another script, the __name__ is set to the name of the script/module.
- > Python files can act as either reusable modules, or as standalone programs.
-  >if __name__ == “main”: is used to execute some code only if the file was run directly, and not imported.

-------------------------------------------------------------

## Recursion

it is a function that recursively calls it self over and over again until it reaches what is called a base value, which will solve the whole function and stop the function from endlessly calling itself.  The recusion works on multiple ns not one but many which make the problem smaller and smaller until we get to the base and they all meet in a stack.
```
for example:
def factorial (n)
    if n == 1:
        return 1
    else: 
        return n * factorial(n-1)
```
factorial (4) 
that is divided into different values of n until we can solve it.

factorial (4) = 4 * factorial(3) * 3 * factorial(2) * 2 * factorial(1) * 1

pending multiply is what each stack is doing to multiply

4 * factorial(3)  // top of the stack

1          // base value bottom of the stack