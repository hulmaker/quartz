TARGET DECK: FIT-2021-2
FILE TAGS: ADM FIT-2021-2

## Lec 01 - 18.02.2021

Co je za vlastnost generalizace modelu? #flashcard 
Schopnost dobrého fungování na datech co nikdy neviděl.
<!--ID: 1613660364226-->


definuj categorical cross-entropy error a k čemu je? #flashcard 
$$\hat{p}(x)=\hat{\mathrm{P}}(Y=1 \mid X=x)$$
$$L(Y, \hat{p}(x))=-\sum_{j=1}^{c} \mathbb{1}_{Y=j} \log \hat{p}_{j}(x)=-\log \hat{p}_{Y}(x)$$
Ztrátová funkce pro úlohu klasifikace. Penalizuje velké chyby víc, než ty malé.
<!--ID: 1613660364232-->


co penalizuje jinak MSE oproti MAE? #flashcard 
MSE penalizuje velke chyby mnohem vice nez MAE. MSE vede k tomu, že je ok se plést málo, ale není ok se plést hodně. MAE vede k tomu, že je přesnější, ale sem tam udělá velkou chybu.
<!--ID: 1613660364238-->


Rozdíl mezi error a loss při trénování modelu. #flashcard
Error je chyba pro jedno dato oproti skutečnosti. Loss je nějaká agregace chyb na všech trénovacích datech.
<!--ID: 1613660364242-->


Najde gradientní sestup globální minimum? #flashcard 
Skoro nikdy, najde většinou jen lokální.
<!--ID: 1613660364246-->


Jak odhadnout test error modelu? (generalization error). #flashcard 
$$\overline{\mathrm{err}}_{\text{test}}=\frac{1}{N_{\text{test}}} \sum_{i=1}^{N_{\text{test}}} L\left(Y_{i}, \hat{Y}_{i}\left(x_{i}\right)\right)$$
<!--ID: 1613660364252-->


co je model selection a model assessment #flashcard 
**model selection** - odhad performace více modelů a vybrání z nich nejlepší
**model assessment** - odhad testovaci chyby toho nejlepšího vybraného modelu
<!--ID: 1613660364256-->


Jak rozdělit a použít data, pokud chceš udělat dobře model selection a model assessment? #flashcard 
trénovací, validační a testovací v poměru cca 50:25:25. Na trénovací natrénuju více kandidátů, na validační vyberu nejlepšího kandidátata a na testovací otestuju.
<!--ID: 1613660364260-->


Definuj MSE #flashcard 
$$\mathrm{MSE}=\frac{1}{N} \sum_{i=1}^{N}\left(Y_{i}-\hat{Y}_{i}\right)^{2}$$
<!--ID: 1613660364264-->


Definuj RMSE #flashcard 
$$\mathrm{RMSE}=\sqrt{\mathrm{MSE}}$$
Bude jiná rychlost konvergence, ale pozice extrémů bude stejná jako v MSE. Výhoda je v tom, že RMSE je ve stejných jednotkách jako míra té vysvětlované věci.
<!--ID: 1613660364270-->


Definuj RMSLE #flashcard 
$$\mathrm{RMSLE}=\sqrt{\frac{1}{N} \sum_{i=1}^{N}\left(\log Y_{i}-\log \hat{Y}_{i}\right)^{2}}$$ Je to citlivý na malý odchylky a míň citlivý na velký odchylky.
<!--ID: 1613660364274-->


Definuj MAE #flashcard 
$$\mathrm{MAE}=\frac{1}{N} \sum_{i=1}^{N}\left|Y_{i}-\hat{Y}_{i}\right|$$ Není tolik citlivý na outliery.
<!--ID: 1613660364278-->

## Lec 02 - 25.02.2021

Definuj confusion matrix #flashcard 
![[confusion_matrix.png]]
<!--ID: 1614286642413-->


Definuj TPR, FPR, FNR, TNR #flashcard 
| rates       | $Y=1$                  | $Y=0$                  |
| ----------- | ---------------------- | ---------------------- |
| $\hat{Y}=1$ | $TPR = \frac{TP}{N_+}$ | $FPR = \frac{FP}{N_-}$ |
| $\hat{Y}=0$ | $FNR = \frac{FN}{N_+}$ | $TNR = \frac{TN}{N_-}$ |
$$N_+ = TP+FN, \quad N_- = FP+TN$$
<!--ID: 1614261312660-->


Definuj Accuracy a Precision #flashcard 
$$ACC = \frac{TP+TN}{N}$$ - not suitable for unbalanced datasets
$$PPV = \frac{TP}{TP+FN}$$
precision = PPV = positive predictive value
<!--ID: 1614261312665-->

