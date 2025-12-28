---
tags:
  - ML
link: https://en.wikipedia.org/wiki/Vanishing_gradient_problem
---
**Diminishing gradients during the training of deep neural networks**. It occurs when the gradients propagated backward through the layers become very small, making it difficult for the network to update the weights effectively.

Particularly associated with sigmoid and hyperbolic tangent

Methods like LSTM, GRUs, RNNs suffer from this

#### Indicators:
- weights ****converging to 0**** or stagnation over training epochs
- loss function fails to decrease significantly, or if there is erratic behaviour in the learning curves
- examining the gradients during backpropagation


#### Solutions
* [[Batch Normalization]]
* ReLU, GeLU, SeLU...
* Skip Connections (ResNets)
* [[Gradient Clipping]]