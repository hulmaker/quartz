---
tags:
  - on/ai
---

[[Autoencoder]], [[Generative AI]], [[Stable Diffusion]]

A variational autoencoder (VAE) provides a _probabilistic_ manner for describing an observation in latent space. Thus, rather than building an encoder which outputs a single value to describe each latent state attribute, we'll formulate our encoder to describe a probability distribution for each latent attribute.
![[vae.png]]
Z distribucí co dostaneme v latentním prostoru pak můžeme samplovat a dostaneme tak různé výstupy ve stejné distribuci.
[tohle](https://www.jeremyjordan.me/variational-autoencoders/) je super článek.


## Loss
![](https://www.jeremyjordan.me/content/images/2018/03/Screen-Shot-2018-03-17-at-11.31.15-PM.png)
Our loss function for this network will consist of two terms, one which penalizes reconstruction error (which can be thought of maximizing the reconstruction likelihood as discussed earlier) and a second term which encourages our learned distributioni $q(z\mid x)$ to be similar to the true prior distribution $p(x)$, which we'll assume follows a unit Gaussian distribution, for each dimension of the latent space.
$$\mathcal{L}(x, \hat{x})+\sum_j K L\left(q_j(z \mid x) \| p(z)\right)$$

## Applications
[[Stable Diffusion]]
Používají se variational autoencoder (VAE), a generative AI algorithm that uses deep learning to generate new content, detect anomalies and remove noise. Dále se dají použít pro generování textu, časových řad, ale i videa.