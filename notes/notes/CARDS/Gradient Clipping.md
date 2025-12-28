---
tags:
  - ML
link: https://paperswithcode.com/method/gradient-clipping
---


**Gradient Clipping** clips the size of the gradients to ensure optimisation performs more reasonably near sharp areas of the loss surface. Helps with the [[Exploding Gradient Problem]]


$$
\text { if }\|\mathbf{g}\|>v \text { then } \mathbf{g} \leftarrow \frac{\mathbf{g} v}{\|\mathbf{g}\|}
$$
[paperswithcode](https://paperswithcode.com/method/gradient-clipping)
[neptune.ai](https://neptune.ai/blog/understanding-gradient-clipping-and-how-it-can-fix-exploding-gradients-problem)
