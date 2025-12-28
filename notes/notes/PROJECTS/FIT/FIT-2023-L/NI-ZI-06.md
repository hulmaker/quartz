TARGET DECK: NI-ZI-2023::NI-PDD
FILE TAGS: NI-ZI-2023 NI-ZI-06 NI-PDD

prev::[[NI-ZI-05]]
next::[[NI-ZI-07]]
# Lineární projekce dat do prostoru o méně dimenzích: metoda hlavních komponent (PCA), lineární diskriminační analýza (LDA)


Popiš Random mapping (Random Projection) jakožto způsob lineární redukce dimenzionality #flashcard 
Pomocí náhodné matice R s jednotkovými sloupci, zobraz d dimenzí na k dimenzí.
$$X_{k, N}^{RP} = R_{k,d}X_{d, N}$$
* $X_{k,n}^{RP}$ - Random Projection (výsledek dimenze k)
* $R_{k, d}$ - random matice
* $X_{d, n}$ - původní data dimenze d
<!--ID: 1691966314084-->



Popiš PCA (Principal Component Analysis) #flashcard 
Maximalizuje rozptyl v datech pomocí ortogonální projekce.
* Minimalizujeme information loss: $\min \mid\mid X-\hat{X} \mid\mid$
* Prvních k nejvýznamějších vlastních vektorů a čísel z $U\Sigma V^T$ (SVD)
* lze počítat exaktně, ale i jako optimalizační problém
* dominantní směr nemusí odpovídat třídám v datech (z separabilních dat můžou být neseparabilní)
<!--ID: 1691966314085-->



Popis ICA (Independent Component Analysis) #flashcard 
Předpoklad: data jsou mix různých signálů
Cíl: Najít transformaci, co signály rozdělí $WAs=Wx=z$
![[PROJECTS/FIT/FIT-2023-L/media/ica.png]]
$S_i$: neznámé vstupy, $A$: neznámá transformace, $x$: naše data, $W$: hledaná transformace, $z$: chceme rozmotat x aby byly signály podobné původním
* Je to optimalizační problém
* PCA se snaží maximalizovat informační hodnotu (rozptyl), Zatímco ICA se snaží proložit data hlavními směry
<!--ID: 1691966314086-->



Popiš LDA (Linear Discriminant Analysis) #flashcard 
Snaží se zároveň:
* maximalizovat **rozptyl centroidů**: $S_b=\sum^C\left(\boldsymbol{\mu}_i-\boldsymbol{\mu}\right)\left(\boldsymbol{\mu}_i-\boldsymbol{\mu}\right)^T$
* minimalizovat **vnitřní rozptyl třídách**: $S_w=\sum_{i=1}^C \sum_{j=1}^{M_i}\left(y_j-\boldsymbol{\mu}_i\right)\left(y_j-\boldsymbol{\mu}_i\right)^T$
* takže: $\max \frac{\left|U^T S_b U\right|}{\left|U^T S_w U\right|}$
Řešení je dáno vlastními vektory $S_B u_k=\boldsymbol{\lambda}_k S_w u_k$, kde $u_k$: vlastní vektory, $\lambda$: parametr
<!--ID: 1691966314087-->



Porovnejte metody lineární projekce dat do prostoru o méně dimezní #flashcard 
- PCA: lepší na malých datech, získání nejexpresivnějších příznaků, komprese informací
- ICA: nejlepší při slepém oddělování zdrojů (informací), kdy nemáme k dispozici predikovanou třídu
- LDA: dobrá na velkých a reprezentativních datech pro každou třídu, získání nejrozlišitelnějcích příznaků
<!--ID: 1691966314088-->



# Nelineární metody redukce dimensionality (Sammonova projekce)


Stručný popis t-SNE #flashcard 
Nelineární redukce dimenzionality. Formulováno jako optimalizační problém, který zachovává relativní vzdálenosti mezi daty.
* Iterační algoritmus
* Používá se primárně pro vizualizace dat o vysoké dimenzi.
* Hledá nejbližší sousedy
* minimalizuje [Kullback–Leibler divergence](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence) (původně Euler distance)
* Občas se chová záhadně a dělá zavádějící výsledky. (velikosti clusterů nic neznamenají, často se vytváří clustery kde nejsou, vzdálenosti mezi clustery nemusí nic znamenat, random noise nevypadá vždycky random) 
* Musí se dobře rozumět parametrizaci aby vizu byla k něčemu
https://distill.pub/2016/misread-tsne/
<!--ID: 1691966314089-->



Sammon Mapping #flashcard 
Nelineární metoda redukce dimenzionality, co se snaží zachovat relativní vzdálenosti a patterny v datech. Nedělá transformaci souřadnic, ale přeorganizuje data tak, aby byly zachoány patterny a vzdálenosti.
$$Err=\frac{1}{\sum_{i<j} d_{i j}^*} \sum_{i<j} \frac{\left(d_{i j}^*-d_{i j}\right)^2}{d_{i j}^*}$$
$d_{ij}^**$ je vzdálenost v původní dimenzi,  $d_{ij}$ je vzdálenost v nové projekci. 
Použijem gradientní sestup.
<!--ID: 1691966314090-->
