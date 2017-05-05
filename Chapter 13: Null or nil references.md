# Chapter 13: Null/nil references

## Python

### Which does the language use?

Null.

### Does the language have features for handling null/nil references?

The `Null` object is returned by functions that don’t explicitly return a value. It supports no special operations. There is exactly one `null` object, named `None` (a built-in name). `type(None)()` produces the same singleton. It is written as `None`.


## C`#`

### Which does the language use?

In C#, null is used for empty references.

### Does the language have features for handling null/nil references?

Throwing an exception is expensive, so if an object can return null, check the object's value before trying to access it. 

```csharp
if (object1 == null) 
{
  //do something here 
}
```

