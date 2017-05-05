# Chapter 9: Inheritance & extension

## Python

Python has two built-in functions that work with inheritance:

* Use `isinstance()` to check an instance’s type:

  `isinstance(obj, int)` will be True only if `obj.__class__` is [int](https://docs.python.org/2/library/functions.html#int) or some class derived from [int](https://docs.python.org/2/library/functions.html#int).
* Use `issubclass()` to check class inheritance:

  `issubclass(bool, int)` is `True` since [bool](https://docs.python.org/2/library/functions.html#bool) is a subclass of [int](https://docs.python.org/2/library/functions.html#int). However, `issubclass(unicode, str)` is `False` since [unicode](https://docs.python.org/2/library/functions.html#unicode) is not a subclass of [str](https://docs.python.org/2/library/functions.html#str) (they only share a common ancestor, [basestring](https://docs.python.org/2/library/functions.html#basestring)).

Python support multiple inheritance. A class definition with multiple base classes looks like this:

```python
class DerivedClassName(Base1, Base2, Base3):
    <statement-1>
    .
    .
    .
    <statement-N>
```
For old-style classes, the only rule is depth-first, left-to-right. Thus, if an attribute is not found in **DerivedClassName**, it is searched in **Base1**, then (recursively) in the base classes of **Base1**, and only if it is not found there, it is searched in **Base2**, and so on.

For [*new-style classes*](https://docs.python.org/2/glossary.html#term-new-style-class), the method resolution order changes dynamically to support cooperative calls to [*super()*](https://docs.python.org/2/library/functions.html#super). This approach is known in some other multiple-inheritance languages as call-next-method and is more powerful than the super call found in single-inheritance languages.

With [*new-style classes*](https://docs.python.org/2/glossary.html#term-new-style-class), dynamic ordering is necessary because all cases of multiple inheritance exhibit one or more diamond relationships (where at least one of the parent classes can be accessed through multiple paths from the bottommost class). For example, all new-style classes inherit from [object](https://docs.python.org/2/library/functions.html#object), so any case of multiple inheritance provides more than one path to reach [object](https://docs.python.org/2/library/functions.html#object). To keep the base classes from being accessed more than once, the dynamic algorithm linearizes the search order in a way that preserves the left-to-right ordering specified in each class, that calls each parent only once, and that is monotonic (meaning that a class can be subclassed without affecting the precedence order of its parents). Taken together, these properties make it possible to design reliable and extensible classes with multiple inheritance.

## C`#`

In C#, one class can inherit from another class, and the latter is called base class and provides abstract methods to be implemented by its children. 

C# doesn’t allow multiple inheritance, using interfaces to solve this.

Extension methods in C# are a special kind of static method, but they are called as if they were instance methods on the extended type
The most common extension methods are the LINQ standard query operators that add query functionality, such OrderBy. 

