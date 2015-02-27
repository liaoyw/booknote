#Case classes and Pattern Matching

## excample of Simple expression

In scala, you can leave out the braces around an empty class if you wish, so ```class C {} ``` is the same as ```class C```

### Case classes

classes with **case** modifier are called case class, Using the modifier makes the Scala compiler add some syntactic conveniences to your class.

- Add factory method with the name of the class, no **new** needed for create a new instance```val v = Var("x")```
- All arguments implicitly get a ```val``` prefix
- Compiler adds "natural" implimentations of methods```toString, hashcode, equals``` 
- Add copy method to class

The case class will become a little bit larger, because of additional methods and implicit fields added

### Patterm matching

```scala
selector match { alternatives } 
// instead of java switch
switch (selector) { alternatives }
```

A *variable* or *wildcard(_)* pattern matches every value. Pattern matching is diffent with java switch in 3 aspect:

1. pattern matching is an expression(return a value)
2. new "fall through" int next case
3. if no pattern match, ```MatchError``` will be thrown

## Kinds of patterns

### wildcard patterns

The wildcard pattern (_) matches any object, and ignore then

### Constant patterns

matches only itself. eg: Nil, a singleton object, is a pattern that matches only the empty list.

### variable patterns

matches any object like ```_```, but bind the value to the variable.  

**Variable or constant?**  
a simple name starting with a lowercase letter is taken to be a pattern variable; all other references are taken to be constants.  
If you need to, you can still use a lowercase name for a pattern constant, using one of two tricks. 

```scala
val pi = 3.1415926
E match {    case `pi` => "strange math? Pi = "+ pi    case _ => "OK"}
```

### Construct patterns

check that the constructor parameters 

### Sequence patterns

you can specify any number of elements within the pattern

```scala
expr match {          case List(0, _, _) => println("found it")          case _ =>}
```

If you want to match against a sequence without specifying how long it can be, you can specify _* as the last element of the pattern.

```scala
expr match {          case List(0, _*) => println("found it")          case _ =>}
val l = List(1, 2, 3)
val l0 = l match { case List(1, x, _*) => x }
//l0: Int = 2
```

### Tuple patterns

like sequence pattern, unpack tuple elements to variables

```scala
def tupleDemo(expr: Any) =      expr match {        case (a, b, c)  =>  println("matched "+ a + b + c)        case _ => 
      }
```

### Typed patterns
You can use a typed pattern as a convenient replacement for type tests and type casts.

```scala
  def generalSize(x: Any) = x match {    case s: String => s.length    case m: Map[_, _] => m.size    case _ => -1}

// otherwise, we have to check
expr.isInstanceOf[String]
// and cast
expr.asInstanceOf[String]
```

*Type erasure*

Just like java generics, scala will remove type info of collection(**excluding array**), here is no way to determine at runtime whether a given Collection object has been created with two Int arguments

The only exception to the erasure rule is arrays, because they are handled specially in Java as well as in Scala. 

```scala
def isIntIntMap(x: Any) = x match {           case m: Map[Int, Int] => true           case _ => false}
isIntIntMap(Map(1 -> 1)) // true ok
isIntIntMap(Map("abc" -> "abc")) // true, type erasure
```

### Varible binding
In addition to the standalone variable patterns, you can also add a variable to any other pattern. You simply write the variable name, an at sign (@), and then the pattern. 

```scala
expr match {  case UnOp("abs", e @ UnOp("abs", _)) => e // e has to match UnOp("abs", _)  case _ =>}
```

## Pattern guards

Scala restricts patterns to be linear: a pattern variable may only appear once in a pattern

A pattern guard comes after a pattern and starts with an if. The guard can be an arbitrary boolean expression, which typically refers to variables in the pattern. If a pattern guard is present, the match succeeds only if the guard evaluates to true. 

```scala
def simplifyAdd(e: Expr) = e match {                 case BinOp("+", x, y) if x == y =>                   BinOp("*", x, Number(2))                 case _ => e}
```

## Pattern overlaps

Patterns are tried in the order in which they are written. This is very important to write case class

## The Option type

Option has two forms ```Some(x) None```, we can get value use pattern matching.

```scala
val v = x match { 
  case Some(s) => s
  case None => "?"
```

## Patterns everywhere

### patterns in variable definitions

```scala
val myTuple = (123, "abc")
val (number, String) = myTuple

val exp = new BinOp("*", Number(5), Number(1))
val BinOp(op, left, right) = exp
```

### Case sequences as partial functions

A sequence of cases (i.e., alternatives) in curly braces can be used anywhere a function literal can be used. Essentially, a case sequence is a function literal, only more general. Instead of having a single entry point and list of parameters, a case sequence has multiple entry points, each with their own list of parameters. Each case is an entry point to the function, and the parameters are specified with the pattern. The body of each entry point is the right-hand side of the case.

```scala
val withDefault: Option[Int] => Int = {          case Some(x) => x          case None => 0}
```

### Patterns in ```for``` expression

```for ((country, city) <- capitals)```