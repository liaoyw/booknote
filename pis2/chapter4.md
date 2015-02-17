##Charpter 4: Classes and objects

### classes , fields, methods

Same as java, except all the instance variables are public by default.

Parameters of a method are vals, so can not be changed. We need no <mark>return</mark> in the end of method, and if there is only one line expression within a method, just write it after equal sign

If method has no equal sign, then the result type is definitely Unit.

```scala
class ChecksumAccumulator {  private var sum = 0
  def add2(b:Byte):Unit = sum += b  def add(b: Byte) { sum += b }  def checksum(): Int = ~(sum & 0xFF) + 1}
```

### semicolon inference

Usually, we need no semicolon in the end of scala statement, except:

* two statement in one line
* use paranthese to group a expression in more than 1 line

### Singleton object (Companion object)

You must define both the class and its companion object in the same source file. It can't have parameters, because it should not be initialized.

Methods in companion object can be viewed as static method in java class.


### App traits

Any object with main method can be treated as program entry point. Also we can inherit  App traits and write some code in the object body

```scala
// Application trait is deprecated
object ShowArgs extends App {
  args.foreach(println _)
}
```

```bash
# -Dscala.time will print the execution time
$ scala -Dscala.time=True ShowArgs 1 2 3
a
b
c
[total 1ms]
```