Definuj F1 score a k čemu je #flashcard 
Harmonic mean of precision and recall.
$F_{1}=\frac{2}{1 / \mathrm{PPV}+1 / \mathrm{TPR}}=2 \frac{\mathrm{PPV} \cdot \mathrm{TPR}}{\mathrm{PPV}+\mathrm{TPR}}$
Užitečné pro nevyvážené datasety, kde $P(Y=1)$
<!--ID: 1614791981367-->


Definuj Mathews correlation coefficient a k čemu je #flashcard 
$$\mathrm{MCC}=\frac{\mathrm{TP} \cdot \mathrm{TN}-\mathrm{FP} \cdot \mathrm{FN}}{\sqrt{(\mathrm{TP}+\mathrm{FP})(\mathrm{TP}+\mathrm{FN})(\mathrm{TN}+\mathrm{FP})(\mathrm{TN}+\mathrm{FN})}}$$
$$ = \frac{TP \cdot TN-FP \cdot FN}{\sqrt{ \widehat{N}_+\widehat{N}_-N_+N_-}}$$
Užitečné pro nevyvážené datasety, je to korelační koeficient mezi $\widehat{Y}$ a $Y$, je symetrická (korelační koeficient mezi predikcí a skutečností)
<!--ID: 1614791981373-->


Definuj ROC curve (reciever operating characteristic) and AUC - (area under curve) #flashcard 
**Ladim parametr t** - pro každé t si změřím TPR a FPR. Sekvence FPR je na ose x a TPR na ose y -> to mi udělá křivnku. Cílem je najít takový t, pro který je TPR co největší a FPR co možná nejmenší.
**Způsob jak najít optimální bod** - vezmi přímku y=x a posouvej jí nahoru. Ten bod, na který narazíš první je nejlepší pro t.
**AUC** - area under curve (selfexplanatory) Čím větší, tím lepší. Dají se tak porovnat modely.
(ROC works on a similar principle as the precision-recall curve and AUC ~ AP)
<!--ID: 1614791981379-->


Popiš k-fold cross-validaci #flashcard 
1. rozdělím si dataset na k stejných částí
2. projíždím k částí cyklem. i-tou použiju na validaci a všechny krom i-te na trénování
3. tím dostanu k odkadů testovací chyby
4. celkový odhad je průměr naměřených hodnot
<!--ID: 1614791981383-->


Kdy chceš použít cross validaci? Popiš její vlastnosti. #flashcard 
- Když mám málo dat, jsem schopný získat rozumnou metriku o modelu. Je to ale 	výpočetně velmi náročný a proto se nevyplatí používat na větší datasety (tam to ostatně není potřeba).
- Odhaduje expected test error, ne tu skutečnou co predikuje jak dobře to pojede v reálu. Odhaduje to průměrnou error toho procesu trénování (pro každý trénování najdu jiný hyper-parametry).
<!--ID: 1614791981387-->



Popiš model evaluation metodou bootstrap #flashcard 
1. Vybírám náhodně body (s opakováním) a vytvořím tak B datasetů
2. Na každým z B ds nafituju model, validaci, test atd
3. Mám B různých setů měření
Mean B chyb dělá podobnou věc jako cross-validace
Můžu ale i koukat na distribuci těch chyb, rozptyl chyb, quartily a analyzovat jak dobrý odhad to je, jestli je rozptyl malý, tak je to dobrý atd.
Bootstrap odhaduje taky expected test error a ne skutecny error.
<!--ID: 1614791981391-->



Definuj AIC (akaike information criterion) a BIC (bayesian information criterion), řekni k čemu jsou. #flashcard 
Metriky co penalizují model podle toho, kolik má parametrů = víc parametrů je větší citlivost na odchylky v inputu atd.
$$AIC=\log L - d$$
$$BIC=\log L - \frac{d}{2} \log N$$
$L$ - likelihood function - čím lepší model, tím větší pravděpodobnost model tomu datasetu přisoudí (pro klasifikaci cross entropy, regression MSE... atd).
$d$ - počet parametrů (degrees of freedom)
$N$ - velikost datasetu
BIC je asymptoticky konzistentní (pokud $N \to \infty$, tak je pst že BIC vybere správný model se blíží 1)
AIC má tendenci vybírat hodně složitý modely a BIC zase jednoduchý. Není teda jasný, co použít. Asi je dobrý vzít oba, porovnat a rozhodnout.
Pro obě metriky platí, že čím větší, tím lepší.
<!--ID: 1614791981395-->

## Lec 03 - 04.03.2021

