---
tags:
  - on/ai
  - note/tidy
---

[[Multi Layer Perceptron]], [[Convolutional Neural Networks (CNN)]], [[NI-MVI]]


Regularization is a set of strategies used in Machine Learning to reduce the generalization error. Most models, after training, perform very well on a specific subset of the overall population but fail to generalize well. This is also known as overfitting. Regularization strategies aim to reduce overfitting and keep, at the same time, the training error as low as possible.



## Selection of techniques
* **L1, L2** - $L_{n e w}(w)=L_{\text {original }}(w)+\lambda\|w\|_1$
* **Weight decay**: $L_{n e w}(w)=L_{\text {original }}(w)+\lambda w^T w$ (weight decay is specified in the weight update rule, L2 reg. is is specified in the objective function)
* **Dropout** - drops a unit (and connections) at training with probability
* **Label smoothing** - Předpokládáme noise v datech, replace hard 0, 1 target class with a softmax $\frac{\epsilon}{k-1}, 1-\epsilon$
* **Early stopping** - stops training when updates don't help on a validation
* **Weight sharing** - forces a group of parameters to be equal
* Batch, layer, instance, group, **normalization**: normalizace skupiny vah


![[Dropout]]