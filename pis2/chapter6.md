# Chapter 6: Functional(Immutable) objects

Topics contains oo in scala: class parameters and constructors, methods and op- erators, private members, overriding, checking preconditions, overloading, and self references.

## Constructing object

you can put parameter list in class define, if it has no body, then the culy braces ```class Rational(n:Int, d:Int)```, they are called class parameter. The scala compiler will use class parameters to create a <mark>primary constructor</mark>.  
Scala will put any code which is not part of a field or a method definition into the primary constructor.

```scala
class Rational(n:Int, d:Int) {
  println(s"Created ${n}/${d}")
}
```

### override toString

```scala
class Rational(n:Int, d:Int) {
  // check preconditions
  require(d != 0)
  // override is needed
  override def toString() = s"Rational: $n/$d"
}
```

### adding fileds

we can not use class parameters of another object with same class. but we can add new field, then use it from anywhere. such as:

```scala
 // but if we add val/var before class parameters, then it's ok
 class Rational(n: Int, d: Int) {    require(d != 0)    val numer: Int = n    val denom: Int = d    override def toString = numer +"/"+ denom    def add(that: Rational): Rational =      new Rational(        numer * that.denom + that.numer * denom,        denom * that.denom) }
```

#### private field and methods are like java, add *private* modifier in front of the definition.

#### self reference using this is the same as java


## Auxiliary constructors

Auxiliary constructors in Scala start with ```def this(...)```, In Scala, every auxiliary constructor must invoke another constructor of the same class as its first action. and unlike java, you can only call primary constructor or other auxiliary constructor, Not super class's constructor.

## define operators

Becaurse operators like +, -, *, /  are just normal methods, we can define it if we want. ```def +(n: Int) = ...```  

## Scala Indentifiers

+ alphanumeric identifier: ```test()```, constant starts with the first character uppercase and others camelCase
+ operator identifier: ```_, +```
+ mixed identifier: ```unary_-```
+ literal identifier ```Thread.`yield`()```

## Method overloding

Nothing special, same as java

## Implicit conversions

```scala
implicit def intToRational(x: Int) = new Rational(x)
```
with this implicit conversion in scope, we can use Int as Rational
