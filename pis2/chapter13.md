# Packages and Imports

This chapter shows several constructs that help you program in a modular style. It shows how to place things in packages, make names visible through imports, and control the visibility of definitions through access modifiers.

## Putting code in packages

You can place code into named packages

- like java, placing the contents of an entire file into a package

```scala
package bobsrockets.navigationclass Navigator
```
- like c# namespaces, you follow a package clause by a section in curly braces that contains the definitions that go into the package. This syntax is called a packaging. 

```scala
package bobsrockets.navigation {          class Navigator}
```

However, one use of the more general notation is to have different parts of a file in different packages. For example, you might include a class’s tests in the same file as the original code

```scala
package bobsrockets {          package navigation {            // In package bobsrockets.navigation            class Navigator            package tests {              // In package bobsrockets.navigation.tests              class NavigatorSuite            }} }
```

## Concise access to related code

* First, as you would expect, a class can be accessed from within its own package without needing a prefix.
* a package itself can be accessed from its containing package without needing a prefix.

## Imports

```scala
// import Fruit
import bobsdelights.Fruit

// import all member of  package bobsdelights
// like import bobsdelight.* in java
import bobsdelights._ 

// import all members of class Fruit
// like java's static import
import bobsdelights.Fruit._
```

Import can appear every where, and can import member of object, like python's import

```scala
def shwoFruit(fruit: Fruit) {
  import fruit._
  // name and color imported
  println(name + "s are " + color)
}
```

Another way Scala’s imports are flexible is that they can import packages themselves, not just their non-package members. 

```scala
import java.util
println(new util.Date())
```

Imports in Scala can also rename or hide members. This is done with an import selector clause enclosed in braces.

```scala
import Fruits.{Apple, Orange}
import Fruits.{Apple => McIntosh, Orange}
//  hiding Pear
import Fruits.{Pear => _, _}
```

## Implicit imports

```scala
import java.lang._ // everything in the java.langpackageimport scala._     // everything in the scala packageimport Predef._    // everything in the Predef object
```
The three import clauses above are treated a bit specially in that later imports overshadow earlier ones. 

## Access modifiers

Members of packages, classes, or objects can be labeled with the access modifiers private and protected. These modifiers restrict accesses to the members to certain regions of code.

### private members
A member labeled private is visible only inside the class or object that contains the member definition. Not like java which permit both accesses because it lets an outer class access private members of its inner classes.

```scala
class Outer {  class Inner {    private def f() { println("f") }    class InnerMost {      f() // OK 
    }  }  (new Inner).f() // error: f is not accessible
}
```

### proteced members

In Scala, a protected member is only accessible from subclasses of the class in which the member is defined. In Java such accesses are also possible from other classes in the same package.

```scala
package p {	       class Super {            protected def f() { println("f") }          }          class Sub extends Super {            f()          }          class Other {            (new Super).f()  // error: f is not accessible          }}
```

### public members 

Same as java

### public is the **default**

### Scope of protection (a little complicated.. Section 13.5)

no access modifier  private[bobsrockets]  private[navigation]  private[Navigator]  private[LegOfJourney]  private[this]  public access  access within outer package same as package visibility in Java same as private in Java  same as private in Scala  access only from same object

### Visibility and companion objects

they have some access ability

## Package objects

```package object packageName``` in package.scala, and can be imported to any package

