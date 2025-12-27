---
tags:
  - on/mathematics
  - on/statistics
  - on/DS
---
## Linear projections
[[NI-PDD]], [[NI-ZI-06]]

### Principal Component Analysis (PCA)
PCA je rozklad, který se dá zapsat následovně: $T=XW$
$W \in \mathbb{R}^{p, p}$, kde sloupce $W_{\bullet, i}$ jsou vlastní vektory $X^TX$
PCA Maximalizuje rozptyl v datech pomocí ortogonální projekce. 
* Minimalizujeme information loss: $\min \mid\mid X-\hat{X} \mid\mid$
* lze počítat exaktně, ale i jako optimalizační problém
* dominantní směr nemusí odpovídat třídám v datech (z separabilních dat můžou být neseparabilní)

#### Souvislost PCA a SVD
K PCA potřebujeme prvních k nejvýznamějších vlastních vektorů a čísel z $X$
SVD: $X=U\Sigma W^T$
PCA: $T=XW$, platí: $T=XW=U\Sigma W^TW=U\Sigma$

### Independent Component Analysis (ICA)
[wiki](https://en.wikipedia.org/wiki/Independent_component_analysis)
Předpokládáme, že data jsou mix různých nezávislých komponent. Chceme najít transformaci, co signály rozdělí:
$z=Wx=WAs$
$S_i$: neznámé vstupy, $A$: neznámá transformace, $x$: naše data, $W$: hledaná transformace, $z$: chceme rozmotat x aby byly signály podobné původním
* Je to optimalizační problém
* PCA se snaží maximalizovat informační hodnotu (rozptyl), Zatímco ICA se snaží proložit data hlavními směry
![[EXTRAS/Media/ica.png]]

### Linear Discriminant Analysis (LDA)
LDA ([wiki](https://en.wikipedia.org/wiki/Linear_discriminant_analysis)) se pokouší najít takovou lineární kombinaci featurs, co charakterizuje/dělí dvě a více tříd v datech.
Snaží se zároveň:
* maximalizovat **rozptyl centroidů**: $S_b=\sum^C\left(\boldsymbol{\mu}_i-\boldsymbol{\mu}\right)\left(\boldsymbol{\mu}_i-\boldsymbol{\mu}\right)^T$
* minimalizovat **vnitřní rozptyl třídách**: $S_w=\sum_{i=1}^C \sum_{j=1}^{M_i}\left(y_j-\boldsymbol{\mu}_i\right)\left(y_j-\boldsymbol{\mu}_i\right)^T$
* takže: $\max \frac{\left|U^T S_b U\right|}{\left|U^T S_w U\right|}$
Řešení je dáno vlastními vektory $S_B u_k=\boldsymbol{\lambda}_k S_w u_k$, kde $u_k$: vlastní vektory, $\lambda$: parametr

### Porovnání lineárních projekcí
- **PCA**: lepší na malých datech, získání nejexpresivnějších příznaků, komprese informací
- **ICA**: nejlepší při slepém oddělování zdrojů (informací), kdy nemáme k dispozici predikovanou třídu
- **LDA**: dobrá na velkých a reprezentativních datech pro každou třídu, získání nejrozlišitelnějcích příznaků

## Nelineární metody redukce dimensionality 

### Sammon mapping
[wiki](https://en.wikipedia.org/wiki/Sammon_mapping)
Nelineární metoda redukce dimenzionality, co se snaží zachovat relativní vzdálenosti a patterny v datech. Nedělá transformaci souřadnic, ale přeorganizuje data tak, aby byly zachoány patterny a vzdálenosti.
$$Err=\frac{1}{\sum_{i<j} d_{i j}^*} \sum_{i<j} \frac{\left(d_{i j}^*-d_{i j}\right)^2}{d_{i j}^*}$$
$d_{ij}^**$ je vzdálenost v původní dimenzi,  $d_{ij}$ je vzdálenost v nové projekci. 
Použijem gradientní sestup.

### t-SNE
Nelineární redukce dimenzionality. Formulováno jako optimalizační problém, který zachovává relativní vzdálenosti mezi daty.
* Iterační algoritmus
* Používá se primárně pro vizualizace dat o vysoké dimenzi.
* Hledá nejbližší sousedy
* minimalizuje [Kullback–Leibler divergence](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence) (původně Euler distance)
* Občas se chová záhadně a dělá zavádějící výsledky. (velikosti clusterů nic neznamenají, často se vytváří clustery kde nejsou, vzdálenosti mezi clustery nemusí nic znamenat, random noise nevypadá vždycky random) 
* Musí se dobře rozumět parametrizaci aby vizu byla k něčemu
https://distill.pub/2016/misread-tsne/


Lze použít i [[Autoencoder]]