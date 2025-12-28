---
tags:
  - ML
  - CV
link: https://en.wikipedia.org/wiki/Local_binary_patterns
---
[[Keypoint Descriptor]]
 
* compare the center $g_c$ with it's neighbourhood -> this will result in a binary number of length **P**
* To ensure rotation invariant LBP, rotate the binary number with binary shift. -> then the result is the smallest number of all rotations

easy, fast, good for textures. Works well with [HOG descriptor](https://en.wikipedia.org/wiki/Histogram_of_oriented_gradients)

![LBP](https://www.researchgate.net/publication/341341744/figure/fig1/AS:890572973813761@1589340551159/Visualization-of-calculation-of-Local-Binary-Pattern-LBP-An-example-region-of-the.ppm)