## Chapter 9 Control Abstraction

### Reduce code cuplication

These higher-order functions—functions that take functions as parameters—give you extra opportunities to condense and simplify code.

### Currying

Currying makes a list of parameters to many lists of a single parameter

Curried function is a function that takes one parameter an returns a function that takes one parameter and so on ,until there is a value.

```scala
def plainOldSum(x: Int, y: Int) = x + y

def curriedSum(x:Int)(y:Int) = x + y
```

### Writing new control structures

In any method invocation in Scala in which you’re passing in exactly one argument, you can opt to use curly braces to surround the argument, <mark> this is where curry shines!</mark>  
The purpose of this ability to substitute curly braces for parentheses for passing in one argument is to enable client programmers to write function literals between curly braces. 

```scala
println("Hello, world!")
println { "hello, world!" }
```

```scala
// loan pattern
// a control-abstraction function, such as withPrintWriter,
// opens a resource and “loans” it to a function
def withPrintWriter(file: File)(op: PrintWriter => Unit) {    val writer = new PrintWriter(file)    try {      op(writer)    } finally {      writer.close()    }}

val file = new File("date.txt")  withPrintWriter(file) {    writer => writer.println(new java.util.Date)}
```

### By name parameters

To make a by- name parameter, you give the parameter a type starting with => instead of () =>

```scala
 def byNameAssert(predicate: => Boolean) =   if (assertionsEnabled && !predicate)     throw new AssertionError
 // 5> 3 is evaluated at runtime
 byNameAssert(5 > 3) 
```