Popiš ID3 algoritmus #flashcard 
Rekurzivně rozděluji dataset $x_i < a_i$ na stranu $L$ a $R$. Dělím podle information gain $IG(x, a, D)=crit(D)-t_L crit(D_L) - t_R crit(D_R)$
<!--ID: 1615588131307-->


Popiš AdaBoost #flashcard 
Ensamble metoda. Stavíme kaskádu weak learners.
Přiřazujeme váhy datovým bodům podle toho jestli jsou špatně predikované
Finální rozhodnutí je vážené hlasování/průměr
<!--ID: 1615588131311-->


Popiš gradient boosting # flashcard 
Konstruujeme posloupnost weak learners $f^0, ..., f^$
máme loss function $l(y, \hat{y})$, kde y je číslo a $\hat{y}$ 1 proměnná. $l$ je fce 1 promenne
máme velkou loss, což je suma loss přes všchny proměnných

## Lec 05 - 18.03.2021


Co je LOOCV? #flashcard 
Leave-one-out cross-validation. Je to spešl případ k-cross validace, kdy vynechame jedno dato a na tom datu merime chybu. jako (n-1) fold validace.
<!--ID: 1616260958839-->


Co je stratified cross-validation #flashcard 
[link](https://scottclowe.com/2016-03-19-stratified-regression-partitions/)
Nemame vyvazene tridy. Zajistime, aby se v tech tridach vyskytovaly alespon nejake tridy. A aby byly rozlozeny podobne jako realita.
<!--ID: 1616260958848-->


Čím je způsoben bias v předpovědi modelu? #flashcard 
Nedokonalostí modelu. Je to vychýlení.
<!--ID: 1616260958854-->


Jak spočítáš bias v predikci? #flashcard 
$$Bias[\hat{f}] = f-E[\hat{f}]$$
Je to metrika, kterou určíme jaký je odchyl modelu od reality modelu.
<!--ID: 1616260958860-->


Definuj rozptyl, bias a error #flashcard 
Střední hodnota residuí - kvadrát rozdílu středu od predikce
$$\operatorname{Var}(X)=\mathrm{E}\left[(X-\mathrm{E}[X])^{2}\right]=\mathrm{E}\left[X^{2}\right]-\mathrm{E}\left[X\right]^{2}$$
$$Bias[\hat{f}] = f-E[\hat{f}]$$
$$Err = E[(Y-\hat{f})^2]$$
<!--ID: 1616260958865-->


Popiš co dělá model, když máš (velkou-malou)varianci a (velký-malý)bias #flashcard 
Velký bias je velké vychýlení. model se nedokáže přiblížit k datům.
Velká variance je rozptyl odhadů.
![[bias-variance_mx.png]]
<!--ID: 1616260958870-->


Udělej bias a variance dekompozici => Dokaž že $Err = E[(Y-\hat{f})^{2}] = \sigma_{\epsilon}^{2}+\operatorname{Bias}^{2}[\hat{f}]+\operatorname{Var}[\hat{f}]$  když platí $E[y]=E[f+\varepsilon]=E[f]=f$, kde $y=f(x)+\epsilon$ a $\epsilon$ je šum. #flashcard 
$E[(Y-\hat{f})^2] = \sigma^2_\varepsilon + E[(f-\hat{f})^2] + 0$ (trik, kdy dám prvního $-f+f$)
No a $E[(f-\hat{f})^2] = Bias^2[\hat{f}]+Var[\hat{f}]$ (trik, kdy dám dovnitř prvního $+E[\hat{f}]-E[\hat{f}]$)
No a když to spojím, tak mám $E[(Y-\hat{f})^2] = \sigma^2_\varepsilon + Bias^2[\hat{f}]+Var[\hat{f}]$
<!--ID: 1616260958875-->


Jak uděláš bias variance decomposition pro ensamble learning? #flashcard 
Záleží jak to vyhodnocuješ, ale pokud vracíš např. při regresi průměrnou hodnotu, tak výstup ensamblu je jako průměrný model. potom.
$E\left[\frac{1}{M} \sum_{i}\left(\hat{f}_{i}-f\right)^{2}-\frac{1}{M} \sum_{i}\left(\hat{f}_{i}-\bar{f}\right)^{2}\right]=\overline{\text { bias }}^{2}+\frac{1}{M} \overline{v a r}+\left(1-\frac{1}{M}\right) \overline{\text { covar }}$
<!--ID: 1616260958880-->


Popiš kdy využiješ negative correlation learning a jak to uděláš #flashcard 
[gbrown o tom ma disertacku](http://www.cs.man.ac.uk/~gbrown/)
Když mám ensamble learning a dělám bias variance decomposition, tak jejich chyby spolu nějak korelují. My chceme snižovat složku chyby, co vzniká korelací modelů.
Toto je regularizační člen: $R=p_{i}=\left(f_{i}-\bar{f}\right) \sum_{j \neq i}\left(f_{j}-\bar{f}\right)$
mám model i a j. Pokud se budou oba oproti průměru vychylovat na stejnou stranu, tak je to špatný a jsou korelovaný. A tudíž dávám chybě na té straně větší váhu a tudíž průměr bude vychýlen k nim.
Negative correlation learning je to, že k chybě weak learners přidám regularizační člen pronásobený váhou a ten mi zajistí to, že jednotlivý learners "propojím" se zbytkem.
<!--ID: 1616260958885-->


## Lec 06 - 25.03.2021 - Úvod do jádrových metod

Define linear basis expansion model #flashcard 
value $\boldsymbol{x}=(x_1, ..., x_p)^T$ of $X$ gives us target variable $Y$
$$Y=x_1 \varphi_1(\boldsymbol{x}) + ..., x_M \varphi_M(\boldsymbol{x}) + \varepsilon = \boldsymbol{w}^T \boldsymbol{\varphi(x)} + \varepsilon$$
where $\boldsymbol{\varphi} : \chi \rightarrow \mathbb{R}^M$
<!--ID: 1617305841088-->


Describe the $RSS_\lambda(w)$ for linear basis ridge regression #flashcard 
$RSS_\lambda(w) = \mid\mid \boldsymbol{Y-\phi w} \mid\mid^2 + \lambda w^Tw$
<!--ID: 1617305841093-->


Describe normal equation,  $\hat{\boldsymbol{w}}_\lambda$ estimation and prediction $Y$ for the linear basis ridge regression #flashcard 
Normal equation: $\boldsymbol{\phi^TY -  \phi^T\phi w} - \lambda \boldsymbol{w = 0}$
solution for $\lambda > 0$: $\hat{\boldsymbol{w}}_\lambda = (\boldsymbol{\phi^T\phi} + \lambda \boldsymbol{I})^{-1} \boldsymbol{\phi^TY}$
prediction of $Y$ at $x$: $\hat{Y}=\boldsymbol{\hat{w}_\lambda^T \varphi(x)}$
<!--ID: 1617305841097-->


$RSS_\lambda(w) = \mid\mid \boldsymbol{Y-\phi w} \mid\mid^2 + \lambda w^Tw$, definujme $\boldsymbol{w = \phi^T \alpha}$, kde $\boldsymbol{\alpha} \in \mathbb{R}^N$. Jaká je (ne)rovnost mezi $min RSS_\lambda(w)$ a $min RSS_\lambda(\alpha)$? #flashcard 
$min RSS_\lambda(w) \leq min RSS_\lambda(\alpha)$, jelikož když používám $\alpha$, tak mám menší prostor než s $w$. 
Máme ale theorem, který říká, že jsou ta minima stejná a že se dají $w$ a $\alpha$ vzájemně pro to minimum převádět.
<!--ID: 1617305841100-->


Definuj pozitivne definitni, semi-definitivni, negativne .... a indefinitni matici #flashcard 
$\boldsymbol{A} \in \mathbb{R}^{n, n}$ is 
positive semi-definite: $x^TAx \geq 0, \forall x \in \mathbb{R}^{n, n}$
positive definite: $x^TAx \gt 0, \forall x \in \mathbb{R}^{n, n}$
negative definite: $x^TAx \lt 0, \forall x \in \mathbb{R}^{n, n}$
negative semi-definite: $x^TAx \leq 0, \forall x \in \mathbb{R}^{n, n}$
$A$ is indefinite $\iff \exists x, y \in \mathbb{R}^{n, n}, x^TAx \gt 0 \land y^TAy \lt 0$
<!--ID: 1617305841104-->


Define kernel function $k(x, y)$, define Gram matrix #flashcard 
$k(\boldsymbol{x}, \boldsymbol{y}) = \boldsymbol{\varphi(x)^T}\boldsymbol{\varphi(y)}$, where $\boldsymbol{\varphi(x)} = (\varphi_1(\boldsymbol{x}), ..., \varphi_M(\boldsymbol{x}))^T$
Gram matrix: Given a kernel function $k$ and inputs $\boldsymbol{x}_1, . . . ,\boldsymbol{x}_n \in  \chi$, the $n \times n$ matrix $G = (G_{i,j})$, where $G_{i,j} = k(\boldsymbol{x}_i, \boldsymbol{x}_j)$
<!--ID: 1617305841108-->
