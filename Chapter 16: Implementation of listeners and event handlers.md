# Chapter 16: Implementation of listeners and event handlers

## Python

The following answer comes from [this question](http://stackoverflow.com/questions/1092531/event-system-in-python):

The most basic style of event system is the 'bag of handler methods', which is a simple implementation of the [Observer pattern](https://en.wikipedia.org/wiki/Observer_pattern). Basically, the handler methods (callables) are stored in an array and are each called when the event 'fires'.
* [zope.event](https://pypi.python.org/pypi/zope.event) shows the bare bones of how this works (see [details](http://stackoverflow.com/questions/1092531/event-system-in-python/1092617#1092617)). Note: this example does not even support handler arguments.


* [LongPoke's 'callable list'](http://stackoverflow.com/questions/1092531/event-system-in-python/2022629#2022629) implementation shows that such an event system can be implemented very minimalistically by subclassing `list`.

```python
class Event(list):
    """Event subscription.

    A list of callable objects. Calling an instance of this will cause a
    call to each item in the list in ascending order by index.

    Example Usage:
    >>> def f(x):
    ...     print 'f(%s)' % x
    >>> def g(x):
    ...     print 'g(%s)' % x
    >>> e = Event()
    >>> e()
    >>> e.append(f)
    >>> e(123)
    f(123)
    >>> e.remove(f)
    >>> e()
    >>> e += (f, g)
    >>> e(10)
    f(10)
    g(10)
    >>> del e[0]
    >>> e(2)
    g(2)

    """
    def __call__(self, *args, **kwargs):
        for f in self:
            f(*args, **kwargs)

    def __repr__(self):
        return "Event(%s)" % list.__repr__(self)
```
* [spassig's EventHook (Michael Foord's Event Pattern)](http://stackoverflow.com/questions/1092531/event-system-in-python/1094423#1094423) is a straightforward implementation.

* [Josip's Valued Lessons Event class](http://stackoverflow.com/questions/1092531/event-system-in-python/1096614#1096614) is basically the same, but uses a `set` instead of a `list` to store the bag, and implements `__call__` which are both reasonable additions. The following shows the implementation:

```python
class Event:
    def __init__(self):
        self.handlers = set()

    def handle(self, handler):
        self.handlers.add(handler)
        return self

    def unhandle(self, handler):
        try:
            self.handlers.remove(handler)
        except:
            raise ValueError("Handler is not handling this event, so cannot unhandle it.")
        return self

    def fire(self, *args, **kargs):
        for handler in self.handlers:
            handler(*args, **kargs)

    def getHandlerCount(self):
        return len(self.handlers)

    __iadd__ = handle
    __isub__ = unhandle
    __call__ = fire
    __len__  = getHandlerCount

class MockFileWatcher:
    def __init__(self):
        self.fileChanged = Event()

    def watchFiles(self):
        source_path = "foo"
        self.fileChanged(source_path)

def log_file_change(source_path):
    print "%r changed." % (source_path,)

def log_file_change2(source_path):
    print "%r changed!" % (source_path,)

watcher              = MockFileWatcher()
watcher.fileChanged += log_file_change2
watcher.fileChanged += log_file_change
watcher.fileChanged -= log_file_change2
watcher.watchFiles()
```


* [PyNotify](http://home.gna.org/py-notify/) is similar in concept and also provides additional concepts of variables and conditions ('variable changed event').

* [axel](https://pypi.python.org/pypi/axel) is basically a bag-of-handlers with more features related to threading, error handling, ...

The disadvantage of these event systems is that you can only register the handlers on the actual Event object (or handlers list). So at registration time the event already needs to exist.

That's why the second style of event systems exists: the [publish-subscribe pattern](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern). Here, the handlers don't register on an event object (or handler list), but on a central dispatcher. Also the notifiers only talk to the dispatcher. What to listen for, or what to publish is determined by 'signal', which is nothing more than a name (string).

* [blinker](https://pythonhosted.org/blinker/) has some nifty features such as automatic disconnection and filtering based on sender.
* [PyPubSub](https://github.com/schollii/pypubsub) at first sight seems to be pretty straightforward; apparently does not yet support Python3.

* [PyDispatcher](http://pydispatcher.sourceforge.net/) seems to emphasize flexibility with regards to many-to-many publication etc.

* [louie](https://github.com/11craft/louie) is a reworked PyDispatcher "providing plugin infrastructure including Twisted and PyQt specific support".
* [django.dispatch](https://github.com/django/django/tree/master/django/dispatch) is a rewritten PyDispatcher "with a more limited interface, but higher performance".


* Qt's Signals and Slots are available from [PyQt](http://pyqt.sourceforge.net/Docs/PyQt4/new_style_signals_slots.html) or [PySide](https://wiki.qt.io/Signals_and_Slots_in_PySide). They work as callback when used in the same thread, or as events (using an event loop) between two different threads. Signals and Slots have the limitation that they only work in objects of classes that derive from `QObject`.

Note: `threading.Event` is not an 'event system' in the above sense. It's a thread synchronization system where one thread waits until another thread 'signals' the Event object.

## C`#`

The event model in the .NET Framework is based on having an event delegate that connects an event with its handler. To raise an event, two elements are needed:
A delegate that refers to a method that provides the response to the event.
Optionally, a class that holds the event data, if the event provides data.

```csharp
//This delegate can be used to point to methods
//which return void and take a string.
public delegate void MyEventHandler(string foo);

//This event can cause any method which conforms
//to MyEventHandler to be called.
public event MyEventHandler SomethingHappened;

//Here is some code I want to be executed
//when SomethingHappened fires.
void HandleSomethingHappened(string foo)
{
    //Do some stuff
}

//I am creating a delegate (pointer) to HandleSomethingHappened
//and adding it to SomethingHappened's list of "Event Handlers".
myObj.SomethingHappened += new MyEventHandler(HandleSomethingHappened);
```
