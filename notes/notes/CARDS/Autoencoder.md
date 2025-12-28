---
tags:
  - on/ai
---
[[Variational Autoencoder (VAE)]]

Type of neural network used for encodings (supervised). First, you somehow encode the input to do [[Dimensionality Reduction]]. Then we try to reconstruct the original input as as close as possible. (intention: copy input to its output)

![[autoencoder_schema.png]]

We basically try to reduce the input to it’s essence which defines the original image.

Effective for solving many problems (face recognition, semantic meaning of words).

### Usage in Computer vision
Často se používá architektura U-net, která mezi encoder a decoder přidává residual connections:
Superresolution, denoising, image compression, dogenerování barev, oldify, image classification, image generation, semantic segmentation
