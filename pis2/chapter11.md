# Scala's Hierachy

Every class inherits from a common superclass named <mark>Any</mark>, and there are common sumclasses **Null, Nothing**

## class hierachy

Any has two subclasses: **AnyVal** and **AnyRef**  
AnyVal: Byte, Short, Char, Int, Long, Float, Double, Boolean, and Unit. they are both abstract and final. **Unit** is roughly corresponds to java's void, and it has only instance **()**

Scala classes are different from Java classes in that they also inherit from a special marker trait called ScalaObject.

*eq* and *ne* compares using reference equality, and *==* and *!=* compares using *equals*

## Bottom types

**Null** is the type of null, and can not be assigned to value types.

**Nothing** is at the very bottom of Scala’s class hierarchy; it is a sub- type of every other type. However, there exist no values of this type whatso- ever. 