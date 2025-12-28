TARGET DECK: Obsidian::DS

[[NI-ZI-04]], [[NI-ZI-05]], [[NI-ZI-06]]

## Dimensionality Reduction
[[Dimensionality Reduction]]

### Linear Dimensionality Reduction

Popiš PCA (Principal Component Analysis) #flashcard 
PCA je rozklad, který se dá zapsat následovně: $T=XW$
$W \in \mathbb{R}^{p, p}$, kde sloupce $W_{\bullet, i}$ jsou vlastní vektory $X^TX$
PCA Maximalizuje rozptyl v datech pomocí ortogonální projekce. 
* Minimalizujeme information loss: $\min \mid\mid X-\hat{X} \mid\mid$
* Prvních k nejvýznamějších vlastních vektorů a čísel z $U\Sigma V^T$ (SVD)
- Konkrétně: $T=XW=U\Sigma W^TW=U\Sigma$
* lze počítat exaktně, ale i jako optimalizační problém
* dominantní směr nemusí odpovídat třídám v datech (z separabilních dat můžou být neseparabilní)
<!--ID: 1729010154076-->



Jaký je vztah PCA (Principal Component Analysis) a SVD (Singular Value Decomposition)? #flashcard 
SVD: $X=U\Sigma W^T$
PCA: $T=XW$, platí: $T=XW=U\Sigma W^TW=U\Sigma$
* Prvních k nejvýznamějších vlastních vektorů a čísel z $U\Sigma V^T$ (SVD)
<!--ID: 1729010154077-->



