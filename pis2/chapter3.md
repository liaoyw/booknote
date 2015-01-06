# Chapter 3 

##Next step in Scala

### Parameterize Arrays with types

you parameter an instance with types by specifying one or more types in square brackets. When you parameterize a parameter with both a type and a value, the type comes first in its square brackets, followed by the value in parantheses.

```scala
val greetingString: Array[String] = new Array[String](3)
```

Scala has no notation as operator overloading, but all **operators** are just normal methods

```scala
1 + 2 // just like
1.+(2)
```
Scala has fewer special cases than Java. Arrays are simply instances of classes like any other class in Scala. When you apply parentheses surrounding one or more values to a variable, Scala will transform the code into an invocation of a method named apply on that variable. So greetStrings(i) gets transformed into <mark>greetStrings.apply(i)<mark>. 

```scala
val greeting = Array(1, 2, 3) 
val greeting2: Array[String] = new Array[String](3)
greeting(0) = 0 // is same as
greeting.update(0, 0)
```

### Use List

As Array, Scala.List can only hold the same type of elemetns, but not like array, list is immutable.

```scala
val list1 = List(1, 2)
val list2 = List(3, 4)
val concated = list1 ::: list2 // List(1, 2, 3, 4)

//  cons(::) is right hand operand
// If the method name ends in a colon, the method is invoked on the right operand. 
// Therefore, in 1 :: list2, the :: method is invoked on twoThree,
val consResult = 1::list2 // List(1, 3, 4)

// Nil is List()
println(List(1,2,3) == 1::2::3::Nil) // true
```

### Use tuples

Like lists, tuples are immutable, but unlike lists, tuples can contain different types of elements. You can use tuple to return multiple objects from a method

```scala
val pair = (42, 'vgs')
// tuple序号从1开始，Haskell和ML传统
print pair._1
// 之所以不用pair(2)是因为apply总是会返回一样类型的数据
// 而tuple元素类型不同
print pair._2 
```

Tuple的类型由它的元素决定，(1, 2)类型为Tuple2[Int, Int], ('i', "am", 28, "years old now")为Tuple4[Char, String, Int, String). 现在scala库支持的tuple元素个数为22

### Use sets and maps

set和map分可变和不可边的，类名相同，包名不同

```scala
val aSet = Set(1, 2)
// "name" -> "yf" is same as tuple ("name", "yf")
val aMap = Map("name" -> "yf", "hobby" -> "no")
val map2 = Map(("name", "yf"), ("hobby", "no"))
```

### Learn to recognize the functional style

尽量少用var， 用pure fuction, 方法不带side effection


### 读文件例子

```scala
import scala.io.Source
def widthOfLength(s: String) = s.length.toString.length  
if (args.length > 0) {  val lines = Source.fromFile(args(0)).getLines().toList  val longestLine = lines.reduceLeft(    (a, b) => if (a.length > b.length) a else b  )  val maxWidth = widthOfLength(longestLine)  for (line <- lines) {    val numSpaces = maxWidth - widthOfLength(line)    val padding = " " * numSpaces    println(padding + line.length +" | "+ line)  } 
}else  Console.err.println("Please enter filename")
```
