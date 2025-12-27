---
tags:
  - on/ai
  - source/paper
link: https://arxiv.org/abs/1903.06733
---

* when $y$ is stuck in negative side -> y is always 0. 
* related to the [[Vanishing Gradient Problem]]
* This is unlikely to recover, neuron is then useless.
* likely to occur when LR is too high, or with large negative bias

## possible solutions
* Smaller LR, greater bias
* Leaky ReLU, PReLU, ELU, SELU, GELU -> **reduced performance!**
* [[Activation Functions]]
* weight initialization (**R**andomized **A**symetric **I**nitialization)
* wider NN -> they reduce $P(\text{dying ReLU})$, but expensive

## detection
count zeroes in the output activation -> NN is sparse, if no. active neurons < 50%
