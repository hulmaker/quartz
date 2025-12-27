---
tags:
  - on/ai
---
Related to: [[Multi Layer Perceptron]]

Often in a form of L2 [[Regularization]]. Helps to keep wights within a reasonable range by adding their scaled norm into the loss function.

The most simple example of the L2 regularization is in the [Ridge regression](https://en.wikipedia.org/wiki/Ridge_regression). It's L1 alternative is known as the [Lasso regresion](https://en.wikipedia.org/wiki/Lasso_(statistics))


$$
L_{\text {new }}(w)=L_{\text {original }}(w)+\lambda w^T w
$$

Weight decay is also often used in deep learning. For example with [[Adam Optimiser]]. Authors of [[AdamW Optimiser]] showed, that L2 regularisation is not relatively equal penalisation. They propose "Decoupled weight decay" - also use in the [[Prodigy Optimiser]]