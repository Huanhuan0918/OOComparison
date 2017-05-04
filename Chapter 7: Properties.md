# Chapter 7: Properties

## Python

### Getters and setters...write your own or built in?

Getters and setters are used in many object oriented programming languages to ensure the principle of data encapsulation.A method which is used for getting a value is decorated with "`@property`", i.e. we put this line directly in front of the header. The method which has to function as the setter is decorated with "`@x.setter`". If the function had been called "f", we would have to decorate it with "`@f.setter`".

Two things are noteworthy: We just put the code line "`self.x = x`" in the `__init__` method and the property method x is used to check the limits of the values. The second interesting thing is that we wrote "two" methods with the same name and a different number of parameters "`def x(self)`" and "`def x(self,x)`".

The following example shows a class, which has internal attributes, which can't be accessed from outside. These are the private attributes `self.__potential_physical` and `self.__potential_psychic`. Furthermore we show that a property can be deduced from the values of more than one attribute. The property "condition" of our example returns the condition of the robot in a descriptive string. The condition depends on the sum of the values of the psychic and the physical conditions of the robot.

```python
class Robot:

    def __init__(self, name, build_year, lk = 0.5, lp = 0.5 ):
        self.name = name
        self.build_year = build_year
        self.__potential_physical = lk
        self.__potential_psychic = lp

    @property
    def condition(self):
        s = self.__potential_physical + self.__potential_psychic
        if s <= -1:
           return "I feel miserable!"
        elif s <= 0:
           return "I feel bad!"
        elif s <= 0.5:
           return "Could be worse!"
        elif s <= 1:
           return "Seems to be okay!"
        else:
           return "Great!"

if __name__ == "__main__":
    x = Robot("Marvin", 1979, 0.2, 0.4 )
    y = Robot("Caliban", 1993, -0.4, 0.3)
    print(x.condition)
    print(y.condition)
```

### Backing variables & Computed properties

The easiest way to implement a computed attribute is with an object of type **property**, introduced in Python 2.2. Depending on the way you access a property object, it dispatches a function to perform either a "get the value" operation or a "set the value" operation (or even "delete the attribute"). You specify the dispatch functions when you create the property object; it's up to you to ensure that the work they do makes sense. The following diagram illustrates how a property works.

![alt text](https://wiki.python.org/moin/ComputedAttributesUsingPropertyObjects?action=AttachFile&do=get&target=py-props.png "Logo Title Text 1")

Some tips should attention:
* In Python 2.x, a class containing a computed attribute must be based on the type object.
* In Python 3.x, all classes are automatically based on object, so you can code the class statement either way.
The property object must be assigned to a class attribute.

## C`#`

heiheiheiheiheihei
