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