Popis ICA (Independent Component Analysis) #flashcard 
[wiki](https://en.wikipedia.org/wiki/Independent_component_analysis)
Předpokládáme, že data jsou mix různých nezávislých komponent. Chceme najít transformaci, co signály rozdělí:
$z=Wx=WAs$
$S_i$: neznámé vstupy, $A$: neznámá transformace, $x$: naše data, $W$: hledaná transformace, $z$: chceme rozmotat x aby byly signály podobné původním
* Je to optimalizační problém
* PCA se snaží maximalizovat informační hodnotu (rozptyl), Zatímco ICA se snaží proložit data hlavními směry
![[EXTRAS/Media/ica.png]]
<!--ID: 1729010154078-->




Co je to LDA? (Linear Discriminant Analysis) #flashcard 
LDA ([wiki](https://en.wikipedia.org/wiki/Linear_discriminant_analysis)) se pokouší najít takovou lineární kombinaci featurs, co charakterizuje/dělí dvě a více tříd v datech.
Snaží se zároveň:
* maximalizovat **rozptyl centroidů**: $S_b=\sum^C\left(\boldsymbol{\mu}_i-\boldsymbol{\mu}\right)\left(\boldsymbol{\mu}_i-\boldsymbol{\mu}\right)^T$
* minimalizovat **vnitřní rozptyl třídách**: $S_w=\sum_{i=1}^C \sum_{j=1}^{M_i}\left(y_j-\boldsymbol{\mu}_i\right)\left(y_j-\boldsymbol{\mu}_i\right)^T$
* takže: $\max \frac{\left|U^T S_b U\right|}{\left|U^T S_w U\right|}$
Řešení je dáno vlastními vektory $S_B u_k=\boldsymbol{\lambda}_k S_w u_k$, kde $u_k$: vlastní vektory, $\lambda$: parametr
<!--ID: 1729010154079-->



Porovnejte metody lineární projekce dat do prostoru o méně dimezní. Kdy byste jaké použili? #flashcard 
- **PCA**: lepší na malých datech, získání nejexpresivnějších příznaků, komprese informací
- **ICA**: nejlepší při slepém oddělování zdrojů (informací), kdy nemáme k dispozici predikovanou třídu
- **LDA**: dobrá na velkých a reprezentativních datech pro každou třídu, získání nejrozlišitelnějcích příznaků
<!--ID: 1729010154080-->


### Nelineární metody redukce dimensionality (Sammonova projekce)


Stručný popis t-SNE #flashcard 
Nelineární redukce dimenzionality. Formulováno jako optimalizační problém, který zachovává relativní vzdálenosti mezi daty.
* Iterační algoritmus
* Používá se primárně pro vizualizace dat o vysoké dimenzi.
* Hledá nejbližší sousedy
* minimalizuje [Kullback–Leibler divergence](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence) (původně Euler distance)
* Občas se chová záhadně a dělá zavádějící výsledky. (velikosti clusterů nic neznamenají, často se vytváří clustery kde nejsou, vzdálenosti mezi clustery nemusí nic znamenat, random noise nevypadá vždycky random) 
* Musí se dobře rozumět parametrizaci aby vizu byla k něčemu
https://distill.pub/2016/misread-tsne/
<!--ID: 1729010154081-->



Sammon Mapping #flashcard 
Nelineární metoda redukce dimenzionality, co se snaží zachovat relativní vzdálenosti a patterny v datech. Nedělá transformaci souřadnic, ale přeorganizuje data tak, aby byly zachoány patterny a vzdálenosti.
$$Err=\frac{1}{\sum_{i<j} d_{i j}^*} \sum_{i<j} \frac{\left(d_{i j}^*-d_{i j}\right)^2}{d_{i j}^*}$$
$d_{ij}^**$ je vzdálenost v původní dimenzi,  $d_{ij}$ je vzdálenost v nové projekci. 
Použijem gradientní sestup.
<!--ID: 1729010154082-->



## Undersampling
[[Undersampling]]
https://en.wikipedia.org/wiki/Oversampling_and_undersampling_in_data_analysis

Proč nám vadí nevybalancovaná data? Co s tím lze dělat? #flashcard 
Roziko overfittingu.
* under sampling - odeberu nějaké datové body z dominantních tříd
* over sampling - generuju data do malých tříd - obecně lepší než undersampling.
* Bodům při učení přidělím váhy významnosti podle toho do jak velké třídy patří
<!--ID: 1729010154083-->



Jaké znáš undersampling metody? Kontext zpracování dat. #flashcard 
**Random**: Náhodný výběr
**Tomek links**: Najdem tomkovy spoje a odstraníme z nich body z majoritní třídy
**Condensing**: retain points along the decision boundary
* **Condensed Nearest Neighbor**:  selects instances near the decision boundary
* **Reduced NN**: Remove a smple if doing so does not cause any incorrect classifications
* **Proximity Graphs**:  NN, min. spanning tree, Gabriel, Delaunay, RNG
**Editing**: 
* **Wilson Editing**: Remove points that do not agree with the majority of their kNN
* **Multi-edit**: repeatedly apply Wilson editing
**Neighborhood Cleansing Rule**: Třídy V (velká), M (malá), bod b, 3 neighbors. Odstraň $b$, pokud je z V a sousedi ho přehlasují. Odstraň sousedy, pokud jsou z V a b je z M.
Extended Nearest Neighbor: odebere jakýkoli bod, jehož třída se liší od třídy alespoň 2 ze 3 jeho NN
**IB3**: Odstraní špatně klasifikované body.
<!--ID: 1729010154084-->


## Oversampling
[[Oversampling]]

Jaké znáš oversampling metody #flashcard 
SMOTE: Udělej kNN, vem náhodný pár z minoritní třídy a interpoluj
Tomek Links: random interpoluj tomek link
<!--ID: 1729010154085-->


## Feature Selection
[[Feature Selection]]

Jaké metriky hodnocení relevance se používají pro feature selection v kontextu zpracování dat? #flashcard 
- **t-test**: slouží k ověření hypotéz o konkrétní střední hodnotě/zda dvě normální rozdělení mají stejný rozptyl/střední hodnotu
- **korelace**: Lineární závislost mezi proměnnými (přímá/nepřímá)
	- Spearman
	- Pearson correlation coefficient $\rho_{X, Y}=\frac{\operatorname{cov}(X, Y)}{\sigma_X \sigma_Y}=\frac{E\left\{\left(X-\mu_X\right)\left(Y-\mu_Y\right)\right\}}{\sigma_X \sigma_Y}$
- **entropie**: očekávané množství informace, které příznak nese $H=-\sum_i P_i \log P_i$
- **Mutual information coefficient** $MI(X, Y) = \int P(X, Y) \log \frac{P(X, Y)}{P(X)P(Y)} dXdY$
<!--ID: 1729010154086-->


## Missing Values
[[Missing Values]]

Jaké metody pro vypořádání se s chybějícími hodnotami znáš? (NI-PDD) #flashcard 
* Smazání řádku, který obsahuje chybějící hodnotu v některém z příznaků
* Nahrazení vhodnou hodnotou (0, -1, inf)...
* Pro každý příznak spočítám mean/median a tím je v každém sloupci nahradím
* Hodnoty na základě shlukové analýzy (kNN, k-means, hierarchical)
<!--ID: 1729010154087-->



## Outlier Detection
[[Outlier Detection (Data Science)]]

Jak lze v datech detekovat odlehlé hodnoty? #flashcard 
**Kouknu a vidim**:
* Pohledem např. na graf vidím vzdálené hodnoty
**Statistika**:
* výpočty nad daty jako rozptyl, kolik standartních odchylek je bod vzdálen od středu atd.
**Pomocí shlukové analýzy**:
* Hierarchické shlukování: Ti co se spojí poslední jsou daleko
* K-means: nějaké skupiny obsahují výrazně méně vzorků, nebo jsou daleko od ostatních, nebo mají velký vnitřní rozptyl
* kNN průměrná vzdálenost sousedů je o dost větší...
<!--ID: 1729010154088-->



Jak se lze vypořádat s odlehlými hodnotami v datech? #flashcard 
* do nothing
* enforce upper and lower bounds
* let binning handle the problem
* Use cluster analysis
* Examine data statistics
<!--ID: 1729010154089-->
