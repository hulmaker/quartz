---
tags:
  - on/ai
---

# ReLU
[wiki](https://en.wikipedia.org/wiki/Rectifier_(neural_networks))
$y=max(0,x)$
* often inactive 
	-> fast and sparse ([paper 1](https://www.cv-foundation.org/openaccess/content_cvpr_2015/html/Sun_Deeply_Learned_Face_2015_CVPR_paper.html) [paper 2](http://proceedings.mlr.press/v15/glorot11a))
* Danger of the [[Dying ReLU Problem]]

# Leaky ReLU (PReLU)
small slope for the negative x.
$y=x \iff x >= 0,\ x*0.01\ \text{otherwise}$
more balanced -> **may** learn faster

## PReLU -> Parametric ReLU
paramerized leaky ReLU -> instead of slope 0.01, there is a parameter.

# ELU (Exponential Linear Unit)
[Fast and Accurate Deep Network Learning by ELUs](https://arxiv.org/abs/1511.07289)
$y=x \iff x >= 0,\ \alpha (e^x-1)\ \text{otherwise}$
\- $\alpha$ is not learned
\- longer computation
\- slower than the [[Activation Functions#Leaky ReLU (PReLU)]]
\+ activations for negative numbers

# SELU (Scaled ELU)
$y=\lambda \cdot ELU(x)$ -> $\alpha \approx 1.673, \lambda \approx 1.0507$

* if you init weights with lecun_normal and use SELU -> the nn remains within bounds [self-normlizing NN](https://arxiv.org/abs/1706.02515)

- Internal normalization is faster than external normalization, which means the network converges faster.
- [[Vanishing Gradient Problem]] and exploding gradient problem is _impossible_, shown by their theorems 2 & 3 in the appendix

# GELU (Gaussian Error Linear Unit)
$\operatorname{GELU}(x)=0.5 x\left(1+\tanh \left(\sqrt{2 / \pi}\left(x+0.044715 x^{3}\right)\right)\right)$

An activation function used in the most recent Transformers – Google's [BERT](https://arxiv.org/abs/1810.04805) and OpenAI's GPT-2.
- state-of-the-art in NLP, specifically Transformer models
- Avoids [[Vanishing Gradient Problem]]
https://paperswithcode.com/method/gelu


# Cross Entropy Loss
It is useful when training a classification problem with C classes