# Chapter 5: Classes

## Python

### Defining

The simplest form of class definition looks like this:

```python
class ClassName:
    <statement-1>
    ...
    ...
    <statement-N>
```

### Creating new instances

Class ***instantiation*** uses function notation. Just pretend that the class object is a parameterless function that returns a new instance of the class. For example (assuming the above class): `x = MyClass()`creates a new ***instance*** of the class and assigns this object to the local variable x.

### Constructing & Initializing

The first method ***\__init\__()*** is a special method, which is called class constructor or initialization method that Python calls when you create a new instance of this class. The following code shows the details.
```python
class Employee:
   'Common base class for all employees'
   empCount = 0

   def __init__(self, name, salary):
      self.name = name
      self.salary = salary
      Employee.empCount += 1

   def displayCount(self):
     print "Total Employee %d" % Employee.empCount

   def displayEmployee(self):
      print "Name : ", self.name,  ", Salary: ", self.salary
```

### Destructing/de-initializing

Object ***\__del\__(self)*** called when the instance is about to be destroyed. This is also called a destructor. If a base class has a *\__del\__()* method, the derived class’s *\__del\__()* method, if any, must explicitly call it to ensure proper deletion of the base class part of the instance. Note that it is possible (though not recommended!) for the *\__del\__()* method to postpone destruction of the instance by creating a new reference to it. It may then be called at a later time when this new reference is deleted. It is not guaranteed that *\__del\__()* methods are called for objects that still exist when the interpreter exits.

## C`#`

hahahaha
