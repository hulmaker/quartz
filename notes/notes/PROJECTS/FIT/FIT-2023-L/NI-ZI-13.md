TARGET DECK: NI-ZI-2023::NI-ADM
FILE TAGS: NI-ZI-2023 NI-ZI-13 NI-ADM

prev::[[NI-ZI-12]]
next::[[NI-ZI-14]]
# Algoritmy pro doporučování

## základní přístupy a způsob vyhodnocení kvality

Algoritmy pro doporučování se dělí do různých kategorií. Podle čeho se dá dělit a jaké jsou kategorie? #flashcard 
Podle typu úlohy: item2user, user2item, item2item, user2user
Podle interakcí
- Explicitní - uživatel ohodnotil 5*
- Implicitní - uživatel shlédl 80% videa
Podle atributů: uživatele-(gender, age, ...), itemu-(popis, metadata, ...)
Podle typu filtrování: kolaborativní, content-based
<!--ID: 1691966314055-->



Jaký je základní princip recommenderů co používají kolaborativní/content-based doporučování? #flashcard 
Kolaborativní: A a B si oblíbí knihu K1. Druhý den si B oblíbí knihu K2. Uživateli A doporučíme knihu K2.
* Hledáme relace mezi uživateli/skupinami na základě jejich chování. Předpokládáme, že se všem líbí podobné věci.
Content-based: A se líbí kniha žánfu drama. Doporučíme mu drama co ještě nečetl.
* Doporučujeme na základě obsahu. Podobný, ale jiný item.
<!--ID: 1691966314056-->



Jaké jsou metriky pro vyhodnocení doporučovacích systémů? #flashcard 
Similarity metrics: Cosine similarity, Jaccard similarity
Predictive metrics: MAE, RMSE ... 
Classification: Presicion@K, Recall@K, HitRatio@K
Ranking: MAP@K
<!--ID: 1691966314057-->



Jak definujeme MAP@K - metrika vhodná pro evaluaci rankingu? #flashcard 
Nejdříve je nutné definovat následující dvě funkce:
$$
\begin{aligned}
& \operatorname{TPseen}(i)=\left\{\begin{array}{cl}
0 & ; i^{t h} \text { is False } \\
\text { TP seen till i } & ; i^{t h} \text { is True }
\end{array}\right. \\
& N(k)=\min \left(k, T P_{\text {total }}\right) \\
\end{aligned}
$$
Pak můžeme definovat average precision a mean average precision jako:
$$
\begin{aligned}
& A P @ k=\frac{1}{N(k)} \sum_{i=1}^k \frac{T P \operatorname{seen}(i)}{i} \\
& m A P @ k=\frac{1}{N} \sum_{i=1}^N A P @ k_i \\
\end{aligned}
$$
<!--ID: 1691966314058-->



## faktorizační metody pro doporučování

Jaká je hlavní myšlenka maticové faktorizace u doporučovacích algoritmů? #flashcard 
Recommender matrix: $m\times n$ matice, s $m$ users a $n$ items. Hodnoty jsou hodnocení itemu userem. Cílem je předpovědět chybějící hodnoty.
Faktorizací rozumíme nějaký netriviální rozklad typu: $R=UV^T$
Základní myšlenka se dá vyjádřit jako: Pro matici $R$, najdi matice nižší dimenze $U$ a $V$ tak, aby hodnoty v R byly dobře aproximovány maticí $UV^T$
<!--ID: 1691966314059-->



Jak formulujeme optimalizační úlohu maticové faktorizace pro doporučovací algoritmy. #flashcard 
Hledáme rozklad matice $R\in \mathbb{R}^{m\times n}$  na netriviální matice nižší dimenze tak aby platilo $R=UV^T$.  kde $U\in \mathbb{R}^{m\times d}, V\in \mathbb{R}^{n\times d}$
Optimalizační kritérium: 
$$
\operatorname{argmin}_{\mathbf{U}, \mathbf{v}} \sum_{(i, j) \in \Omega}\left(r_{i, j}-u_i^T v_j\right)^2+\lambda\left(\sum_x\left\|u_x\right\|^2+\sum_y\left\|v_y\right\|^2\right)
$$
kde $\lambda > 0$ je regularizace, $d$ pozitivní celé číslo udávající dimenzi. (výrazně menší než m, n)
Rate of error: $\left(r_{i, j}-u_i^T v_j\right)^2$
<!--ID: 1691966314060-->



Popište algoritmus alternating least squares (ALS) pro řešení optimalizační úlohy maticové faktorizace u rekomendačních algoritmů. #flashcard 
ALS na střídačku zafixuje jednu nebo druhou matici, kde náhodně inicializuje hodnoty, a v druhé minimalizuje chyby skrze OLS, dokud není splněno kritérium konvergence
1. Náhodně inicializuj U, V
2. Opakuj dokud alg. nekonverguje:
$$
\begin{aligned}
\forall i \in \mathcal{U}, \min _{u_i}\left\|R_{\Omega^i}-u_i^{\top} V_{\Omega^i} \top\right\|^2+\lambda\left\|u_i\right\|^2 &\\
\forall j \in \mathcal{I}, \min _{v_j}\left\|R_{\Omega^j}-v_j{ }^{\prime} U_{\Omega^j} \top\right\|^2+\lambda\left\|v_j\right\|^2 &\\
\end{aligned}
$$
![[alternating_least_squares.png]]
<!--ID: 1691966314061-->



