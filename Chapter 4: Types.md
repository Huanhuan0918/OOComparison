# Chapter 4: Types

## Python

### What types does the language support?

Python's built-in (or standard) data types can be grouped into several classes. Sticking to the hierarchy scheme used in the official Python documentation these are **numeric types**, **sequences**, **sets** and **mappings** (and a few more not discussed further here). Some of the types are only available in certain versions of the language as noted below.

- **boolean**: The type of the built-in values True and False. Useful in conditional expressions, and anywhere else you want to represent the truth or falsity of some condition. Mostly interchangeable with the integers 1 and 0. In fact, conditional expressions will accept values of any type, treating special ones like boolean False, integer 0 and the empty string "" as equivalent to False, and all other values as equivalent to True. But for safety’s sake, it is best to only use boolean values in these places.

- Numeric types:
  - **int**: Integers; equivalent to C longs in Python 2.x, non-limited length in Python 3.x
  - **long**: Long integers of non-limited length; exists only in Python 2.x
  - **float**: Floating-Point numbers, equivalent to C doubles
  - **complex**: Complex Numbers

- Sequences:
  - **str**: String; represented as a sequence of 8-bit characters in Python 2.x, but as a sequence of Unicode characters (in the range of U+0000 - U+10FFFF) in Python 3.x
  - **bytes**: a sequence of integers in the range of 0-255; only available in Python 3.x
  - **byte array**: like bytes, but mutable (see below); only available in Python 3.x
  - **list**
  - **tuple**

- Sets:
  - **set**: an unordered collection of unique objects; available as a standard type since Python 2.6
  - **frozen set**: like set, but immutable (see below); available as a standard type since Python 2.6

- Mappings:
  - **dict**: Python dictionaries, also called hashmaps or associative arrays, which means that an element of the list is associated with a definition.

- More:
  Can be found in [*This Website*](https://en.wikibooks.org/wiki/Python_Programming/Data_Types).

### Are both reference and value types supported?

Python uses a mechanism, which is known as "[Call-by-Object](http://stackoverflow.com/questions/10844088/python-what-is-the-difference-between-call-by-value-and-call-by-object)", sometimes also called "Call by Object Reference" or "Call by Sharing".

If you pass immutable arguments like integers, strings or tuples to a function, the passing acts like call-by-value. If we pass mutable arguments. They are also passed by object reference, but they can be changed in place in the function.
Anyway, Python initially behaves like call-by-reference, but as soon as we are changing the value of such a variable, Python "switches" to call-by-value.

### Can new value types be created?

**Yes!** The Python runtime sees all Python objects as variables of type PyObject, which serves as a “base type” for all Python objects. PyObject itself only contains the refcount and a pointer to the object’s “type object”. So, if you want to define a new object type, you need to create a new type object.

## C# #

### What types does the language support?

C# supports both value type and reference type. 

### Are both reference and value types supported?

Yes.

### Can new value types be created?

Yes, there are user defined value types in C#, such as Struct.

```
// user defined value type Point
public final class Point extends System.ValueType
{
    public int x;
    public int y;
}
class CMain
{
    public static void main()
    {
        Point p = new Point();
        p.x = 5;
        p.y = 10;
        System.Console.WriteLine("Point [x,y] = " + p.x + ", " + p.y);
    }
}
```
- Reference:
  MSDN: https://msdn.microsoft.com/en-us/library/wysdab55(v=vs.80).aspx
