## Recursion schemes using @tsplus/stdlib
Some simple examples for using the recursion scheme library.

### Why?
#### Recursive functions are hard
Writing functions over recursive data structures requires mixing the data manipulation with the recursive structure.
Consider the humble `List<A>`.
```
type List<A> = Cons<A> | Nil
type Nil = null
type Cons<A> = {head: A, tail: List<A>}
const cons = <A>(head: A, tail: List<A>) => ({head, tail})
```

And the `list` operation.  Operations like `list` must deal with both their computation *and* the recursion. 
```
const length = (list:List<A>) => list == null ? 0 : 1 + length(list.tail)
```


###  `Recursive` data
The Recursion Scheme Gods do, unfortunately, exact a high price: Your existing recursive data structure will need to be modified with an extra type parameter:
```
type ListR<A, R> = ConsR<A, R> | null
type ConsR<A, R> = {head: A, tail: R}

```
The `prelude/Recursive` module from @tsplus/stdlib requires a 




### What is @tsplus/stdlib?
[@tsplus](https://github.com/ts-plus) is a compiler for Typescript.  Its standard library [@tsplus/stdlib](https://github.com/ts-plus/stdlib) is a generalized
functional programming library.  For this post, we're mostly concerned with 
