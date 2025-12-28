---
tags:
  - ML
  - paper
link: https://paperswithcode.com/method/layer-normalization
---

$$
\begin{gathered}
\mu^l=\frac{1}{H} \sum_{i=1}^H a_i^l \\
\sigma^l=\sqrt{\frac{1}{H} \sum_{i=1}^H\left(a_i^l-\mu^l\right)^2}
\end{gathered}
$$

Normalizes each sample in batch across channels. The problem with [[Batch Normalization]] is, that you need very large batches. Therefore it is useful for example in. Layer Norm is useful for example in the [[Reinforcement Learning]]. For example with chess in [[AlphaZero]], if you don't have a beefy computer, you won't have large enough batches.