---
tags:
  - on/ai
  - source/paper
  - on/algorithm
link: https://paperswithcode.com/method/rmsprop
---

RMSProp (Tieleman & Hinton, 2012),

**RMSProp** is an unpublished adaptive learning rate optimizer [proposed by Geoff Hinton](http://www.cs.toronto.edu/~tijmen/csc321/slides/lecture_slides_lec6.pdf). The motivation is that the magnitude of gradients can differ for different weights, and can change during learning, making it hard to choose a single global learning rate. RMSProp tackles this by keeping a moving average of the squared gradient and adjusting the weight updates by this magnitude. The gradient updates are performed as:

$$
\begin{aligned}
E\left[g^2\right]_t & =\gamma E\left[g^2\right]_{t-1}+(1-\gamma) g_t^2 \\
\theta_{t+1} & =\theta_t-\frac{\eta}{\sqrt{E\left[g^2\right]_t+\epsilon}} g_t
\end{aligned}
$$

