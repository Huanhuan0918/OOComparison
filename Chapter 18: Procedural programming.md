# Chapter 18: Procedural programming

## Python

Since Python is multi-paradigm languages that support several different approaches. Procedural programming approach is supported by python.

Procedural mains tasks are treated as step-by-step iterations where common tasks are placed in functions that are called as needed. This coding style favors iteration, sequencing, selection, and modularization.

The procedural style relies on procedure calls to create modularized code. It seeks to simplify the application code by creating small pieces that a developer can view easily. Even though the procedural coding style is an older form of application development, it’s still a viable approach when a task lends itself to step-by-step execution. Here’s an example of the procedural coding style:

```python
def DoAdd(MyList):
    Sum = 0
    if type(MyList) is list:
        for X in MyList:
            Sum += X
    return Sum
MyList = [1, 2, 3, 4, 5]
print(DoAdd(MyList))
```
Notice how the use of a function, `DoAdd()`, simplifies the overall code in this case. The execution is still systematic, but the code is easier to understand because it’s broken into chunks.

In some point, Python could not to be considered as a procedural language like C. But it can approach some procedure in method case. Here is a [article](http://stackoverflow.com/questions/721090/what-is-the-difference-between-a-function-and-a-procedure) talking about functional and procedural programming.

## C`#`

houhouhouhou
