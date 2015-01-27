# Composition and inheritance

## Abstract class

A class with abstract members must iterself be declared abstract.
A method is abstract if it does not have an implemen- tation (i.e., no equals sign or body), and need no abstract modifier.

```scala
abstract class Element {
  def contents: Array[String] // abstract method
}
```

## Define parameterless methods

*parameterless method* ```def xx = 5 ```  
*empty-paren method* ```def xx() = 5```  
The recommended convention is to use a parameterless method whenever there are no parameters and the method accesses mutable state only by reading fields of the containing object (in particular, it does not change mutable state). This convention supports the uniform access principle,1 which says that client code should not be affected by a decision to implement an attribute as a field or method. And add paratheses when the method has side effects.
In principle it’s possible to leave out all empty parentheses in Scala function calls

```scala
def test() = 5
test() // ok
test //ok
def test = 5
test //ok
test() // error
```

## Overriding methods and fields

In scala, fields and methods belong to the same namespace. This makes it possible for a field to overridee a parameterless method.  
On the other hand, in scala it's forbidden to define a field with same name in the same class.

```
Generally, Scala has just two namespaces for definitions in place of Java’s four. Java’s four namespaces are fields, methods, types, and packages. By contrast, Scala’s two namespaces are:• values (fields, methods, packages, and singleton objects)• types (class and trait names)The reason Scala places fields and methods into the same namespace is pre- cisely so you can override a parameterless method with a val, something you can’t do with Java.
```

## Defining parametric fields

<mark>parametric field</mark> is a parameter defined as class parameter. It's a shorthand that defines at the same time a parameter and field with the same name.

```scala
// x is a parametric field
// and could be var
class Test(val x)
// is equal to
class Test(val a) {
    val x = a
}
```

Finally, it is possible to add modifiers such as private, protected,5 or override to these parametric fields, just as you can do for any other class member.

## Invoking supclass constructor

If the superclass have parametered constructor, subclass have to extend it with proper argument

```scala
class LineElement(s: String) extends ArrayElement(Array(s)) {  override def width = s.length  override def height = 1}
```

## Using oerriding modifiers

Scala requires such a modifier for all members that override a concrete member in a parent class.  
The modifier is optional if a member implements an abstract member with the same name.  
The modifier is forbidden if a member does not override or implement some other member in a base class

## Polymorphism and dynamic binding

Same as java.

## declaring final memebers

final class and final methods