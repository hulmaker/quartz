---
tags:
  - ML
  - paper
link: https://paperswithcode.com/method/adagrad
---
AdaGrad (Duchi et al., 2011)

**AdaGrad** is a stochastic optimization method that adapts the [[Learning Rate]] to the parameters. It performs smaller updates for parameters associated with frequently occurring features, and larger updates for parameters associated with infrequently occurring features. 

In its update rule, Adagrad modifies the general learning rate $\eta$ at each time step $t$ for every parameter $\theta_i$ based on the past gradients for $\theta_i$

$$
\theta_{t+1, i}=\theta_{t, i}-\frac{\eta}{\sqrt{G_{t, i i}+\epsilon}} g_{t, i}
$$

Benefit: 
* automatic LR tuning
* works well for sparse gradients

Weakness: 
* accumulation of the squared gradients in the denominator. 
* Since every added term is positive, the accumulated sum keeps growing during training, causing the learning rate to shrink and becoming infinitesimally small.

