# Recursion schemes using @tsplus/stdlib
Writing functions over recursive data structures requires mixing the data manipulation with the recursive structure.
Consider the humble `List<E>`.
```
type List<E> = Cons<E> | Nil
type Nil = null
type Cons<E> = {head: E, tail: List<E>}
const cons = <E>(head: E, tail: List<E>) => ({head, tail})
```

Operations like `list` must deal with both their computation *and* the recursion.
```
const length = (list:List<A>) => list == null ? 0 : 1 + length(list.tail)
```

##  Non-Recursive `Recursive` data
Instead of writing recursive functions on recursive data, we'd prefer non-recursive functions on a related, non-recursive data type.

Let's define a new type called `ListR` and replace its `tail` property with a generic parameter, `A` and its `head` with a generic `E`
```
  type ListR<E, A> = ConsR<E, A> | NillR
  type NillR = null
  export type ConsR<E, A> = { head: E; tail: A }
  const make = <E, A>(head: E, tail: A) => ({head, tail})
  export const empty = () => null

```
Note how our `ListR` can contain *different* types for its `tail` and `head`
```
const oneString = make(1, "string")
const stringOne = make("string", 1)
```
This is definitely weird -- but if we think of the value in `tail` as the accumulation of 
#### The `Recursive` type
```

```

The `prelude/Recursive` module from @tsplus/stdlib requires a 




### What is @tsplus/stdlib?
[@tsplus](https://github.com/ts-plus) is a compiler for Typescript.  Its standard library [@tsplus/stdlib](https://github.com/ts-plus/stdlib) is a generalized
functional programming library.  For this post, we're mostly concerned with 
