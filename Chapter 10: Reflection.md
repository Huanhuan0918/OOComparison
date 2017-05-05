# Chapter 10: Reflection

## Python

###  What reflection abilities are supported?

Python has some functions on dealing with reflection. Shown as the following:

* [PyObject<sup>*</sup>](https://docs.python.org/2/c-api/structures.html#c.PyObject) ` PyEval_GetBuiltins()`

  * *Return value: Borrowed reference.*

  * Return a dictionary of the builtins in the current execution frame, or the interpreter of the thread state if no frame is currently executing.

* [PyObject<sup>*</sup>](https://docs.python.org/2/c-api/structures.html#c.PyObject) ` PyEval_GetLocals()`

  * *Return value: Borrowed reference.*

  * Return a dictionary of the local variables in the current execution frame, or NULL if no frame is currently executing.

* [PyObject<sup>*</sup>](https://docs.python.org/2/c-api/structures.html#c.PyObject) ` PyEval_GetGlobals()`

  * *Return value: Borrowed reference.*

  * Return a dictionary of the global variables in the current execution frame, or NULL if no frame is currently executing.

* PyFrameObject\* ` PyEval_GetFrame()`

  * *Return value: Borrowed reference.*

  * Return the current thread state’s frame, which is NULL if no frame is currently executing.

* int ` PyFrame_GetLineNumber(PyFrameObject *frame)`

  * Return the line number that frame is currently executing.

* int `PyEval_GetRestricted()`

  * If there is a current frame and it is executing in restricted mode, return true, otherwise false.

* const char\* `PyEval_GetFuncName(PyObject *func)`

  * Return the name of _func_ if it is a function, class or instance object, else the name of _funcs_ type.

* const char\* `PyEval_GetFuncDesc(PyObject *func)`

  * Return a description string, depending on the type of _func_. Return values include “()” for functions and methods, ”constructor”, ”instance”, and ”object”. Concatenated with the result of [PyEval_GetFuncName()](https://docs.python.org/2/c-api/reflection.html#c.PyEval_GetFuncName), the result will be a description of _func_.

### How is reflection used?

The following source code defines a class with a constructor `__init__()` and two methods. A function introduce() is also defined to provide an example of reflection for method.

```python
class reflect(object):
	'''
	A demo class for Python reflection
	'''
	def __init__(self):
    	'''
    	Constructor for reflect class
    	'''
    	self.name = "Hongbao Chen"
    	self.gender = "Male"
    	self.hobby = "Computer game"

	def message(self):
    	print "I am ", self.name, " and my gender is ", self.gender, "I like ", self.hobby
    	print "How do you do?"

	@classmethod
	def static_message(self):
    	print "I can be called without an instance."

def introduce():
	print "I just introduce myself."
```

Every method inside a class receive a ‘self’ parameter because the ‘self’ will be passed into a reference to it corresponding instance of its class. In the inner virtual machine, the ‘binding’ will save you lots of time and keep you from many troubles.

Function `introduce()` is defined without self as parameter because it is not a instance method nor class method.

### Reflection in Actions

The following codes shows an example on reflection:

```python
from Reflect import reflect
from Reflect import introduce
if __name__ == '__main__':
	ref = reflect()

	print ref.__class__
	print ref.__dict__
	print ref.__doc__
	print ref.__sizeof__()

	print ref.__getattribute__('name')

	ref.__setattr__('name', 'Stranger')
	print ref.name

	introduce()
	ref.intro = introduce;
	ref.intro()

	ref.message()
	ref.message = introduce
	ref.message()

	print ref.__hash__()

	#ref.__delattr__('name')
	print ref.name

	reflect.static_message();
```

The first line is used to get an instance of the certain class. There are several built-in functions for the class can you can use it without importing any libraries.

And then, we assign the introduce function to the ***Reflction*** and then call the `intro()`. we find that the output of the latter is different from the former ones. Note that, the function `intro()` is a new funciton whose name is just been added to class reflect.

The modification of `message()` method is an example of modifying class; inner structure.

We can use `__delattr__(string)` to delete any variable. If you uncomment the last third line, you will find that ‘print’ statement following it will cause error because the attribute in class reflection is deleted by ourselves.

The `object.__doc__()` will return the printable string describing the attributes and their values currently in the class reflect. The `__doc__()` will return the comment for the class. The sizeof() is very useful because it make you a chance to have a look the memory consumption when the design of the new products were changed.

The last line of the second script demonstrate the use of a class method. A class method takes in the first parameter as a class and then can be called in both class and instance.

More information can be found in [*this website*](http://www.assembleforce.com/2012-08/reflection-in-python.h).

## C`#`

###  What reflection abilities are supported?

In C#, reflection provides objects (of type Type) that describe assemblies, modules and types. We could use reflection to dynamically create an instance of a type, bind the type to an existing object, or get the type from an existing object and invoke its methods or access its fields and properties. Reflection also enables us to access attributes if we have attributes in the code. (From MSDN)

### How is reflection used?

```csharp
//using GetType to obtain type information
int i = 42;
System.Type type = i.GetType();
System.Console.WriteLine(type);

//using reflection to get information from an Assembly
System.Reflection.Assembly info = typeof(System.Int32).Assembly;
System.Console.WriteLine(info);
```
