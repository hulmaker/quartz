TARGET DECK: Obsidian::ML

[[NI-ZI-11]], [[NI-ZI-12]], [[NI-ZI-13]]

## Ensemble metody

# Ensemble metody: rozdíl mezi základními metodami (např. Bagging, Boosting, XGBoost).

Co to jsou ensemble metody? Kategorizuj je a uveď příklady. #flashcard 
Techniky, které vytváří vícero modelů podílejících se na predikci výsledků.
**Bagging**: Na náhodných podmnožinách dat natrénuj estimátory, jejichž predikce agregujeme do finální predikce
* **Random Forests**
**Boosting**: Datovým bodům přiřazujeme významnost.
* **AdaBoost**: Kaskády N weak learners, konstruováno postupně, agregace: hlasování/průměr
* **GradientBoosting**: (XGBoost): Zobecnění boostingu pro libovolnou derivovatelnou ztrátu.
Jako klasifikátory se typicky používaljí stromy, ale lze se setkat i s modely jako kNN atd.
<!--ID: 1729010154042-->



Ensemble metody - Popiš princip Bagging a uveď výhody/nevýhody #flashcard 
**Bootstrap Aggregating** (bagging):
1. sampling with replacement to allow for variation
2. training a model on each subset: decision tree, neural network, kNN, ...
3. Aggregating predictions: average, mode, voting ...
Větší stabilita predikcí, menší overfitting, vyšší složitost algoritmu, náchylné na bias
<!--ID: 1729010154043-->



Ensemble metody - Popiš princip Boosting a uveď výhody/nevýhody #flashcard 
**Boosting**: Iterativní trénování na jednom datasetu se zaměřením na problémové datové body.
* Kombinuje vícero weak learners a pomocí agregace predikuje finální výsledek
* vyšší složitost, snadný overfitting, větší variance, nižší bias
* modely: 1-2 úrovňové stromy, naive Bayes, kNN
<!--ID: 1729010154044-->




Ensemble metody - Popiš princip AdaBoost. #flashcard 
Kaskády weak learners, iterativní učení, těžké datové body mají vyšší váhu, výsledná predikce je vážená kombinace slabých predikcí.
Amount of say (classifier weight $\propto$ accuracy): $\alpha_i=\frac{1}{2} \log _2 \frac{1-\text { error }_i}{\text { error }_i}$
Final sample weights are summarized over all predictions and normalized:
* Correct classified weight: $\bar{w}_j^{i+1}=w_j^i e^{-\alpha_i}$
* Misclassified weight: $\bar{w}_j^{i+1}=w_j^i e^{\alpha_i}$
<!--ID: 1729010154045-->



