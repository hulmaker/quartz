---
tags:
  - on/ai
  - on/CV
  - source/paper
link: https://link.springer.com/article/10.1023/B:VISI.0000029664.99615.94
---
It is a [[Keypoint Descriptor]]

* A 4x4 histogram lattice of orientation histograms (2x2 shown)
* Orientations quantized (with interpolation) into 8 bins
* Each bin contains a weighted sum of the norms of the image
gradients around its center, with complex normalization

![SFIT descriptor](https://www.researchgate.net/publication/301817766/figure/fig5/AS:669387199631388@1536605753750/SIFT-descriptor-The-well-known-SIFT-descriptor-consists-of-3D-histograms-of-image.png)

* the descriptor can also bee seen as a 3D histogram

## RootSIFT
- SIFT vectors are compared using L2 distance - kernel is dot product. But SIFT is a histogram -> there are better ways to compare histograms

[Hellinger kernel](https://en.wikipedia.org/wiki/Hellinger_distance) for L1-normalized histograms. 

**implementation**: 
```python
if use_rootsift:
	desc /= desc.sum(axis=1, keppdims=True) + 1e-8
	desc = np.sqrt(desc)
```

[Arandjelovic and Zisserman. CVPR 2012](https://ieeexplore.ieee.org/abstract/document/6248018?casa_token=sEZaHvWbivgAAAAA:gHFRz7msTUF8Ujv-CurTaAd1RK6Fu5aay5bmbiPoAjU2ew6kZ07jhXQGQmDDrZJwPqcQ-dJ1kkE)