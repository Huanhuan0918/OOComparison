# Chapter 15: Lambda expressions, closures, or functions as types

## Python

The lambda operator or lambda function is a way to create small anonymous functions, i.e. functions without a name. These functions are throw-away functions, i.e. they are just needed where they have been created. Lambda functions are mainly used in combination with the functions `filter()`, `map()` and `reduce()`.
The following example of a lambda function returns the sum of its two arguments:

```
>>> f = lambda x, y : x + y
>>> f(1,1)
2
```

In Python, lambda-expression may only have a single expression for its body, and no `return` statement is permitted. In Java, you can do something like this: `(int a, int b) -> { return a * b; };` and other optional things as well.

## C# #

In C#, lambda expression is an anonymous function used to create delegates or expression tree types; to write local functions that can be passed as arguments or returned as the value of function calls. Lambda expressions are mostly helpful for writing LINQ query expressions. 
Use => in Lambda expressions.

```csharp
int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };  
int oddNumbers = numbers.Count(n => n % 2 == 1);  
```
