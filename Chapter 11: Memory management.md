# Chapter 11: Memory management

## Python

### How is it handled?

Memory management in Python involves a private heap containing all Python objects and data structures. The management of this private heap is ensured internally by the ***Python memory manager***. The Python memory manager has different components which deal with various dynamic storage management aspects, like sharing, segmentation, preallocation or caching.

### How does it work?

At the lowest level, a raw memory allocator ensures that there is enough room in the private heap for storing all Python-related data by interacting with the memory manager of the operating system. On top of the raw memory allocator, several object-specific allocators operate on the same heap and implement distinct memory management policies adapted to the peculiarities of every object type. For example, integer objects are managed differently within the heap than strings, tuples or dictionaries because integers imply different storage requirements and speed/space tradeoffs. The Python memory manager thus delegates some of the work to the object-specific allocators, but ensures that the latter operate within the bounds of the private heap.

### Garbage collection

Python uses two strategies for memory allocation **reference counting** and **garbage collection**. Python schedules garbage collection based upon a threshold of object allocations and object deallocations. When the number of allocations minus the number of deallocations are greater than the threshold number, the garbage collector is run. One can inspect the threshold for new objects (objects in Python known as generation 0 objects) by loading the gc module and asking for garbage collection thresholds:

```python
import gc
print "Garbage collection thresholds: %r" % gc.get_threshold()
```

### Automatic reference counting

Prior to Python version 2.0, the Python interpreter only used reference counting for memory management. Reference counting works by counting the number of times an object is referenced by other objects in the system. When references to an object are removed, the reference count for an object is decremented. When the reference count becomes zero the object is deallocated.

### More information

[*This website*](https://www.digi.com/wiki/developer/index.php/Python_Garbage_Collection) shows the details on garbage collection in Python programming

## C`#`

lolololol
