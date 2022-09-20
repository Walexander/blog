## Recursion schemes using @tsplus/stdlib
Some simple examples for using the recursion scheme library.

### Why?
#### Recursive functions are hard
Writing functions over recursive data structures requires mixing the data manipulation with the recursive structure.
Consider the humble `List<E>`.
```
type List<E> = Cons<E> | Nil
type Nil = null
type Cons<E> = {head: E, tail: List<E>}
const cons = <E>(head: E, tail: List<E>) => ({head, tail})
```

And the `list` operation.  Operations like `list` must deal with both their computation *and* the recursion. 
```
const length = (list:List<A>) => list == null ? 0 : 1 + length(list.tail)
```


###  Non-Recursive `Recursive` data
Instead of writing recursive functions on recursive data, we'd prefer non-recursive functions on a related, non-recursive data type.  First, we
replace add a new type parameter to our list.  We'll call this new type `ListR<E, A>`and use the `A` to store our recursive type.  Note how the `head` of our `ListR` is an `E` and the tail is a non-recursive `A`.

```
  type ListR<E, A> = ConsR<E, A> | NillR
  type NillR = null
  export type ConsR<E, A> = { head: E; tail: A }
  const make = <E, A>(head: E, tail: A) => ({head, tail})
  export const empty = () => null

```
#### ???
This dont look like no `List` I ever heard of.  Our new encoding of `List` fails to capture that `List`s contain another `List`
```
const oneString = make(1, "string")
const stringOne = make("string", 1)
```
Even worse, if we do use another `ListR` as the `tail` each level of recursion is *reflected* by the type signature.  `threeToOne` is of the type `ListR<number, ListR<number, ListR<number, NillR>>`!
```
const one: ListR<number, NillR> = make(1, null)
const twoOne: ListR<number, ListR<number, NillR>> = make(2, one)
const threeToOne = make(3, twoOne)
```
#### The `Recursive` type
We can use the @tsplus encoding of Higher-Kinded Types (HKT) and its `Recursive` data structure to solve the type puzzle.  Instead of making the `A` type anything, we can make our tail a `Recursive<ListR>` and gain some sanity.  First, let's define a new `cons`
```

```

The `prelude/Recursive` module from @tsplus/stdlib requires a 




### What is @tsplus/stdlib?
[@tsplus](https://github.com/ts-plus) is a compiler for Typescript.  Its standard library [@tsplus/stdlib](https://github.com/ts-plus/stdlib) is a generalized
functional programming library.  For this post, we're mostly concerned with 