Ensemble metody - Pipiš princip GradientBoosting #flashcard 
[yt](https://youtu.be/3CC4N4z3GJc), [lecture 1](https://courses.fit.cvut.cz/NI-ADM/@B212/lectures/index.html), [lecture notes](https://courses.fit.cvut.cz/NI-ADM/@B212/lectures/files/NI-ADM-03-04-notes.pdf)
N weak learners, iterativní učení, výsledná predikce je vážená kombinace slabých predikcí
Loss musí mít druhou derivaci (Taylorův polynom)
**XGBoost**:
* objective function odvozujeme obecně pro libovolnou derivovatelnou loss
* Musíme se jen rozhodnout, jaký podstrom budeme dál větvit. To je NP-hard
* Proto používáme greedy alg jako v ID3
* Greedy alg. dělí strom na L a R podle Gain
* Gain je odvozený od druhého Taylora objective function
* Gain je něco jako krit(D)-krit(DL)-krit(DR)
<!--ID: 1729010154046-->



# Linear Basis Expansion Model

Linear model - Describe the ordinary least squares OLS, and the residual sum of squares RSS. #flashcard 
$RSS(w)=\sum^N_{i=1}(Y_i-w_Tx_i)^2=\mid\mid Y-Xw \mid\mid^2$
The minimum is given by the solution of the normal equation corresponding to 
$\nabla RSS(w)=0 \iff X^TY-X^TXw=0$
When $X^TX$ is regular, the solution is $\hat{w}_{OLS} = (X^TX)^{-1}X^TY$
<!--ID: 1729010154047-->



Jakou roli hrají bázické funkce v linear basis expansion model? Vyjmenuj nějaké příklady. (ADM) #flashcard 
Dovolují nám do modelu přidat nelinearitu. Bázické funkce transformují linear features.
Basis function choices:
* $\varphi(x) = x_i$
* $\varphi(x) = x_i^2$, or polynomial regression: $\varphi(x) = x_kx_\ell$
* $\varphi(x)=\log(x_i), \sqrt{x_i}, \sin(x_i), ...$
* $\varphi(x) = \max(0, x_i)$
<!--ID: 1729010154048-->



Define linear basis expansion model and provide examples of basis functions. (ADM) #flashcard 
value $\boldsymbol{x}=(x_1, ..., x_p)^T$ of $X$ gives us target variable $Y$
$$Y=x_1 \varphi_1(\boldsymbol{x}) + ..., x_M \varphi_M(\boldsymbol{x}) + \varepsilon = \boldsymbol{w}^T \boldsymbol{\varphi(x)} + \varepsilon$$
where $\boldsymbol{\varphi} : \chi \rightarrow \mathbb{R}^M$
Basis function choices:
* $\varphi(x) = x_i$
* $\varphi(x) = x_i^2$, or polynomial regression: $\varphi(x) = x_kx_\ell$
* $\varphi(x)=\log(x_i), \sqrt{x_i}, \sin(x_i), ...$
* $\varphi(x) = \max(0, x_i)$
<!--ID: 1729010154049-->



Describe the $RSS_\lambda(w)$ (residual sum of squares) for linear basis ridge regression #flashcard 
$RSS_\lambda(w) = \mid\mid \boldsymbol{Y-\Phi w} \mid\mid^2 + \lambda w^Tw$, where
$$
\boldsymbol{\Phi}=\left(\begin{array}{c}
\boldsymbol{\varphi}\left(\boldsymbol{x}_1\right)^T \\
\vdots \\
\boldsymbol{\varphi}\left(\boldsymbol{x}_N\right)^T
\end{array}\right)=\left(\begin{array}{ccc}
\varphi_1\left(\boldsymbol{x}_1\right) & \cdots & \varphi_M\left(\boldsymbol{x}_1\right) \\
\vdots & \ddots & \vdots \\
\varphi_1\left(\boldsymbol{x}_N\right) & \cdots & \varphi_M\left(\boldsymbol{x}_N\right)
\end{array}\right), \quad \boldsymbol{Y}=\left(\begin{array}{c}
Y_1 \\
\vdots \\
Y_N
\end{array}\right), \quad \boldsymbol{\varepsilon}=\left(\begin{array}{c}
\varepsilon_1 \\
\vdots \\
\varepsilon_N
\end{array}\right)
$$
<!--ID: 1691251771704-->



Describe normal equation,  $\hat{\boldsymbol{w}}_\lambda$ estimation and prediction $Y$ for the linear basis ridge regression #flashcard 
Normal equation: $\boldsymbol{\phi^TY -  \phi^T\phi w} - \lambda \boldsymbol{w = 0}$
solution for $\lambda > 0$: $\hat{\boldsymbol{w}}_\lambda = (\boldsymbol{\phi^T\phi} + \lambda \boldsymbol{I})^{-1} \boldsymbol{\phi^TY}$
prediction of $Y$ at $x$: $\hat{Y}=\boldsymbol{\hat{w}_\lambda^T \varphi(x)}$
<!--ID: 1691251771710-->



$RSS_\lambda(w) = \mid\mid \boldsymbol{Y-\phi w} \mid\mid^2 + \lambda w^Tw$, definujme $\boldsymbol{w = \phi^T \alpha}$, kde $\boldsymbol{\alpha} \in \mathbb{R}^N$. Jaká je (ne)rovnost mezi $\min RSS_\lambda(w)$ a $\min RSS_\lambda(\alpha)$? #flashcard 
$\min RSS_\lambda(w) \leq \min RSS_\lambda(\alpha)$, jelikož když používám $\alpha$, tak mám menší prostor než s $w$. 
Máme ale theorem, který říká, že jsou ta minima stejná a že se dají $w$ a $\alpha$ vzájemně pro to minimum převádět.
<!--ID: 1729010154050-->



# Jadrove metody, Jadrova Regrese,  Kernel Trick


Definuj pozitivne definitni, semi-definitivni, negativne .... a indefinitni matici #flashcard 
$\boldsymbol{A} \in \mathbb{R}^{n, n}$ is 
positive semi-definite: $x^TAx \geq 0, \forall x \in \mathbb{R}^{n, n}$
positive definite: $x^TAx \gt 0, \forall x \in \mathbb{R}^{n, n}$
negative definite: $x^TAx \lt 0, \forall x \in \mathbb{R}^{n, n}$
negative semi-definite: $x^TAx \leq 0, \forall x \in \mathbb{R}^{n, n}$
$A$ is indefinite $\iff \exists x, y \in \mathbb{R}^{n, n}, x^TAx \gt 0 \land y^TAy \lt 0$
<!--ID: 1729010154051-->



Define kernel function $k(x, y), k: \mathbb{R}^p \times \mathbb{R}^p \to \mathbb{R}$, define Gram matrix (ADM) #flashcard 
$k(\boldsymbol{x}, \boldsymbol{y}) = \boldsymbol{\varphi(x)^T}\boldsymbol{\varphi(y)}$, where $\boldsymbol{\varphi(x)} = (\varphi_1(\boldsymbol{x}), ..., \varphi_M(\boldsymbol{x}))^T$
Gram matrix: Given a kernel function $k$ and inputs $\boldsymbol{x}_1, . . . ,\boldsymbol{x}_n \in  \chi$, the $n \times n$ matrix $G = (G_{i,j})$, where $G_{i,j} = k(\boldsymbol{x}_i, \boldsymbol{x}_j)$
<!--ID: 1729010154052-->



Formulate the linear model for regression and classification in terms of a dual representation - kernel trick + Gram matrix. Using the kernel trick, the basis functions are then given implicitly. #flashcard 
$RSS_\lambda(\alpha) = \mid\mid Y-G\alpha \mid\mid^2 + \lambda\alpha^TG\alpha$, where $G_{i, j}=k(x_i, x_j)$
Minimiser for $\lambda > 0$ is given: $\hat{\alpha}=(G+\lambda I)^{-1}Y$
Prediction of $Y$ at $x$ is: $\hat{Y}=\sum^N_{x=1}\hat{\alpha}_ik(x_i, x)=\hat{\alpha}^Tk(x)$
* input vector $x$ enters only in the form of scalar products
* The replacement of scalar products with a kernel function is known as the kernel trick
* Now the natural extension is to start with a kernel without specifying the basis functions explicitly (allows us to use feature spaces of high, even infinite, dimensionality)
<!--ID: 1729010154053-->



Write examples of kernels used in linear models (ADM) #flashcard 
* **Linear kernel**: $k(x, y)=x^Ty$
* **Polynomial kernel**: $k(x, y)=(x^Ty+1)^n$
* **RBF kernel**: $k(\boldsymbol{x}, \boldsymbol{y})=\mathrm{e}^{-\frac{\|x-y\|^2}{2 \sigma^2}}$
* Kernel for comparing documents: $k\left(\boldsymbol{x}_i, \boldsymbol{x}_j\right)=\frac{\boldsymbol{x}_i^T \boldsymbol{x}_j}{\left\|\boldsymbol{x}_i\right\|\left\|\boldsymbol{x}_j\right\|}$
<!--ID: 1729010154054-->



What are kernel machines, vector machines and sparse vector machines? (ADM) #flashcard 
Kernel machine is model $f(x)=\sum^K_{j=1}\alpha_jk(x, \mu_j)$, where $\mu_1, ... \mu_K \in \chi$ are some centers
Kernel machines corresponds to linear basis expansion with $\varphi_j(\cdot)=k(\cdot, \mu_j)$
Vector machines are special case of Kernel machines $f(x)=\sum^K_{j=1}\alpha_jk(x, x_j)$
Sparse vector machines are vector machines where $\alpha_j = 0$ for many points
<!--ID: 1729010154055-->



# Support Vector Machine (SVM): separabilní a neseparabilní případ

Popiš **SVM** - lineárně separabilní případ #flashcard 
* **Discriminant function**: bod lze rozdělit na 2 vektory. Jeden je paralelní a druhý kolmý s decision boundary. Kolmý vektor je úměrný vzdálenosti bodu od hranice. Bodům přidělíme znaménko v závislosti na jaké straně od hranice jsou.
Vzdalenost i-teho bodu $\varphi(x_i)$ je $r_i=\frac{f(x_i)}{\mid\mid w \mid\mid}$. Hledáme tudíž:
$$\max_{w, w_0} \min_i \frac{Y_i(w^T\varphi(x_i)+w_0)}{\mid\mid w \mid\mid} \propto \min_i\frac{1}{\mid\mid w \mid\mid}$$
Řešíme ekvivalentní problém $\min_{w, w_0} \frac{1}{2}\mid\mid w\mid\mid^2 \text{ subject to } Y_i(w^T\varphi(x_i)+w_0)\geq 1 \text{ for all } i$
<!--ID: 1729010154056-->



Popiš **SVM** - lineárně neseparabilní případ #flashcard 
Řešení, kde $Y_i(w^T\varphi(x_i)+w_0)\geq 1$ neexistuje, proto relaxujeme a penalizujeme body na špatné straně. $\xi_i= \mid Y_i - f(x_i)\mid \text{ (for the wrong side) } 0 \text{ otherwise}$
Pak optimalizujeme: $\mid_{w, w_0, \xi} \frac{1}{2} \mid\mid w\mid\mid^2 + C\sum^N_{i=1}\xi_i$
<!--ID: 1729010154057-->




# Algoritmy pro doporučování

## základní přístupy a způsob vyhodnocení kvality

Algoritmy pro doporučování se dělí do různých kategorií. Podle čeho se dá dělit a jaké jsou kategorie? #flashcard 
**Podle typu úlohy**: item2user, user2item, item2item, user2user
**Podle interakcí**:
- Explicitní - uživatel ohodnotil 5*
- Implicitní - uživatel shlédl 80% videa
**Podle atributů**: uživatele-(gender, age, ...), itemu-(popis, metadata, ...)
**Podle typu filtrování**: kolaborativní, content-based
<!--ID: 1729010154058-->



Jaký je základní princip reccommenderů co používají kolaborativní/content-based doporučování? #flashcard 
**Kolaborativní**: A a B si oblíbí knihu K1. Druhý den si B oblíbí knihu K2. Uživateli A doporučíme knihu K2.
* Hledáme relace mezi uživateli/skupinami na základě jejich chování. Předpokládáme, že se všem líbí podobné věci.
**Content-based**: A se líbí kniha žánfu drama. Doporučíme mu drama co ještě nečetl.
* Doporučujeme na základě obsahu. Podobný, ale jiný item.
<!--ID: 1729010154059-->



Jaké jsou metriky pro vyhodnocení doporučovacích systémů? #flashcard 
**Similarity metrics**: Cosine similarity, Jaccard similarity
**Predictive metrics**: MAE, RMSE ... 
**Classification**: Presicion@K, Recall@K, HitRatio@K
**Ranking**: MAP@K
<!--ID: 1729010154060-->



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
<!--ID: 1729010154061-->



## faktorizační metody pro doporučování

Jaká je hlavní myšlenka maticové faktorizace u doporučovacích algoritmů? #flashcard 
Recommender matrix: $m\times n$ matice, s $m$ users a $n$ items. Hodnoty jsou hodnocení itemu userem. Cílem je předpovědět chybějící hodnoty.
Faktorizací rozumíme nějaký netriviální rozklad typu: $R=UV^T$
Základní myšlenka se dá vyjádřit jako: Pro matici $R$, najdi matice nižší dimenze $U$ a $V$ tak, aby hodnoty v R byly dobře aproximovány maticí $UV^T$
<!--ID: 1729010154062-->



Jak formulujeme optimalizační úlohu maticové faktorizace pro doporučovací algoritmy. #flashcard 
Hledáme rozklad matice $R\in \mathbb{R}^{m\times n}$  na netriviální matice nižší dimenze tak aby platilo $R=UV^T$.  kde $U\in \mathbb{R}^{m\times d}, V\in \mathbb{R}^{n\times d}$
Optimalizační kritérium: 
$$
\operatorname{argmin}_{\mathbf{U}, \mathbf{v}} \sum_{(i, j) \in \Omega}\left(r_{i, j}-u_i^T v_j\right)^2+\lambda\left(\sum_x\left\|u_x\right\|^2+\sum_y\left\|v_y\right\|^2\right)
$$
kde $\lambda > 0$ je regularizace, $d$ pozitivní celé číslo udávající dimenzi. (výrazně menší než m, n)
Rate of error: $\left(r_{i, j}-u_i^T v_j\right)^2$
<!--ID: 1729010154063-->




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
<!--ID: 1729010154064-->



