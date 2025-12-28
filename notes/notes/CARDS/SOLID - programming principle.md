---
tags:
  - on/programming
  - type/principle
publish: true
---
5 basic deign principles to make write a good OOP code.

The acronym **SOLID** stands for:
- **S**ingle responsibility principle: every class should have only one responsibility
- **O**pen-Closed principle: software netities should be open for extension, but closed for modification.
- **L**iskov substitution principle: Functions using poiters of reference to base classes must be able to use objects of derived classes without knowing it.
- **I**nterface segregation principle: clients should not be forced to depend upon interfaces that they do not use.
- **D**ependency inversion principle: depend upon abstractions, not concretes. Use interfaces between modules.

### Critique
- Single responsibility principle - it is faster and easier to write multipurpose things sometime.
- Locality of behavior - sometimes it is better to have locality of behavior over abstraction
- These principles are scale dependent - on smaller scale, things that do not follow the principles are perfectly reasonable.
- It is better to abstract when you discover/realize the abstraction - don't abstract before you need it, you **abstract when** you need it

> First you learn the instrument, then you learn the music, then you forget all that s**t and just play
### Links:
[wiki](https://en.wikipedia.org/wiki/SOLID), [video YT](https://youtu.be/q1qKv5TBaOA?si=PwDSk63DTmWdKZ-U), [rant YT](https://youtu.be/TT_RLWmIsbY?si=miSm3_MGWsJT1nNs)