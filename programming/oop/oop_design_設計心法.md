# Good articles

## [物件導向程式的九個體操練習](http://ihower.tw/blog/archives/1960) by ihower

## [Tell, don't ask](https://pragprog.com/articles/tell-dont-ask)

> That is, you should endeavor to tell objects what you want them to do; do not ask them questions about their state, make a decision, and then tell them what to do.

-

> It is easier to stay out of this trap if you start by designing classes based on their responsibilities, you can then progress naturally to specifying commands that the class may execute, as opposed to queries that inform you as to the state of the object.

### Just the data
> The biggest danger here is that by asking for data from an object, you are only getting data. You're not getting an object—not in the large sense. Even if the thing you received from a query is an object structurally (e.g., a String) it is no longer an object semantically. It no longer has any association with its owner object. Just because you got a string whose contents was 「RED」, you can't ask the string what that means. Is it the owners last name? The color of the car? The current condition of the tachometer? An object knows these things, data does not.

### Law of Demeter
> What that means is that the more objects you talk to, the more you run the risk of getting broken when one of them changes.

-

> according to the Law of Demeter for Methods, any method of an object should only call methods belonging to:

- itself.
- any parameters that were passed in to the method.
- any objects it created.
- any composite objects.

#### Example
Bad example:
```java
SortedList thingy = someObject.getEmployeeList();
thingy.addElementWithKey(foo.getKey(), foo);
```
Instead, this should be:
```java
someObject.addToThingy(foo);
```
