## Charpter 5: Basic types and operations

### basic types

There are java wrappers: Int, Char, Boolean... They have the exact same range as the corresponding types in Java, so scala compiler can transform the instance of <mark>value types</mark> to java native bytecodes.

### Literal

Almost the same as java. Unicode characters can appear any where in scala program. such as indentifiers:

``` bash
 scala> val B\u0041\u0044 = 1
 BAD: Int = 1
```
 
 Raw strings using (""")
 
 ```scala
 // the leading spaces before the second line are included in the string
 println("""Welcome to Ultamix 3000.                   Type "HELP" for help.""")
 // better print  
 println("""|Welcome to Ultamix 3000.            |Type "HELP" for help.""".stripMargin)
 ```
 
 Symbols
 
 ```bash
 # symbol is interned, but is rarely seen
 # String is good enough
 scala> val s = 'aSymbol  s: Symbol = 'aSymbol
 # name is the only method of symbol scala> s.name res20: String = aSymbol
 ```
 
### Operators are methods

```scala
1 + 2
// is just infix operator notation of
(1).+(2)
```

You can use any method in operator notation, there are also prefix and postfix operators.  
The only identifiers that can be used as prefix operators are +, -, !, and ~. They are treated as unary_-, unary_+  
Postfix operators are methods that take no arguments, when invoked without a dot or parentheses. In scala, <mark>you can leave empty paratheses on method calls</mark>.   
Convention is that you include parenthese if the method has side effects, such as println, and leave them off if no side effects.


```scala
"abc" indexOf 'a'
// call a method that takes multiple arguments using operator notation,
// you have to place those arguments in parentheses.
"abc" indexOf ('a', 3)

```

### Object equality

Unlike java, == and != is used as call equals method to compare contents, and scala will check if the left hand operator is null or not. and use <mark>eq, ne</mark> to check reference equality