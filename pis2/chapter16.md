# Work with Lists

## List literals

```List('a', 'b', 'c')```

## List type

Like arrays, lists are **homogeneous**, elements must have the same type. list of T is written as ```List[T]```.

List type is covariant. <mark>This means that for each pair of types S and T, if S is a subtype of T, then List[S] is a subtype of List[T].</mark> ```List[CharSequence] = List("a", "b", "c")```, empty list ```List()``` has type ```List[Nothing]``` 

## Constructing Lists

All lists are built from ```Nil``` and ```::```, ```List(1, 2, 3) eq 1::2::3::Nil```

## Basic operations on Lists

```head, tail, isEmpty```, head and tail is only defined for non-empty lists, if list is empty, they will throw exceptions

## List patterns

```scala
val List(a, b, c) = List("apple", "orange", "pear")
val a::b::c::Nil = List("apple", "orange", "pear")
```

Insert sort

```scala
def isort(xs: List[Int]) = xs match {
    case List() => xs
    case x :: xs1 => insert(x, isort(xs1))
}

def insert(x: Int, xs: List[Int]) = xs match {
    case List() => List(x)
    case y :: ys => if (x < y) x :: xs 
                    else y :: insert(x, ys)
}
```

## First-order methods on class List

*first-order* methods don't take function as parameter

*high-order* methods do take functions as parameter

```scala
List(1, 2) ::: List(3, 4) == List(1, 2, 3, 4) // list concatenation
List(1, 2, 3).length == 3 // but it's O(n)
val abcde == List('a', 'b', 'c', 'd', 'e')
// time costing
abcde.init = List('a', 'b', 'c', 'd')
abcde.last = 'e'

abcde.reverse == List(e, d, c, b, a)
```

Prefixes and suffixes: ```drop, take, and splitAt```

Element selection: ```apply and indices```

Flattening a list of lists: ```flatten```

Zipping lists: ```zip and unzip```
Displaying lists: ```toString and mkString```

Converting lists: ```iterator, toArray, copyToArray```

## High-order methods on list

Mapping over lists: map, flatMap and foreach

Filtering lists: filter, partition, find, takeWhile, dropWhile, and span

Predicates over lists: forall and exists

Folding lists: /: and :``` def sum(xs: List[Int]): Int = (0 /: xs) (_ + _)```

Sorting lists: sortWith

...