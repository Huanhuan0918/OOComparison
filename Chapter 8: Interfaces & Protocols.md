# Chapter 8: Interfaces & Protocols

## Python

Python support **protocols** instead of interface. There is no interface definition in Python.The closest thing is probably the abstract base classes module, which allows to define common methods for a set of classes. Since Python support multiple inheritance, so in some kind of situation, we can create something seems like a interface. The abstract base classes module to do this can be seen in `abc` API:

Abstract base classes are a form of interface checking more strict than individual `hasattr()` checks for particular methods. By defining an abstract base class, you can define a common API for a set of subclasses. This capability is especially useful in situations where a third-party is going to provide implementations, such as with plugins to an application, but can also aid you when working on a large team or with a large code-base where keeping all classes in your head at the same time is difficult or not possible.

When defined the ABC, put all of the Interface-like methods in it and have in their body either `pass` or `raise NotImplementedError`. The child classes inherit from your ABC and override these methods just like any other child class overrides parent class methods. (Since Python has multiple inheritance, they can inherit from your ABC plus any other class you like.)

`abc` works by marking methods of the base class as abstract, and then registering concrete classes as implementations of the abstract base. If your code requires a particular API, you can use `issubclass()` or `isinstance()` to check an object against the abstract class.

In python libaray, This module provides the infrastructure for defining [abstract base classes (ABCs)](https://docs.python.org/3/glossary.html#term-abstract-base-class) in Python, as outlined in [PEP 3119](https://www.python.org/dev/peps/pep-3119); see the PEP for why this was added to Python. (See also [PEP 3141](https://www.python.org/dev/peps/pep-3141) and the [numbers](https://docs.python.org/3/library/numbers.html#module-numbers) module regarding a type hierarchy for numbers based on ABCs.)

The [collections](https://docs.python.org/3/library/collections.html#module-collections) module has some concrete classes that derive from ABCs; these can, of course, be further derived. In addition the [collections.abc](https://docs.python.org/3/library/collections.abc.html#module-collections.abc) submodule has some ABCs that can be used to test whether a class or instance provides a particular interface, for example, is it hashable or a mapping.

Here is an example defining an abstract base class to represent the API of a set of plugins for saving and loading data.

```python
import abc

class PluginBase(object):
    __metaclass__ = abc.ABCMeta

    @abc.abstractmethod
    def load(self, input):
        """Retrieve data from the input source and return an object."""
        return

    @abc.abstractmethod
    def save(self, output, data):
        """Save the data object to the output."""
        return
```

By subclassing directly from the base, we can avoid the need to register the class explicitly.

```python
import abc
from abc_base import PluginBase

class SubclassImplementation(PluginBase):

    def load(self, input):
        return input.read()

    def save(self, output, data):
        return output.write(data)

if __name__ == '__main__':
    print 'Subclass:', issubclass(SubclassImplementation, PluginBase)
    print 'Instance:', isinstance(SubclassImplementation(), PluginBase)
```

## C# #

### What does the language support?

C# supports interfaces.

### What abilities does it have?

Using interfaces you can include behavior from multiple sources in a class, which is important since C# doesn’t support multiple inheritance. In addition, you must use an interface if you want to simulate inheritance for structs, because they can't actually inherit from another struct or class. (From MSDN)
Also, in C# interfaces start with I, such as IEnumerable, IQueryable or some other user defined interfaces.

### How is it used?

To use interfaces in C#, simply use colon “:” after a class, and if you want to implement multiple interfaces, use coma “,” to separate interfaces. 

To define interface:

```csharp
    interface ISomething<T>
    {
        //implementation goes here
    }
```

To use interface:

```csharp
    public class Car : ISomething<Car>
    {
        public string Make {get; set;}
        public string Model { get; set; }
        public string Year { get; set; }

        // Implementation of ISomething<T> interface
        public bool Equals(Car car)
        {
            if (this.Make == car.Make &&
                this.Model == car.Model &&
                this.Year == car.Year)
            {
                return true;
            }
            else
                return false;
        }
    }
```



