#note/tidy 
[[NI-MVI]], [[NI-ZI-07]]
[[Dropout]], [[Regularization]]


## Convolution Formula 
1D conv:
$$(x * w)[t]=\sum_\tau x[t-\tau] w[\tau]$$
2D conv: multiple copies of x translated and scaled by w
$$(x * w)[s, t]=\sum_{\sigma, \tau} x[s-\sigma, t-\tau] w[\sigma, \tau]$$
Continuous convolution: $(f * g)(t)=\int_{-\infty}^{\infty} f(x) \cdot g(t-x) \mathrm{d} x$

**dilated convolution (atrous)**: same number of parameters with larger receptive field - convolution filter is distributed to larger area, there is a space between adjoining filter bits.

**Separable Kernel**: pro jeho vícerozměrnou funkci platí: $G(x, y) = g_{x}(x) \cdot g_{y}(y)$ Potom místo 2d conv. můžeme aplikovat 2x 1d conv., což je rychlejší. Např. Gaussian kernel.


## (max) Pooling
Vrstvy redukují dimenzionalitu a tak nějak redukují výstupy. 
1. rozdělíme feature map na čtverce o velikosti $n + (n-1)\times s$
	* $s$ je parametr pro stride a $n$ je pool size
	* Takže vybereme $n\times n$ pixelů v mřížce a mezi nimi bude $s$ vynechaných míst
2. Na každý pool provedeme redukci (max, average)
3. Výsledky uspořádáme na souřadnice čtverců.