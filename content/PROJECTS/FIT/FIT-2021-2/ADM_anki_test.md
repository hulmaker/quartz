TARGET DECK: ADM_test
FILE TAGS: ADM ADM_test

# asdf

Co je za vlastnost generalizace modelu? #flashcard 
Schopnost dobrého fungování na datech co nikdy neviděl.
<!--ID: 1613660364226-->


definuj categorical cross-entropy error a k čemu je? #flashcard 
$$\hat{p}(x)=\hat{\mathrm{P}}(Y=1 \mid X=x)$$
$$L(Y, \hat{p}(x))=-\sum_{j=1}^{c} \mathbb{1}_{Y=j} \log \hat{p}_{j}(x)=-\log \hat{p}_{Y}(x)$$
Ztrátová funkce pro úlohu klasifikace. Penalizuje velké chyby víc, než ty malé.
Tahle loss je jen přes jedno dato! (je to dementní, někde říkají tomuhle error, jinde je error přes celou test množinu, někde to je running loss atd.)
$\mathbb{1}_{Y=j}=\left\{\begin{array}{ll}1 & \text { if } Y=j \\ 0 & \text { otherwise }\end{array}\right.$
<!--ID: 1613660364232-->


co penalizuje jinak MSE oproti MAE? #flashcard 
MSE penalizuje velke chyby mnohem vice nez MAE. MSE vede k tomu, že je ok se plést málo, ale není ok se plést hodně. MAE vede k tomu, že je přesnější, ale sem tam udělá velkou chybu.
<!--ID: 1613660364238-->


Najde gradientní sestup globální minimum? #flashcard 
Skoro nikdy, najde většinou jen lokální. (který je docela blízko tomu globálnímu.)
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


Definuj Mathews correlation coefficient a řekni k čemu je #flashcard 
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
Bootstrap odhaduje taky expected test error.
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


Popiš kdy využiješ negative correlation learning a jak to uděláš #flashcard 
[gbrown o tom ma disertacku](http://www.cs.man.ac.uk/~gbrown/)
Když mám ensamble learning a dělám bias variance decomposition, tak jejich chyby spolu nějak korelují. My chceme snižovat složku chyby, co vzniká korelací modelů.
Toto je regularizační člen: $R=p_{i}=\left(f_{i}-\bar{f}\right) \sum_{j \neq i}\left(f_{j}-\bar{f}\right)$
mám model i a j. Pokud se budou oba oproti průměru vychylovat na stejnou stranu, tak je to špatný a jsou korelovaný. A tudíž dávám chybě na té straně větší váhu a tudíž průměr bude vychýlen k nim.
Negative correlation learning je to, že k chybě weak learners přidám regularizační člen pronásobený váhou a ten mi zajistí to, že jednotlivý learners "propojím" se zbytkem.
<!--ID: 1616260958885-->

## test

definice entropie #flashcard 
$H(D) = - \sum^{c}_{i=1} p_i\ log\ p_i$, kde $c$ jsou třídy a $p_i$ je pravděpodobnost, že příznak náleží třídě $i$
<!--ID: 1620222980063-->


definuj IG v ID3 algoritmu #flashcard 
IG = information gain. jedno z kritérií, podle kterého se dají dělit data při konstrukci rozhodovacího stromu
$IG(D, X_i) = H(D) - t_0H(D) - t_1H(D)$
kde $D_0$ a $D_1$ jsou podmnožiny dat $D$, pro které $X_i = 0$ resp. $X_i = 1$, a $t_i$ je podíl počtu prvků v $D_i$ a $D$ , neboli $t_i = \frac{|D_i|}{|D|}$.
<!--ID: 1620222980069-->


Derivace kolikátého řádu musí existovat pro ztratu XGBoost? #flashcard 
Druhého. Pro gradient boosting stačí jen první, ale XGBoost potřebuje i druhou.
<!--ID: 1620222980074-->


Definuj binary cross entropy loss #flashcard 
$L(Y, \hat{p}(\boldsymbol{x}))=-Y \log \hat{p}(\boldsymbol{x})-(1-Y) \log (1-\hat{p}(\boldsymbol{x}))$
<!--ID: 1620222980078-->


Define training loss. #flashcard 
During the training of a model with fixed hyperparameters, one minimizes a training loss, which is the mean of the loss function over a training sample.
$\mathcal{L}=\frac{1}{N} \sum_{i=1}^{N} L\left(Y_{i}, \hat{Y}_{i}\left(\boldsymbol{x}_{i}\right)\right)$
<!--ID: 1620222980083-->


Jaký nejjednodušší model bychom museli mít, aby naše ROC byla diagonála? tj $TPR \approx FPR$ #flashcard 
Model co vrací random prediction.
<!--ID: 1620222980087-->


Co uděláme, když bude naše ROC křivka pod diagonálou? #flashcard 
Skočíme z okna, nebo půjdem pracovat do mekáče. Pod diagonálou je náš model horší jak random predikce.
<!--ID: 1620222980091-->


Definuj RSS a TSS #flashcard 
RSS - residual sum of squares
TSS - total sum of squares
$\mathrm{RSS}=\sum_{i=1}^{N}\left(Y_{i}-\hat{Y}_{i}\right)^{2}\quad$
$\quad \mathrm{TSS}=\sum_{i=1}^{N}\left(Y_{i}-\bar{Y}\right)^{2}$
<!--ID: 1620222980095-->


Definuj coefficient of determination a řekni k čemu je #flashcard 
[wiki](https://en.wikipedia.org/wiki/Coefficient_of_determination), measures how the squared error differs from the squared error of the trivial model predicting by mean,
Jak se liší kvadratická chyba našecho modelu od kvadratické chyby modelu, který predikuje průměrem hodnot.
$R^2 = 1 - \frac{RSS}{TSS}$,
RSS - residual sum of squares
TSS - total sum of squares
<!--ID: 1620222980099-->


Dej orientační představu, jak velké $k$ se typicky volí v $k$-fold cross validaci. Aspoň řádově. #flashcard 
Většinou se k pohybuje okolo 5 a 10. Výjimkou je leave-one-out cross-validation, kde je k rovno velikosti testovacího datasetu.
<!--ID: 1620222980104-->


Jaký rozdíl je mezi test error a expected test error? Jak je získám? #flashcard 
**Test error** měří chybu modelu na testovacím datasetu. 
**Expected test error** je střední hodnota test erroru na všech možných testovacích datasetech.
Cross-validation by se k expected test error měla blížit více. Pokaždé ale máme jen odhad expected test error.
**Pozn. 1** Cross validace (stejně jako bootstrap) dává spíš chybu procesu trénování modelu a ne chybu toho modelu. Jelikož pokaždé trénujeme znova.
Tím ale nezískáme test error, ale odhad expected test error. Je to chyba, kterou budeme očekávat jako výsledek toho trénovacího procesu a ne přímo toho konkrétního modelu. Jelikož je to mean jednotlivých měření chyby na modelu natrénovaném odznova.
**Pozn. 2** - měření test error na validačních datech a nebo odhadování expected test error v cross validaci je obojí odhad expected test error, jen cross-validace bude pravděpodobně lepší odhad.
<!--ID: 1620222980108-->


Co je hold-out strategy? #flashcard 
Rozdělení datasetu na dvě části - trénovací a validační. Nejlepší hyperparametry modelu jsou vybrány podle úspěšnosti na validační části.
Pozn. Abychom změřili performance modelu, musíme mít ještě testovací data, jelikož měřit to na validačních je biased.
<!--ID: 1620222980112-->

Definuj logistickou regresi pro binární klasifikaci #flashcard 
$y = f(w^Tx = w_0 + w_1x_1 + ... + w_px_p) = f(w^Tx)$, kde funkce $f$ je sigmoida. $w$ je vektor vah, $w_0$ je intercept/bias a $x$ je vektor vstupů.
$P(Y=1|x, w) = \frac{e^{w^Tx}}{1+e^{w^Tx}}$
<!--ID: 1620252081412-->


Napiš předpis pro sigmoidu, načrtni jí, najdi $D_f$ a $H_f$, limity v nekonečnech a nějaké zajímavé body #flashcard 
$f(x) = \frac{e^x}{1+e^x} = \frac{1}{1+e^{-x}}$
$D_f = \mathbb{R}, H_f = (0, 1)$
$\lim{x \to +\infty} f(x) = 1$
$\lim{x \to -\infty} f(x) = 0$
$f(0) = 0.5$
<!--ID: 1620252081417-->


Definuj obdobu sigmoidy pro vícetřídní klasifikaci #flashcard 
[Softmax function](https://en.wikipedia.org/wiki/Softmax_function)
$\sigma(\mathbf{z})_{i}=\frac{e^{z_{i}}}{\sum_{j=1}^{K} e^{z_{j}}}$
<!--ID: 1620252081421-->


Popiš MLE princip pro váhy $w$ v log. regresi pro bin. klasifikaci. #flashcard 
Hledáme $w$ takové, aby pravděpodobnost, že nastala naše trénovací data byla maximální. To změříme pomocí likelihood funkce.
$P_1(x, w) = \frac{e^{w^Tx}}{1+e^{w^Tx}}$
$P_0(x, w) = 1 - P_1(x, w)$
Předpokládáme, že jsou jednotlivé datové body nezávislé. Potom $L(w) = \prod_{i=1}^N P_{yi}(x_i, w)$, kde $L(w)$ je likelihood function.
To najdeme tak, že zderivujeme $L(w)$, ale derivovat součin je kencur, tak derivujeme $l(w) = log L(w) = \sum log P_{yi}(x_i, w)$ (log zachovává extrémy), pak najdu gradient atd.
**Pozn.** $l(w)$ je to samý, jako cross entropy, ale s opačným znamínkem
<!--ID: 1620252081425-->


Kullback-Leiblerova divergence #flashcard 
$D_{KL}(P||Q) = \mathbb{E_p}(log \frac{P}{Q}) = \int_{x\in X} p(x)\ log \frac{p(x)}{q(x)}\ dx =$
$= \int_x p(x)\ log\ p(x)\ dx - \int_x p(x)\ log\ q(x)\ dx = H(P, Q) - H(P)$,  
kde $H(P)$ je entropie a $H(P, Q)$ je cross-entropie
<!--ID: 1620252081430-->


Popiš, proč minimalizovat Kullback-Leiblerovu divergenci je stejný, jako minimalizovat cross-entropii #flashcard 
$D_{KL}(P||Q) = \mathbb{E_p}(log \frac{P}{Q}) = H(P, Q) - H(P)$
Při minimalizaci chceme, aby distribuce Q byla podobná P. Pokud je $H(P, Q)$ minimální, tak $P$ a $Q$ jsou stejná distribuce a platí $H(P, Q) = H(P) = H(Q)$. Minimalizovat divergenci je stejné, jako minimalizovat cross entropii. Protože $H(P)$ je konstanta! A my jí tam máme částečně proto, minimum ztráty bylo nula. 
<!--ID: 1620252081434-->


Řekni distribuce čeho v Kullback-Liebrově divergenci používáme a jak je získáme. #flashcard 
Chceme $D_{KL}(P_{skutečnost}||Q_{model})$, ale distribuci skutečnosti nemáme, musíme si skutečnost odhadnout pomocí empirické hustoty z dat $D_{KL}(P_{data}||Q_{model})$
Je to MLE přístup.
<!--ID: 1620252081438-->

Definuj Dirac delta function #flashcard 
$\delta(x) = 1 \iff x = 0$
$\delta(x) = 0 \iff x \neq 0$
$\int_{\mathbb{R}}\delta(x)\ dx = 1$
Je to v podstatě Gaussovka, kde jsme rozptyl poslali k nule.
<!--ID: 1620252081442-->


Co je empirická distribuční funkce (nebo empirická hustota)? #flashcard 
Distribuční funkci můžeme odhadnout pomocí empirické distribuční funkce.  $P(X \leq x)$ můžeme odhadnout jako podíl pozorovaných dat, která jsou menší nebo rovná x. 
Empirická hustota je v podstatě histogram. Abychom ale dodrželi že se integruje na jedničku, tak musíme použít Dirac delta function aby integrál byl 1.
$P_{data} = \sum_{i=1}^N \frac{1}{N} \delta(x - x_i, y -y_i)$ -> to se započítá pouze pokud $x=x_i$ a $y=y_i$ kvůli vlastnostem Diracovo delta.
<!--ID: 1620252081445-->

Jak dobře funguje accuracy na nevybalancovaném datasetu? #flashcard 
špatně, nebere ho vůbec v potaz. Klasifikátor rozhodující jestli je člověk terorista, může říct pro jakýkoliv vstup, že čověk terorista není a bude mít fakt hodně vysokou accuracy.
<!--ID: 1620254756699-->


Přepiš TPR, FPR na pravděpodobnostní značení #flashcard 
$TPR = TP/(TP+FN) \approx P(\hat{Y}=1 | Y=1)$
$FPR = FP/(FP+TN) \approx P(\hat{Y}=1 | Y=0)$
<!--ID: 1620254756704-->


Co musí model splnit, aby měl AUC=1 #flashcard 
Existuje nějaký threshold, co data perfektně separuje.
Což ještě neznamená, že je náš model naprosto dokonale mega užasný.
<!--ID: 1620254756708-->

Je model, co má AUC=0 špatný model? #flashcard 
Pro model co má AUC=0 platí, že existuje threshold, při kterém zvládne odseparovat data perfektně špatně. Což znamená, že kdybychom při binární klasifikaci obrátili třídu, tak je AUC=1. 
Je tedy špatný? Z inženýrského hlediska vlastně ne. 
Z matematického hlediska ano, ale z toho není ani zaručeno, že model bude dobrý s AUC=1
<!--ID: 1620909090763-->


Dej příklad modelu, co má AUC=1 a má nějaké špatné vlastnosti. (třeba funguje dobře, ale predikce jsou podezřelé atd) #flashcard 
Existuje pro něj nějaký threshold, co dokáže perfektně separovat data. Může ale pro ta data dávat pravděpodobnosti, co jsou úplně hrozně moc blízko sebe, nebo může hodně podstřelit, že ten threshold bude např. 0.01. 
Je potom diskutabilní, jestli je to dobré pro model co modeluje pravděpodobnost.
<!--ID: 1620254756713-->
