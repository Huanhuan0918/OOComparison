# Chapter 19: Functional programming

## Python

Since Python is multi-paradigm languages that support several different approaches. Functional programming is support in Python. In a functional program, input flows through a set of functions. Each function operates on its input and produces some output. Functional style discourages functions with side effects that modify internal state or make other changes that aren’t visible in the function’s return value. Functions that have no side effects at all are called purely functional. Avoiding side effects means not using data structures that get updated as a program runs; every function’s output must only depend on its input.

Python programs written in functional style usually won’t go to the extreme of avoiding all I/O or all assignments; instead, they’ll provide a functional-appearing interface but will use non-functional features internally. For example, the implementation of a function will still use assignments to local variables, but won’t modify global variables or have other side effects.

In this section, I would introduce some language features that are important foundations for writing functional-style programs.

### Iterators

An iterator is an object representing a stream of data; this object returns the data one element at a time. A Python iterator must support a method called `next()` that takes no arguments and always returns the next element of the stream. If there are no more elements in the stream, `next()` must raise the `StopIteration` exception. Iterators don’t have to be finite, though; it’s perfectly reasonable to write an iterator that produces an infinite stream of data.

The built-in `iter()` function takes an arbitrary object and tries to return an iterator that will return the object’s contents or elements, raising `TypeError` if the object doesn’t support iteration. Several of Python’s built-in data types support iteration, the most common being lists and dictionaries. An object is called an **iterable** object if you can get an iterator for it.

Built-in functions such as `max()` and `min()` can take a single iterator argument and will return the largest or smallest element. The `"in"` and `"not in"` operators also support iterators: `X in iterator` is true if X is found in the stream returned by the iterator. You’ll run into obvious problems if the iterator is infinite; `max()`, `min()` will never return, and if the element X never appears in the stream, the `"in"` and `"not in"` operators won’t return either.

### Generators

Generators are a special class of functions that simplify the task of writing iterators. Regular functions compute a value and return it, but generators return an iterator that returns a stream of values.

Here’s the simplest example of a generator function:

```python
def generate_ints(N):
    for i in range(N):
        yield i
```

Any function containing a `yield` keyword is a generator function; this is detected by Python’s [bytecode](https://docs.python.org/2/glossary.html#term-bytecode) compiler which compiles the function specially as a result.

### Built-in functions

Two of Python’s built-in functions, `map()` and `filter()`, are somewhat obsolete; they duplicate the features of list comprehensions but return actual lists instead of iterators.

`map(f, iterA, iterB, ...)` returns a list containing `f(iterA[0], iterB[0]), f(iterA[1], iterB[1]), f(iterA[2], iterB[2]), ....`

`filter(predicate, iter)` returns a list that contains all the sequence elements that meet a certain condition, and is similarly duplicated by list comprehensions. A **predicate** is a function that returns the truth value of some condition; for use with `filter()`, the predicate must take a single value.

### Small functions and the lambda expression

This can be seen in [Chapter 15: Lambda expressions, closures, or functions as types](https://github.com/juchen0401/OOComparison/blob/master/Chapter%2015:%20Lambda%20expressions%2C%20closures%2C%20or%20functions%20as%20types.md)

### The itertools module

The `itertools` module contains a number of commonly-used iterators as well as functions for combining several iterators. This section will introduce the module’s contents by showing small examples.

The module’s functions fall into a few broad classes:

* Functions that create a new iterator based on an existing iterator.

* Functions for treating an iterator’s elements as function arguments.

* Functions for selecting portions of an iterator’s output.

* A function for grouping an iterator’s output.

### The functools module
The `functools` module in Python 2.5 contains some higher-order functions. A **higher-order function** takes one or more functions as input and returns a new function. The most useful tool in this module is the `functools.partial()` function.

For programs written in a functional style, you’ll sometimes want to construct variants of existing functions that have some of the parameters filled in. Consider a Python function `f(a, b, c)`; you may wish to create a new function `g(b, c)` that’s equivalent to `f(1, b, c)`; you’re filling in a value for one of `f()`‘s parameters. This is called “partial function application”.

The constructor for `partial` takes the arguments `(function, arg1, arg2, ... kwarg1=value1, kwarg2=value2)`. The resulting object is callable, so you can just call it to invoke `function` with the filled-in arguments.

Here’s a small but realistic example:

```python
import functools

def log (message, subsystem):
    "Write the contents of 'message' to the specified subsystem."
    print '%s: %s' % (subsystem, message)
    ...

server_log = functools.partial(log, subsystem='server')
server_log('Unable to open socket')
```

### The operator module

The `operator` module was mentioned earlier. It contains a set of functions corresponding to Python’s operators. These functions are often useful in functional-style code because they save you from writing trivial functions that perform a single operation.

Some of the functions in this module are:

* Math operations: `add()`, `sub()`, `mul()`, `div()`, `floordiv()`, `abs()`, ...
* Logical operations: `not_()`, `truth()`.
* Bitwise operations: `and_()`, `or_()`, `invert()`.
* Comparisons: `eq()`, `ne()`, `lt()`, `le()`, `gt()`, and `ge()`.
* Object identity: `is_()`, `is_not()`.

Consult the operator module’s documentation for a complete list.

### References

All the text above are collection from this [website](https://docs.python.org/2/howto/functional.html#the-functools-module).

## C`#`

heiheihei
