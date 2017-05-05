# Chapter 6: Instance reference name in data type (class)

## Python

### *this()* or *self()*?

In python, we use `self`. Python does not use the `@` syntax to refer to instance attributes. Python decided to do methods in a way that makes the instance to which the method belongs be *passed* automatically, but not *received* automatically: the first parameter of methods is the instance the method is called on. That makes methods entirely the same as functions, and leaves the actual name to use up to you (although `self` is the convention, and people will generally frown at you when you use something else.) `self` is not special to the code, it's just another object.

The especially in Python is `self` is not a method. Moreover, the name self can be anything. It's not a keyword, as you already know. you can even change it to this, and it will work fine. But people like to use `self`, as it has now become a bit of a convention.
Others, self cannot be omitted when we must passed as an instance in the function. In inheritance, which instance is passed to the child class, the instances in the child class will be the instance which passed, not the instance parent node has in itself. Here is some code example:

```python
class Parent:
    def pprt(self):
        print(self)

class Child(Parent):
    def cprt(self):
        print(self)
```
```python
c = Child()
c.cprt()
c.pprt()
p = Parent()
p.pprt()
```
The sesult shows:

```python
<__main__.Child object at 0x0000000002A47080>
<__main__.Child object at 0x0000000002A47080>
<__main__.Parent object at 0x0000000002A47240>
```

The reason why c.pprt() function calls the object the same as c.cprt() is because when the function called, it presented Child.pprt(t) called, so this will called the instance of child, not parent.

## C# #

### *this()* or *self()*?

The this keyword refers to the current instance of the class and is also used as a modifier of the first parameter of an extension method.

```csharp
  public Employee(string name, string alias)
  {
        // Use this to qualify the fields, name and alias:
        this.name = name;
        this.alias = alias;
  }
```
