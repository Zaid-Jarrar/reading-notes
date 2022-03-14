# Python Scope & the LEGB Rule: Resolving Names in Your Code

Reading from [Python Scope & the LEGB Rule](https://realpython.com/python-scope-legb-rule/)

## Understanding Scope

The scope of a name defines the area of a program in which you can unambiguously access that name, such as variables, functions, objects, and so on. A name will only be visible to and accessible by the code in its scope. Several programming languages take advantage of scope for avoiding name collisions and unpredictable behaviors. Most commonly, you’ll distinguish two general scopes:

- Global scope: The names that you define in this scope are available to all your code.

- Local scope: The names that you define in this scope are only available or visible to the code within the scope.

Scope came about because early programming languages (like BASIC) only had global names. With this kind of name, any part of the program could modify any variable at any time, so maintaining and debugging large programs could become a real nightmare. To work with global names, you’d need to keep all the code in mind at the same time to know what the value of a given name is at any time. This was an important side-effect of not having scopes.

Some languages like Python use scope to avoid this kind of problem. When you use a language that implements scope, there’s no way for you to access all the variables in a program at all locations in that program. In this case, your ability to access a given name will depend on where you’ve defined that name.

>Note: You’ll be using the term name to refer to the identifiers of variables, constants, functions, classes, or any other object that can be assigned a name.

The names in your programs will have the scope of the block of code in which you define them. When you can access the value of a given name from someplace in your code, you’ll say that the name is in scope. If you can’t access the name, then you’ll say that the name is out of scope.

## Names and Scopes in Python

Since Python is a dynamically-typed language, variables in Python come into existence when you first assign them a value. On the other hand, functions and classes are available after you define them using def or class, respectively. Finally, modules exist after you import them. As a summary, you can create Python names through one of the following operations:

- Operation >>>>	Statement

- Assignments	>>>> x = value

- Import operations >>>>	import module or from module import name

- Function definitions >>>>	def my_func(): ...

- Argument definitions in the context of functions >>>>	def my_func(arg1, arg2,... argN): ...

- Class definitions >>>>	class MyClass: ...


All these operations create or, in the case of assignments, update new Python names because all of them assign a name to a variable, constant, function, class, instance, module, or other Python object.

>Note: There’s an important difference between assignment operations and reference or access operations. When you reference a name, you’re just retrieving its content or value. When you assign a name, you’re either creating that name or modifying it.

Python uses the location of the name assignment or definition to associate it with a particular scope. In other words, where you assign or define a name in your code determines the scope or visibility of that name.

For example, if you assign a value to a name inside a function, then that name will have a local Python scope. In contrast, if you assign a value to a name outside of all functions—say, at the top level of a module—then that name will have a global Python scope.

## Python Scope vs Namespace

In Python, the concept of scope is closely related to the concept of the namespace. As you’ve learned so far, a Python scope determines where in your program a name is visible. Python scopes are implemented as dictionaries that map names to objects. These dictionaries are commonly called namespaces. These are the concrete mechanisms that Python uses to store names. They’re stored in a special attribute called .__dict__.

Names at the top level of a module are stored in the module’s namespace. In other words, they’re stored in the module’s .__dict__ attribute. Take a look at the following code:

```
>>> import sys
>>> sys.__dict__.keys()
dict_keys(['__name__', '__doc__', '__package__',..., 'argv', 'ps1', 'ps2'])

```

As a further example, suppose that you need to use the name ps1, which is defined in sys. If you know how .__dict__ and namespaces work in Python, then you can reference ps1 in at least two different ways:

- Using the dot notation on the module’s name in the form module.name
- Using a subscription operation on .__dict__ in the form module.__dict__['name']

```
>>> sys.ps1
'>>> '
>>> sys.__dict__['ps1']
'>>> '
```

Once you’ve imported sys you can access ps1 using the dot notation on sys. You can also access ps1 using a dictionary key lookup with the key 'ps1'. Both actions return the same result, '>>> '.

> Note: ps1 is a string specifying the primary prompt of the Python interpreter. ps1 is only defined if the interpreter is in interactive mode and its initial value is '>>> '.


Whenever you use a name, such as a variable or a function name, Python searches through different scope levels (or namespaces) to determine whether the name exists or not. If the name exists, then you’ll always get the first occurrence of it. Otherwise, you’ll get an error. You’ll cover this search mechanism in the next section.

-------------------------------------

