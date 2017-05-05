# Chapter 12: Comparisons of references and values

## Python

### How are values compared?

`is` will return `True` if two variables point to the same object, `==` if the objects referred to by the variables are equal.
      >>> 1000 is 10**3 False
      >>> 1000 == 10**3 True

## C# #

### How are values compared? (i.e. comparing two strings)

In C#, to compare strings, we have following method:

1. Use CompareTo: 
stringValue.CompareTo(string1)
CompareTo method was designed primarily for use in sorting or alphabetizing operations. It uses CultureInfo.CurrentCulture.CompareInfo.Compare, which means it will use a culture-dependant comparison.

2. Use .Equals()
stringValue.Equals(string2)
if string is empty, then the exception will be thrown. So we’ll need to handle null values before using Equals().

3. Use “==”
stringValue == otherStringValue
The == operator calls the static Equals(string a, string b) method (which in turn goes to an internal EqualsHelper to do the comparison. As we mentioned earlier, calling .Equals() on a null string gets null reference exception, while on == does not.
