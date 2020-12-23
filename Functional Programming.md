# Functional Programming

[freeCodeCamp](https://www.freecodecamp.org/) explains: 

*Functional programming is an approach to software development based around the evaluation of functions. Like mathematics, functions in programming map input to output to produce a result. You can combine basic functions in many ways to build more and more complex programs.*

*Functional programming follows a few core principles:*

- *Functions are independent from the state of the program or global variables. They only depend on the arguments passed into them to make a calculation.*
- *Functions try to limit any changes to the state of the program and avoid changes to the global objects holding data.*
- *Functions have minimal side effects in the program.*

*The functional programming software development approach breaks a program into small, testable parts. *

Thanks, freeCodeCamp.

A common way to think about programming is in terms of inputs and outputs. 

Your code processes an input and provides an output. When you use functions are the process, you are performing functional programming.

Here are three principles:

1) Isolated functions - there is no dependence on the state of the program, which includes global variables that are subject to change
2) Pure functions - the same input always gives the same output
3) Functions with limited side effects - any changes, or mutations, to the state of the program outside the function are carefully controlled

## Terminology
*Callbacks*: functions that are passed into another function to decide the invocation of that function. For example, `filter()` requires a callback function that tells JavaScript how (the criteria) to filter an array.

Functions that can be assigned to a variable, passed into a function, or returned from another function are called *first class* functions. In JavaScript, every function is *first class*.

However, if a function takes in another function as an argument, it becomes a *higher order* function. The function that gets passed in or returned can be called a *lambda*.

## Higher Order Functions
