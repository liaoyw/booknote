## Chapater 8: Functions and Closures

### Methods is same as java methods

### Local functions

To avoid namespace polution, it's usefull to put helper functions inside a function, although we can alse use private method like java.  
Local funtions can access the parameters of their enclosing function.

### First-class function(function literals)

We can express functions in function literal syntax, i.e., ```(x: Int) => x + 1```, and that functions can be represented by objects, which are called func- tion values.  
Function literal: exists in source code, and in runtime, it will be used to create function value. <mark>Function values are objects</mark>  

Function literals with more than one statement can be put inside curly braces(*code block*), and the result is the result of the last expression.

Functions which accept other functions as parameters and/or use functions as return values are known as **higher-order** functions.

```scala
increase = (x: Int) => {                 println("We")                 println("are")
                 println("here!") 
                 x+1}
val someNumbers = List(-11, -10, -5, 0, 5, 10)
// high-order functions
someNumbers.foreach((x: Int) => println(x))
someNumbers.filter((x: Int) => x > 0)
```

### Short forms of function literals

**target typing**(caller knows the type of argument) allow us to leave off parameter type  
Alse we can leave off the paratheses of function with only *one* argument with type inferred.

**place  holder** we can use underscores as placeholders for one or more parameters, as long as each parameter appears only one time within function literals.   
If the compiler have no enough information to infer missing parameter type, we need to specify the types using colon:```val f = (_: Int) + (_: Int)```, multiple underscores means multiple arguments, that's why each parameter can only appears once.

```scala
someNumbers.filter((x: Int) => x > 0)
// target typing
someNumbers.filter((x) => x > 0) 
// target typing with only one argument
someNumbers.filter(x => x > 0)

// placeholder
someNumbers.filter(_ > 0)

// bad, no type information to be inferred
//val f = _ + + 
val f = (_:Int) + (_:Int)
// f: (Int, Int) => Int = <function2>
f(1, 2)
```

### Partial applied function

function using underscore to replace one or more aruments and returns a function value. the returned function is **Partial applied**  
A partially applied function is an expression in which you don’t supply all of the arguments needed by the function. Instead, you supply some, or none, of the needed arguments. function.  
```val p = println _```  
In scala, invoking a function is called applying a function to the arguments

When used as argument, when partial applied functions leaved off all the parameters can leave off the underscore  

```scala
someNumbers.foreach(println _)
someNumbers.foreach(println)
```

### Closures

closure is a function that captures free variable(s), and in scala, closure captures the variable reference, not the value, so closure can see the change of variable and if closure changes the variable is's a availabe out side the function scope.

### Special funtion forms

#### Repeated paramters

```scala
// args is an Array
def echo(args: String*) =
  args.foreach(println)
echo("one")
echo("one", "two")

// but you can not put an array as argument, to do so, we have to
echo(Array("one", "two"): _*)
```

#### Named paramter and default paramter

Just like python, we can use parameter name to pass argument, so that we can pass the argment in any order, if we set value in function define, then it's default parameter

```scala
def speed(distance: Float, time: Float = System.currentTimeMillis): Float =                 distance / time
```

### Tail recursion

Functions call themselves as theire last action is called tail recursion. The Scala compiler can optmize this by detecting tail recursion and replaces it with a jump back to the beginning of the function, after updating the function parameters with the new values.