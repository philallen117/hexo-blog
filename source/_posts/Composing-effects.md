---
title: Composing effects
---

## Why bother

In functional programming, the term *effect* is used for anything that is not (just) the computation of values from other values. That includes: IO, state, errors, and speciuak cases such as logging, reading configuration and so on. Standard texts on pure functional languages explain how to use particular monads to manage effects, such as Either (which you can use for managing errors) and Reader (which you can use for reading configuration).

(A type that satisfies the monad laws supports sequential composition of computation while threading through contextual data.)

This all works very well while your program is a pure core with what amounts to a monolithic imperative *main* around the outside. This approach is not likely to be sustainable for large code bases, with various modules managing different effects, possibly via third party libraries.

The issues start when you try to compose effects.

- Can I predict and control the run-time overhead of the composition itself? (How much extra indirection and pointer-chasing is left at run-time.)
- Have I introduced order dependencies between effects that are not logically necessary?
- Does my use of fine-grained components in code spill over to inefficient use of resources such as threads or stack frames at run-time?
- If I am working on a domain-specific language, can I
