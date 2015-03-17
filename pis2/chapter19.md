# Type Parameteriaztion

## Information hiding

private constructor, place ```private``` before class parameters, then we can only call primary constructor from other auxiliary constructor or companion object.

```scala
class Queue[T] private (          private val leading: List[T],          private val trailing: List[T])

def this(elems: T*) = this(elems.toList, Nil)

object Queue {    // constructs a queue with initial elements ‘xs’    def apply[T](xs: T*) = new Queue[T](xs.toList, Nil)}
```

### private class

Another, more radical way is to hide the class itself and only export a trait that reveals the public interface of the class

## Variance(变化） annotation

if S is a subtype of type T, then should Queue[S] be considered a subtype of Queue[T]?

+ *covariant*(flexible): [+T] Yes 
+ *nonvariant*(rigid): [T] No 
+ *contravariant*: [-T] !!Strage, Queue[T] is subtype of Queue[S]

*variance annotations.*, +/- before type parameter

### todo, how to verify variance?

## Low bound

```scala
class Queue[+T] (private val leading: List[T],      private val trailing: List[T] ) {    def enqueue[U >: T](x: U) =      new Queue[U](leading, x :: trailing) // ...}
```

The new definition gives enqueue a type parameter U, and with the syntax, “U >: T”, defines T as the lower bound for U. As a result, U is required to be a supertype of T.

## Contravariance ?

## Upper bounds [ S <: T]

“T <: Ordered[T]” syntax, you indicate that the type parameter, T, has an upper bound, Ordered[T]. This means that the element type of the list passed to orderedMergeSort must be a subtype of Ordered.
