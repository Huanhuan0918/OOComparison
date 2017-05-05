# Chapter 18: Procedural programming

## Python

Since Python is multi-paradigm languages that support several different approaches. Procedural programming approach is supported by python.

Procedural mains tasks are treated as step-by-step iterations where common tasks are placed in functions that are called as needed. This coding style favors iteration, sequencing, selection, and modularization.

The procedural style relies on procedure calls to create modularized code. It seeks to simplify the application code by creating small pieces that a developer can view easily. Even though the procedural coding style is an older form of application development, it’s still a viable approach when a task lends itself to step-by-step execution. Here’s an example of the procedural coding style:

```python
def DoAdd(MyList):
    Sum = 0
    if type(MyList) is list:
        for X in MyList:
            Sum += X
    return Sum
MyList = [1, 2, 3, 4, 5]
print(DoAdd(MyList))
```
Notice how the use of a function, `DoAdd()`, simplifies the overall code in this case. The execution is still systematic, but the code is easier to understand because it’s broken into chunks.

In some point, Python could not to be considered as a procedural language like C. But it can approach some procedure in method case. Here is a [article](http://stackoverflow.com/questions/721090/what-is-the-difference-between-a-function-and-a-procedure) talking about functional and procedural programming.

## C# #

C# does have imperative (procedural) programming characteristics. Functional programming is a form of declarative programming. In contrast, most mainstream languages, including object-oriented programming (OOP) languages such as C#, Visual Basic, C++, and Java –, were designed to primarily support imperative (procedural) programming.

Let's take a look at following example. Some businesses advertise their phone number as a word, phrase or combination of numbers and alpha characters. This is easier for people to remember than a number. You simply dial the numbers on the keypad that correspond to the characters. For example, “1-800 FLOWERS” translates to 1-800 3569377.

We will write a simple program that translates a word into a list of corresponding numbers.

First, let’s start with a dictionary that contains each number and the corresponding characters:

```csharp
private readonly Dictionary<int, char[]> keys =
            new Dictionary<int, char[]>()
                {
                    {1, new char[] {}},
                    {2, new[] {'a', 'b', 'c'}},
                    {3, new[] {'d', 'e', 'f'}},
                    {4, new[] {'g', 'h', 'i'}},
                    {5, new[] {'j', 'k', 'l'}},
                    {6, new[] {'m', 'n', 'o'}},
                    {7, new[] {'p', 'q', 'r', 's'}},
                    {8, new[] {'t', 'u', 'v'}},
                    {9, new[] {'w', 'x', 'y', 'z'}},
                    {0, new[] {' '}},
                };
```

Next, we create a Translate method that takes a word and returns an array of corresponding numbers.

With a traditional, imperative approach, we would use for-each loops and if-statements to iterate through characters and populate an array of matching numbers:

```csharp
public int[] Translate(string word)
{
    ArrayList numbers = new ArrayList();
 
    foreach (char character in word)
    {
        foreach(KeyValuePair<int, char[]> key in keys)
        {
            foreach(char c in key.Value)
            {
                if(c == character)
                {
                    numbers.Add(key.Key);
                }
            }
        }
    }
 
    return (int[]) numbers.ToArray(typeof (int));
}
```

Alternatively, with a functional approach we can use LINQ to select elements from the dictionary and transform the output to an array of matching numbers:

```csharp
public int[] Translate(string word)
{
    return word.Select(c => 
        keys.First(k => k.Value.Contains(c)).Key).ToArray();
}
```

We see that functional programming is much cleaner and easier than procedural programming in this case. We'll be looking at functional programming in next module.


