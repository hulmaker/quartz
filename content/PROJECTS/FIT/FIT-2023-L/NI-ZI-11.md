TARGET DECK: NI-ZI-2023::NI-ADM
FILE TAGS: NI-ZI-2023 NI-ZI-11 NI-ADM

prev::[[NI-ZI-10]]
next::[[NI-ZI-12]]
# Ensemble metody: rozdíl mezi základními metodami (např. Bagging, Boosting, XGBoost).

Co to jsou ensemble metody a jaké znáš? #flashcard 
Techniky, které vytváří vícero modelů podílejících se na predikci výsledků.
Bagging: Na náhodných podmnožinách dat natrénuj estimátory, jejichž predikce agregujeme do finální predikce
* Random Forests
Boosting: Datovým bodům přiřazujeme významnost.
* AdaBoost: Kaskády N weak learners, konstruováno postupně, agregace: hlasování/průměr
* GradientBoosting: (XGBoost): Zobecnění boostingu pro libovolnou derivovatelnou ztrátu.
Jako klasifikátory se typicky používaljí stromy, ale lze se setkat i s modely jako kNN atd.
<!--ID: 1691578042067-->



definuj information gain v ID3 algoritmu #flashcard 
IG = information gain. jedno z kritérií, podle kterého se dají dělit data při konstrukci rozhodovacího stromu
$IG(D, X_i) = H(D) - t_0H(D) - t_1H(D)$
kde $D_0$ a $D_1$ jsou podmnožiny dat $D$, pro které $X_i = 0$ resp. $X_i = 1$, a $t_i$ je podíl počtu prvků v $D_i$ a $D$ , neboli $t_i = \frac{|D_i|}{|D|}$.
<!--ID: 1691578042071-->



Derivace kolikátého řádu musí existovat pro ztrátu v XGBoost? #flashcard 
Druhého. Pro gradient boosting stačí jen první, ale XGBoost potřebuje i druhou.
<!--ID: 1691578042074-->



Ensemble metody - Bagging (v obecnosti) #flashcard 
Bootstrap Aggregating (bagging):
1. sampling with replacement to allow for variation
2. training a model on each subset: decision tree, neural network, kNN, ...
3. Aggregating predictions: average, mode, voting ...
Větší stabilita predikcí, menší overfitting, vyšší složitost algoritmu, náchylné na bias
<!--ID: 1691578042077-->



Ensemble metody - Boosting (v obecnosti) #flashcard 
* Iterativní trénování na jednom datasetu se zaměřením na problémové datové body.
* Kombinuje vícero weak learners a pomocí agregace predikuje finální výsledek
* vyšší složitost, snadný overfitting, větší variance, nižší bias
* modely: 1-2 úrovňové stromy, naive Bayes, kNN
<!--ID: 1691578042079-->



Ensemble metody - AdaBoost #flashcard 
Kaskády weak learners, iterativní učení, těžké datové body mají vyšší váhu, výsledná predikce je vážená kombinace slabých predikcí.
Amount of say (classifier weight $\propto$ accuracy): $\alpha_i=\frac{1}{2} \log _2 \frac{1-\text { error }_i}{\text { error }_i}$
Final sample weights are summarized over all predictions and normalized:
* Correct classified weight: $\bar{w}_j^{i+1}=w_j^i e^{-\alpha_i}$
* Missclassified weight: $\bar{w}_j^{i+1}=w_j^i e^{\alpha_i}$
<!--ID: 1691578042081-->



Ensemble metody - GradientBoosting #flashcard 
[yt](https://youtu.be/3CC4N4z3GJc), [lecture 1](https://courses.fit.cvut.cz/NI-ADM/@B212/lectures/index.html), [lecture notes](https://courses.fit.cvut.cz/NI-ADM/@B212/lectures/files/NI-ADM-03-04-notes.pdf)
N weak learners, iterativní učení, výsledná predikce je vážená kombinace slabých predikcí
Loss musí mít druhou derivaci (Taylorův polynom)
XGBoost:
* objective function odvozujeme obecně pro libovolnou derivovatelnou loss
* Musíme se jen rozhodnout, jaký podstrom budeme dál větvit. To je NP-hard
* Proto používáme greedy alg jako v ID3
* Greedy alg. dělí strom na L a R podle Gain
* Gain je odvozený od druhého Taylora objective function
* Gain je něco jako krit(D)-krit(DL)-krit(DR)
<!--ID: 1691578042082-->


XGBoost - ztrátová funkce, předpis výrazu co chceme minimalizovat #flashcard 
$$
\sum_{i=1}^N \ell\left(y_i, \hat{y}_i^{(t)}+f_{t+1}\left(\mathbf{x}_i\right)\right)+\Omega\left(f_{t+1}\right)
$$
kde $\ell$ je loss, $f_{t+1}$ je podstrom, predikce $\hat{y}^{(t)}_i = F^{(n)}(x_i) = \sum_{i=0}^t f_i(x_i)$ a $\Omega$ je regularizace.
Tenhle výraz může být těžký minimalizovat, tak ho aproximujeme teylorem druhého řádu.
<!--ID: 1692373428996-->
