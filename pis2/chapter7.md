# Charpter 7 Built-in Control Strutures

Scala has very few control structures:```if, while, for, try, match```, The reason Scala has so few is that it has included function literals since its inception. Instead of accumulating one higher-level control structure after another in the base syntax, Scala accumulates them in libraries.

Almost all control structures result in some value, This is the approach taken by functional languages, in which programs are viewed as <mark>computing a value</mark>, thus the components of a program should also compute values

## if expressions

if returns value, A advantage to using a val instead of a var is that it better sup- ports <mark>*equational reasoning*</mark>

```scala
val filename =  if (!args.isEmpty) args(0)  else "default.txt"
```

## while loops

while is just the same as java, also because it depends vars to change loops status and is imperative style, it's usage is discouraged.

while and do-while are called 'loops', not expressions, because they result type is Unit. it is called unit type and the value is (). The existence of () is how Scala’s Unit differs from Java’s void.   
<mark>Reassignment of a var returns Unit value.</mark>

```scala
var a = 1
(a = 2) == () // True
```

## for expressions

##### iterate through collections

```scala
for (i <- 1 to 4)   println("Iteration "+ i)
```

##### filtering

```scala
for (
  i <- 1 until 9 
  if i % 2 == 0
  if i != 3 // can have multiple filters
) yield i
```

##### nested iteration

```scala
def fileLines(file: java.io.File) =  scala.io.Source.fromFile(file).getLines().toList 
def grep(pattern: String) =   for (     file <- filesHere
     // compiler wont infer semicolons inside parantheses     if file.getName.endsWith(".scala"); // semicolon is needed     line <- fileLines(file)     if line.trim.matches(pattern)   ) println(file +": "+ line.trim)grep(".*gcd.*")
```

##### mid-stream variable bindings

we can defines vals in for expressions, but the val keywords is left off.

```scala
def grep(pattern: String) =    for {      file <- filesHere      if file.getName.endsWith(".scala")      line <- fileLines(file)      trimmed = line.trim // bind new val      if trimmed.matches(pattern)    } println(file +": "+ trimmed)
```

##### produce new collections

using ```yield``` keyword to archieve this. if there is a block of for expression, put ```yield``` before the first curly brace.


```scala
def scalaFiles =    for {      file <- filesHere      if file.getName.endsWith(".scala")    } yield file
```

## Exception handing with try expressions

**throw excpetion** is the same as java. throw expression returns a value with type of Nothing.

##### catch exception

```scala
try {    val f = new FileReader("input.txt")    // Use and close file  } catch {    case ex: FileNotFoundException => // Handle missing file    case ex: IOException => // Handle other I/O error}
```

## Match expressions

```scala
val firstArg = if (args.length > 0) args(0) else ""        firstArg match {          case "salt" => println("pepper")          case "chips" => println("salsa")          case "eggs" => println("bacon")          case _ => println("huh?")}
```

## scala has no break and continue.

## variable scope

curly brace define a new  scope. inner scope can have same variable name.  
Repl can define same val. The reason you can do this is that, conceptually, the interpreter creates a new nested scope for each new statement you type in