---
tags:
  - on/algorithm
  - note/develop
---


* sets/groups consists of items
* each set/group has a representative
* groups are trees, disjoint-set is a forrest

x, y - objects that belong to some groups
- union(x, y): merges groups that x, y belongs to
	- $\mathcal{O}(n)$ (no tree height management)
- find(x): find the group x belongs to
- both union and find:
	- $\mathcal{O}(n)$ (no tree height management)
	- $\mathcal{O}(\alpha(n))$ with height management. $\alpha$ is [inverse Ackermann function](https://en.wikipedia.org/wiki/Ackermann_function#Inverse) which is basically $\mathcal{O}(log(n))$