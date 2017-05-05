# Chapter 14: Errors and exception handling

## Python

There are (at least) two distinguishable kinds of errors: *syntax errors* and *exceptions*.

Syntax errors, also known as parsing errors:

```
>>> while True print('Hello world')
File "<stdin>", line 1
while True print('Hello world')
             ^
SyntaxError: invalid syntax
```

Even if a statement or expression is syntactically correct, it may cause an error when an attempt is made to execute it. Errors detected during execution are called *exceptions*.

It is possible to write programs that handle selected exceptions. Look at the following example, which asks the user for input until a valid integer has been entered, but allows the user to interrupt the program; note that a user-generated interruption is signalled by raising the [*KeyboardInterrupt*](https://docs.python.org/3/library/exceptions.html#KeyboardInterrupt) exception.

```python
while True:
    try:
      x = int(input("Please enter a number: "))
      break
    except ValueError:
      print("Oops!  That was no valid number.  Try again...")
```

The [try](https://docs.python.org/3/reference/compound_stmts.html#try) statement works as follows.

* First, the *try* clause (the statement(s) between the [try](https://docs.python.org/3/reference/compound_stmts.html#try) and [except](https://docs.python.org/3/reference/compound_stmts.html#except) keywords) is executed.

* If no exception occurs, the except clause is skipped and execution of the [try](https://docs.python.org/3/reference/compound_stmts.html#try) statement is finished.

* If an exception occurs during execution of the try clause, the rest of the clause is skipped. Then if its type matches the exception named after the except keyword, the [except](https://docs.python.org/3/reference/compound_stmts.html#except) clause is executed, and then execution continues after the [try](https://docs.python.org/3/reference/compound_stmts.html#try) statement.

* If an exception occurs which does not match the exception named in the except clause, it is passed on to outer [try](https://docs.python.org/3/reference/compound_stmts.html#try) statements; if no handler is found, it is an unhandled exception and execution stops with a message as shown above.

A try statement may have more than one except clause, to specify handlers for different exceptions. At most one handler will be executed. Handlers only handle exceptions that occur in the corresponding [try](https://docs.python.org/3/reference/compound_stmts.html#try) clause, not in other handlers of the same [try](https://docs.python.org/3/reference/compound_stmts.html#try) statement.

## C`#`

In C#, we use try-catch-finally blocks to handle exceptions and throw errors and possibly log them. For Catch blocks, there could be multiple, from most specific to least. A finally block will be executed no matter exception occurs or not.

```csharp
            try
            {
                string s = null;
                ProcessString(s);
            }
            // Most specific:
            catch (ArgumentNullException e)
            {
                Console.WriteLine("{0} First exception caught.", e);
            }
            // Least specific:
            catch (Exception e)
            {
                Console.WriteLine("{0} Second exception caught.", e);
            }
            finally()
            {
               //something that will be done no matter what
            }
            }

```
