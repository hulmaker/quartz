---
tags:
  - ML
link: https://neptune.ai/blog/vanishing-and-exploding-gradients-debugging-monitoring-fixing
---
Related to the [[Vanishing Gradient Problem]]

_Exploding gradients_ problem refers to a **large increase in the norm of the gradient during training**. 

Such events are caused by an explosion of long-term components, which can grow exponentially more than short-term ones. 

This results in an unstable network that at best cannot learn from the training data, making the gradient descent step impossible to execute.

Possible solutions: [[Gradient Clipping]], [[Weight Decay]]