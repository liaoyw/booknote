# Traits

Two of the most common ways traits are useful: widening thin interfaces to rich ones, and defining stackable modifications.

## How traits work

Once a trait is defined, it can be *mixed in* to a class using either **extend** or **with** keywords.  
If you want to mix in multiple traits, you add more with clauses.

A trait is also defines a type. Seems you can not define a class only using *with* without *extends*

```scala
trait T
class A with T; // error: ';' expected but 'with' found.
class B extends T // this is ok
```

In fact, you can do anything in a trait definition that you can do in a class definition, and the syntax looks exactly the same, with only two exceptions.  

* No "class" parameters
* super is dynamic bound

## Thin verses rich interfaces

A rich interface has many methods, which are convenient for the caller. A thin interface, on the other hand, has fewer methods, and thus is easier on the implementers. Clients calling into a thin interface, however, have to wirte more code.

## Traits as stackable modifications

The order of mixins is significant. **traits further to the right take effect first.**