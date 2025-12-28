TARGET DECK: PON-TEST
FILE TAGS: PON PON-TEST

# test

lineární obal souboru vektorů #flashcard
množina všech lineárních kombinací ze souboru
<!--ID: 1619440410002-->



přepiš sumu na maticové značení $$\sum_{i=1}^{N}\left(Y_{i}-w^{T} x_{i}\right)^{2}$$ #flashcard 
$$\|Y-\mathbf{X} w\|^{2}$$
<!--ID: 1619440544333-->




kdy je vektor ortogonální na podprostor #flashcard 
Když je vektor kolmý na podprostor (sloupce matice co ho definuje)
<!--ID: 1619440544339-->



$$v, u \in \mathbb{R}^{p+1}$$ jsou ortogonální právě když #flashcard 
jejich skalární součin je nula $$v^{T}u = 0 = v_0 u_0 + ... + v_p u_p$$
<!--ID: 1619440544347-->



ortonormální matice #flashcard 
sloupce i řádky jsou ortogonální (vzájemně kolmé) a jsou znormovány na jedničku. Je čtvercová.
<!--ID: 1619440544352-->




$\mathbb{Q}$ je ortogonální. Co je výsledkem $\mathbb{Q}^T \mathbb{Q}$ a proč? #flashcard 
jednotková matice - protože dělám dot produkt ortogonálních vektorů = 0, pouze pro ientitu na diagonále to bude 1
<!--ID: 1619440544358-->




Jak získám inverzní matici k ortogonální matici $\mathbb{Q}$? #flashcard 
transponuju ji, jelikož $\mathbb{Q}^T \mathbb{Q} = \mathbb{E}$
<!--ID: 1619440544364-->




dokaž že $||\mathbb{Q}v||^2 = ||v||^2$, kde $\mathbb{Q}$ je ortogonalni #flashcard 
$$||\mathbb{Q}v||^2 = (\mathbb{Q} v)^T \mathbb{Q} v = v^T \mathbb{Q}^T \mathbb{Q} v = v^T \mathbb{E} v = v^T v = ||v||^2$$
<!--ID: 1619440544370-->




proč chceme používat co nejmíň GEM? #flashcard 
GEM je numericky hrozně pomalý, chceme se mu proto vyhnout. Proto je pro inverze nejlepší používat ortogonální matice.
<!--ID: 1619440544375-->


Dokaž, že když násobím víc ortogonálních matic, tak je výsledek taky ortogonální #flashcard 
$$(Q_1 Q_2)^T Q_2 Q_1 = Q_1^T Q_2^T Q_2 Q_1 = Q_1^T E Q_1 = E$$
<!--ID: 1619440544380-->




Popiš princip algoritmu pro QR rozklad. #flashcard 
![[QR_rozklad_princip.png]]
Využívám toho, že násobení ortogonálních matic je ortogonální matice a že její inverze je její transpozice. Pro každou pozici v R, kde má být nula vyrobím jednu ortogonální matici, kterou když vynásobím X, tak mi vyrobí v R nulu. Ty matice potom spolu pronásobím a transponuju.
Giwensovy rotace - pro každou pozici jedna matice (skoro jednotková)
Hausholdovy reflexe - pro každý sloupec jedna matice
<!--ID: 1619440544384-->




## Lec 03 - 02.03.2021

Popiš predikci lineární regrese. #flashcard
$$Y=w_{0}+w_{1} x_{1}+\ldots+w_{p} x_{p}+\varepsilon=\boldsymbol{w}^{T} \boldsymbol{x}+\varepsilon$$
kde $E\varepsilon = 0$, což implikuje $EY=\boldsymbol{w}^{T} \boldsymbol{x}$
<!--ID: 1619440544389-->



Popiš RSS v modelu lineární regrese. A řekni co to je #flashcard
$\operatorname{RSS}(\boldsymbol{w})=\sum_{i=1}^{N}\left(Y_{i}-\boldsymbol{w}^{T} \boldsymbol{x}_{i}\right)^{2}=\|\boldsymbol{Y}-\mathbf{X} \boldsymbol{w}\|^{2}$
Je to součet chyb přes všechny body pro kvadratickou ztrátovou funkci. Residuální součet čtverců.
<!--ID: 1619440544396-->




Popiš $\hat{\boldsymbol{w}}_{\mathrm{OLS}}$ v metodě nejmenších čtverců v LR. Dál řekni co musí platit pro matice co používáš. #flashcard 
$$\hat{\boldsymbol{w}}_{\mathrm{OLS}}=\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1} \mathbf{X}^{T} \boldsymbol{Y}$$
$\mathbf{X}^{T} \mathbf{X}$ je regulární, a tudíž můžeme získat její inverzi. Pokud není inverzní, dá se použít pseudoinverzní matice. Sloupce jsou LN. Pokud jsou LZ, nebo skoro LZ, musíme regularizovat pomocí L2 regularizace, což už je hřebenová regrese.
<!--ID: 1619440544401-->




Definuj idempotent matrix #flashcard 
matice pro kterou platí, že $\mathbf{X}^2 = \mathbf{X}$
<!--ID: 1619440544405-->




Definuj vlastní čísla #flashcard 
$\lambda \in \mathbb{C}$ je vlastní číslo operátoru $A \in L(V)$, právě když existuje $x \in V, x \neq \theta, tž, Ax=\lambda x$. x je pak vlastní vektor operátoru A příslušející vlastnímu číslu $\lambda$
<!--ID: 1619440544411-->



## Lec 05 - 16.03.2021 - Maticove faktorizace 1

$B, A, P$ jsou matice, dokaz, ze $B$ a $A$ maji stejna vlastni cisla pokud plati: $B=PAP^{-1}$ #flashcard 
![[det_eigenvals.png]]
<!--ID: 1619440544416-->




Kdy jsou si matice $A, B$ podobne? #flashcard 
Pokud existuje regulární $P \in \mathbb{C}^{n, n}$ takova, ze $A = P^{-1}BP$
1. A je podobná A,
2. pokud A je podobná B, pak B je podobná A,
3. pokud A je podobná B a B je podobná D, pak A je podobná D.
<!--ID: 1619440544421-->




Popis zakladni myslenku QR algoritmu #flashcard 
Je to algoritmus pro hledani vlastnich cisel. Idealne v hustych maticich. Jelikoz je to slozite, tak si to iteracnim rozkladanim zjednodusujeme. A to si muzeme dovolit diky tomu, ze podobne matice maji stejna vlastni cisla.
![[PROJECTS/FIT/FIT-2021-2/media/QR_algorithm.png]]
```python
Aiter = A,
for i in range(N):,
    Q, R = np.linalg.qr(Aiter)  # QR rozklad
    Aiter = R.matmul(Q)
assert set(np.linalg.eigvals(Aiter)) == set(np.linalg.eigvals(A))
```
<!--ID: 1619440544426-->



Dokaž, že jsou vlastní čísla symetrické matice z $\mathbb{R}$. #flashcard 
![[vl_sym_z_r.jpg]]
Alternativa: $x$ je vl. vektor
jelikož $(\mathbb{A}x, y) = (x, \mathbb{A} y)$, tak to jde i  takhle
$\lambda\|x\|^{2}=(x, \lambda x)=(x, \mathbb{A} x)=(\mathbb{A} x, x)=(\lambda x, x)=\bar{\lambda}\|x\|^{2}$
Z toho plyne $\bar{\lambda} = \lambda$. Jelikož $x \neq \theta, ||x||= neq 0$
<!--ID: 1619440544430-->



## Lec 06 - 30.03.2021 - Maticove faktorizace 3

Je pravda, že matice $A^TA$ a $AA^T$ jsou vždy symetrické? #flashcard 
ano
<!--ID: 1619440544434-->



Je pravda, že je každá symetrická matice diagonalizovatelná? #flashcard 
ano, je to pravda
<!--ID: 1619440544438-->



## TEST

Definuj vztah v modelu lineární regrese pro vysvětlovanou proměnnou $Y$ #flashcard 
$Y=w_{0}+\sum_{i=1}^{p} x_{i} w_{i}+\varepsilon$
$w_0$ - intercept
epsilon - náhodná veličina
maticove -> $Y=w^Yx+\varepsilon$
kdyz jsou $x^T$ ve sloupci, tak -> $Y=Xw+\varepsilon$
<!--ID: 1619440544443-->



jak odhadnout vahy $w$ v linearnim modelu? #flashcard 
Pomoci RSS - residualni soucet ctvercu
$\operatorname{RSS}(\boldsymbol{w})=\sum_{i=1}^{N}\left(Y_{i}-\boldsymbol{w}^{T} \boldsymbol{x}_{i}\right)^{2}=\|\boldsymbol{Y}-\mathbf{X} \boldsymbol{w}\|^{2}$
$\hat{w}=\underset{w \in \mathbb{R}^{p+1}}{argmin}RSS(w)$
<!--ID: 1619440544448-->



Odvoď normální rovnici v lineární regresi, vysvětli kroky. #flashcard 
$\frac{\partial \operatorname{RSS}}{\partial w_{j}}=\sum_{i=1}^{N} 2\left(Y_{i}-\boldsymbol{w}^{T} \boldsymbol{x}_{i}\right)\left(-x_{i ; j}\right)$
z toho odvodime gradient - pro vsechny j
$\nabla \mathrm{RSS}=-\sum_{i=1}^{N} 2\left(Y_{i}-\boldsymbol{w}^{T} \boldsymbol{x}_{i}\right) \boldsymbol{x}_{i}=-2 \mathbf{X}^{T}(\boldsymbol{Y}-\mathbf{X} \boldsymbol{w})$
A z toho mame normalni rovnici - polozime rovno nule.
$X^T - X^TXw=0$
<!--ID: 1619440544452-->



Dokaž, že je $\mathbf{H}_{\mathrm{RSS}}(\boldsymbol{w})=2 \mathbf{X}^{T} \mathbf{X}$ pozitivně semidefinitní. #flashcard 
$s^T(X^TX)s=(Xs)^T(Xs)=||Xs||^2 \geq 0$
<!--ID: 1619440544456-->



Odvoď, jak najdeš minimum RSS pomocí normální rovnice, kterou jsi odvodil v jiné flashcard #flashcard 
Potřevuju najít minimum $RSS$. K tomu mi postačí, aby byla hessova matice v bodě $x*$ pozitivně semidefinitní. 
Druhe parcialni derivace podle $w_j$
$\frac{\partial^{2} \operatorname{RSS}}{\partial w_{k} \partial w_{j}}=\sum_{i=1}^{N} 2\left(-x_{i ; k}\right)\left(-x_{i ; j}\right)$
Z toho mame Hessovu matici
$\mathbf{H}_{\mathrm{RSS}}(\boldsymbol{w})=2 \mathbf{X}^{T} \mathbf{X}$
V jiné flashcard jsme odvodili, že je vždy pozitivně definitní, tudíž je neostré lokální minimum v jakémkoliv bodě $w$, co řeší normální rovnici
<!--ID: 1619440544461-->



Odvoď $\hat{w}_{OLS}$ a dej mi předpis pro $\hat{Y}$ #flashcard 
Z normalni rovnice $X^TY - X^TXw=0$ získáme $\hat{w}_{OLS} = (X^TX)^{-1}X^TY$
no a odhad $\hat{Y} = \hat{w}^T_{OLS}x = x^T(X^TX)^{-1}X^TY$
<!--ID: 1619440544466-->



Dokaž, že odhad $\hat{w}$ získaný metodou nejmenších čtverců je za předpokladu $\mathbb{E}\varepsilon=0$ nestranný. #flashcard 
$\mathbb{E}\hat{w} = \mathbb{E}(X^TX)^{-1}X^TY = (X^TX)^{-1}X^T\mathbb{E}Y = (X^TX)^{-1}X^TXw=w$
takže platí, že $\mathbb{E}\hat{w}=w$
<!--ID: 1619440544470-->



Čemu je rovný $var\ \hat{w}$ v LR a za jakých předpokladů je tomu rovný? #flashcard 
pokud  platí $\mathbb{E}\varepsilon = 0$ a $var\ Y = \sigma^2I_N$
Důkaz: $X^TX$ je symetrická -> $(X^TX)^{-1}$ je také symetrická.
$\operatorname{var} \hat{\boldsymbol{w}}=\operatorname{var}\left(\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1} \mathbf{X}^{T} \boldsymbol{Y}\right)=\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1} \mathbf{X}^{T}(\operatorname{var} \boldsymbol{Y}) \mathbf{X}\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1}$
$=\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1} \mathbf{X}^{T}\left(\sigma^{2} \mathbf{I}_{N}\right) \mathbf{X}\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1}=\sigma^{2}\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1} \mathbf{X}^{T} \mathbf{X}\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1}=\sigma^{2}\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1}$
Hint: $var(BX) = B(var(X))B^T$
<!--ID: 1619440544474-->



Vlastnosti RSS: Označme $P = X(X^TX)^{-1}X^T$ -> dokaž, že je $P$ idepotentní #flashcard 
$\mathbf{P}^{2}=\mathbf{X}\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1} \mathbf{X}^{T} \mathbf{X}\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1} \mathbf{X}^{T}=\mathbf{X}\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1} \mathbf{X}^{T}=\mathbf{P}$
<!--ID: 1619440544480-->



Vlastnosti RSS: Označme $P = X(X^TX)^{-1}X^T$ -> dosaď $P$ do rovnice RSS a dokaž, že je $I_N - P$ idepotentní #flashcard 
Dosazení: $\operatorname{RSS}(\hat{\boldsymbol{w}})=\|\boldsymbol{Y}-\mathbf{X} \hat{\boldsymbol{w}}\|^{2}=\|\boldsymbol{Y}-\mathbf{P} \boldsymbol{Y}\|^{2}=\left\|\left(\mathbf{I}_{N}-\mathbf{P}\right) \boldsymbol{Y}\right\|^{2}$
Důkaz: $\left(\mathbf{I}_{N}-\mathbf{P}\right)^{2}=\mathbf{I}_{N}^{2}-\mathbf{I}_{N} \mathbf{P}-\mathbf{P I}_{N}+\mathbf{P}^{2}=\mathbf{I}_{N}-\mathbf{P}$
<!--ID: 1619440544484-->



Nechť $\mathbb{E}\varepsilon = 0$ a $var\ Y = \sigma^2I_N$. Potom urči, $s^2$ - nestranný odhad $\sigma^2$ #flashcard 
$s^2 = \frac{RSS(\hat{w})}{N-p-1}$, kde $N-p-1=Tr(I_N-P)$.
Důkaz: $\mathbb{E}RSS(\hat{w}) = \mathbb{E} Y^T(I_N-P)Y= ... =$ někam se dopočítáš, uděláš stopu. no seru na to...
<!--ID: 1619440544488-->


Co říká Gauss-Markov theorem? #flashcard 
Odhad $\hat{w}$ získaný metodou nejlepších čtverců je nejlepší nestranný odhad $\hat{w}$ lineární v $Y$. To znamená, že pro každé $c \in \mathbb{R}^N$ je $c^T\hat{w}$ nejlepší nestranný odhad $c^Tw$ lineární v $Y$, tj. $var(c^T\hat{w}) \leq var(d^TY)$ pro každé $d \in \mathbb{R}^N$, kde $d^TY$ je nestranný odhad $c^Tw$.
Dokazuje se to tak, že díky Lemma 1.4 víme, že $c^TX\hat{w}$ je nejlepší nestranný odhad $c^TXw$ v $Y$, tj. $var(c^TX\hat{w}) \leq var(d^TY)$
potom platí: $c^{T} \hat{w} = c^{T}\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1} \mathbf{X}^{T} \mathbf{X} \hat{w} = \left(c^{T}\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1} \mathbf{X}^{T}\right) \mathbf{X} \hat{w}$ Označíme $a=c^{T}\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1} \mathbf{X}^{T}$ Z lemma dostaneme, že $a^TX\hat{w}$ je nejlepší nestranný lin. v $Y$ odhad $a^TXw = \left(c^{T}\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1} \mathbf{X}^{T}\right) \mathbf{X} \hat{w} = c^Tw$
<!--ID: 1619440544492-->



Kdy jsou na sebe vektory $x, y$ kolmé? #flashcard 
pokud je jejich dot product = 0
$x^Ty = 0$
<!--ID: 1619440544497-->



kdy je matice ortogonální? #flashcard 
její sloupce jsou navzájem ortogonální. Tj. dot product libovolných dvou je roven nule
<!--ID: 1619440544501-->


Kdy je matice ortonormální? #flashcard 
je ortogonální a zároveň mají její sloupce normu = 1
$q_{i}^{T} q_{j}=\left\{\begin{array}{ll}0 & \text { pro } i \neq j \\ 1 & \text { pro } i=j\end{array}\right.$
<!--ID: 1619440544504-->



co platí pro soubor ortonormálních vektoru? #flashcard 
* jsou LN
* $||x+y||^2 = ||x||^2+||y||^2$
* xx = 1
<!--ID: 1619440544508-->




Kdy je matice A symetrická? #flashcard 
$A^T=A$
<!--ID: 1619440544513-->



Dej mi vlastnosti ortonormální matice $Q$ #flashcard 
$Q^TQ = I_n$
je-li $Q$ ctvercova, pak je $Q^T = Q^{-1}$
$Q^T$ je ortogonální
$Q_1Q_2...Q_n$ je OG
$(Q_1Q_2...Q_n)^TQ_1Q_2...Q_n=I_m$
$||Qx||^2=||x||^2$
<!--ID: 1619440544518-->



Dokaž, že pro OG matici $Q$ plati $||Qx||=||x||$ #flashcard 
$\|\mathbf{Q} x\|^{2}=(\mathbf{Q} x)^{T} \mathbf{Q} x=x^{T} \mathbf{Q}^{T} \mathbf{Q} x=x^{T} \boldsymbol{x}=\|\boldsymbol{x}\|^{2}$
<!--ID: 1619440544521-->



Dej předpis pro QR rozklad #flashcard 
$A = QR$
![[QR_rozklad.png]]
$\mathbf{A}=\mathbf{Q} \mathbf{R}=\left(\begin{array}{ll}\mathbf{Q}_{L} & \mathbf{Q}_{R}\end{array}\right)\left(\begin{array}{c}\mathbf{R}_{S} \\ \Theta\end{array}\right)$
<!--ID: 1619440544525-->



Definuj dimenzi vektorového prostoru $V$ nad tělesem $T$ #flashcard 
$V$ má dim $n$, pokud ve $V$ existuje LN soubor délky $n$, ale každý $n+1$ dlouhý soubor už je LZ
$dim\ V = len(\text{největší LN soubor z V})$
<!--ID: 1619440544529-->


Definuj hodnost matice $\mathbb{A}$ #flashcard 
dimenze lineárního obalu souboru řádků: $h(\mathbb{A}) = dim\ <\mathbb{A}_{1:}, ..., \mathbb{A}_{m:}>$
Kde dimenze vektorového prostoru $V$ je $n$, pokud ve $V$ existuje LN soubor délky $n$, ale každý $n+1$ dlouhý soubor už je LZ
$dim\ V = len(\text{největší LN soubor z V})$
<!--ID: 1619440544534-->



Dokaž, že $\widehat{\boldsymbol{w}}_{\mathrm{OLS}}=\underset{\boldsymbol{w} \in \mathbb{R}^{p+1}}{\operatorname{argmin}}\|\mathbf{X} \boldsymbol{w}-\boldsymbol{Y}\|=\underset{\boldsymbol{w} \in \mathbb{R}^{p+1}}{\operatorname{argmin}}\left\|\mathbf{R}_{S} \boldsymbol{w}-\mathbf{Q}_{L}^{T} \boldsymbol{Y}\right\|$ #flashcard 
$\mathbf{Q} \mathbf{R}=\left(\begin{array}{ll}\mathbf{Q}_{L} & \mathbf{Q}_{R}\end{array}\right)\left(\begin{array}{c}\mathbf{R}_{S} \\ \Theta\end{array}\right)$
$\|\mathbf{X} \boldsymbol{w}-\boldsymbol{Y}\|^{2}=\|\mathrm{QR} w-\boldsymbol{Y}\|^{2}=\left\|\mathbf{Q}^{T}(\mathbf{Q R} \boldsymbol{w}-\boldsymbol{Y})\right\|^{2}=\left\|\mathbf{R} \boldsymbol{w}-\mathbf{Q}^{T} \boldsymbol{Y}\right\|^{2}$
Násobení OG maticí nemění normu
$= \left\|\left(\begin{array}{c}\mathbf{R}_{S} \boldsymbol{w} \\ \theta\end{array}\right)-\left(\begin{array}{c}\mathbf{Q}_{L}^{T} \boldsymbol{Y} \\ \mathbf{Q}_{R}^{T} \boldsymbol{Y}\end{array}\right)\right\|^{2}=\left\|\left(\begin{array}{c}\mathbf{R}_{S} \boldsymbol{w}-\mathbf{Q}_{L}^{T} \boldsymbol{Y} \\ -\mathbf{Q}_{R}^{T} \boldsymbol{Y}\end{array}\right)\right\|^{2}$
$= \left\|\mathbf{R}_{S} \boldsymbol{w}-\mathbf{Q}_{L}^{T} \boldsymbol{Y}\right\|^{2}+\left\|\mathbf{Q}_{R}^{T} \boldsymbol{Y}\right\|^{2}$
No a jelikož na $w$ závisí jenom ten první sčítanec, tak nás vlastně ten druhý nezajímá. Tudíž máme dokázáno. No a navíc je to stejně jedno, jelikož $QR = Q_LR_S$
<!--ID: 1619440544538-->



Definuj singulární matici #flashcard 
Matice $A \in T^{n, n}$ je regulární, existuje-li $B \in T^{n, n}$ taková, že platí: $AB=BA=E$. Potom $B$ je inverze k $A$ a značíme ji $A^{-1}$. Pokud $A$ není regulární, je **singulární**.
**Věta 6.27 (BI-LIN).** Matice $A \in T^{n, n}$ je regulární, právě když má nenulový determinant. (pokud by byl nulový, musela by mít LZ řádky/sloupce)
<!--ID: 1619440544542-->



Definuj determinant matice #flashcard 
Determinant nám (mimo jiné) určuje scaling faktor, podle kterého nám lineární transformace v podobě matice mění plochu. [3b1b](https://www.youtube.com/watch?v=Ip3X9LOh2dk)
* [Leibniz formula](https://en.wikipedia.org/wiki/Leibniz_formula_for_determinants):
$\operatorname{det}(A)=\sum_{\sigma \in S_{n}}\left(\operatorname{sgn}(\sigma) \prod_{i=1}^{n} a_{i, \sigma_{i}}\right)$, kde $A \in T^{n, n}$
$\sigma$ je permutace (bijekce), množina $S_n$ obsahuje všechny permutace n. A $\operatorname{sgn}(\sigma)$ značí počet inverzí v permutaci (kolik je dvojic takových, že je malé číslo za velkým číslem)
* [Laplace expansion](https://en.wikipedia.org/wiki/Laplace_expansion):
Věta o rozvoji determinantu podle *k*tého sloupce.
$\operatorname{det} \mathbb{A}=\sum_{i=1}^{n}(-1)^{i+k} a_{i k} \operatorname{det} \mathbb{A}(i, k)$, kde $A \in T^{n, n}$ a matice $A(k, l)$ vznikne z matice $A$ vynecháním *k*tého řádku a *l*tého sloupce
* Přes horní trojúhelníkový tvar: zGEMuj A na horní troj. tvar a determinant je potom produkt prvků na diagonále.
<!--ID: 1619440544546-->



Jak rychle spočítám determinant matice v horním trojúhelníkovém tvaru? #flashcard 
$\operatorname{det} \mathbb{A}=\prod_{i=1}^{n} \mathbb{A}_{i i}$
<!--ID: 1619440544550-->



Matice A je čtvercová. Jaké vlastnosti má její determinant? Jaké vlastnosti bude mít, pokud je navíc A regulární? #flashcard
$det(A) = det(A^T)$
$B$ je taky čtvercová, $det(AB) = det(A)det(B)$
Pokud je $A$ navíc regulární, tak platí:
$det(A^{-1})=\frac{1}{det(A)}$
<!--ID: 1619440544554-->


Dokaž, že $\lambda$ je vlastní číslo matice $A$, právě když $det(A - \lambda I) = 0$ #flashcard 
$x$ je vlastni vektor od vlastního čísla $\lambda$
$Ax = \lambda x \iff Ax = \lambda I x \iff (A-\lambda I)x=\theta \iff A-\lambda I \text{ je singulární} \iff det(A - \lambda I) = 0$
Pozn. $(A-\lambda I)x=\theta \iff A-\lambda I \text{ je singulární}$ (platí, jelikož $x \neq \theta$)
<!--ID: 1619440544558-->



Jak spočítáš vlastní čísla matice A? #flashcard 
$p_A(\lambda) := det(A-\lambda I)$ je charakteristický polynom operátoru $A$
Kořeny polynomu jsou vlastní čísla operátoru $A$. Násobnost kořene polynomu označujeme jako algebraickou násobnost vlastního čísla.
<!--ID: 1619440544562-->



Máš vlastní čisla matice A. Řekni, jak z nich získáš vlastní vektory. A geometrickou násobnost #flashcard 
$Ax = \lambda x \iff Ax = \lambda I x \iff (A-\lambda I)x=\theta$
pro všechna vlastní čísla $\lambda$ vyřešíš rovnici $(A-\lambda I)x=\theta$
Tahle rovnice má podprostor, který má dimenzi $n-h(A-\lambda I)$ - tomu číslu říkáme geometrická násobnost vlastního čísla $\lambda$
<!--ID: 1619440544565-->



Dokaž, že mají 2 podobné matice A, B stejná vlastní čísla #flashcard 
Podobné matice mají stejný charakteristický polynom. A tudíž i stejná vlastní čísla.
$\begin{aligned} p_{\mathbf{A}}(\lambda) &=\operatorname{det}(\mathbf{A}-\lambda \mathbf{I})=\operatorname{det}\left(\mathbf{P} \mathbf{B} \mathbf{P}^{-1}-\lambda \mathbf{P} \mathbf{P}^{-1}\right) \\ &=\operatorname{det}\left(\mathbf{P}(\mathbf{B}-\lambda \mathbf{I}) \mathbf{P}^{-1}\right)=\operatorname{det}(\mathbf{P}) \operatorname{det}(\mathbf{B}-\lambda \mathbf{I}) \operatorname{det}\left(\mathbf{P}^{-1}\right)=\operatorname{det}(\mathbf{B}-\lambda \mathbf{I})=p_{\mathbf{B}}(\lambda) . \end{aligned}$
<!--ID: 1619440544569-->



Jaký vztah je mezi vlastními čísly, jejich násobnostmi a diagonalizovatelnými maticemi? #flashcard 
![[diagonalizovatelnost.png]]
Pokud jsou geometrické násobnosti rovny algebraickým násobnostem pro odpovídající vlastní čísla.
<!--ID: 1619440544573-->



Řekni, jak uděláš rozklad matice $A=PDP^{-1}$ tak, aby $P$ byla regulární a $D$ diagonální? #flashcard 
aby platilo $A=PDP^{-1}$, tak musí být $A$ diagonalizovatelná. Protože je podobná diagonální $D$. Musí být teda i čtvercová.
jelikož platí: $Ax = \lambda x$
$D$ má na diagonále vlastní čísla (ideálně seřazená)
$P$ má jako sloupce vlastní vektory odpovídající vlastním číslům. Je regulární.
Potom platí $AP=PD$. A jelikož je $P$ je regulární, tak najdeme inverzi aplatí i $A=PDP^{-1}$
<!--ID: 1619440544578-->



Jakým způsobem můžeme diagonalizovat obdélníkové matice? #flashcard 
Žádným. (nachytal(a/o) ses, co? lolek)
<!--ID: 1619440544581-->


Můžeme o matici $X^TX$ vždy říci, že je pozitivně definitní? (pro každou matici $X$) #flashcard 
Nemůžeme. Víme pouze, že je **pozitivně semidefinitní**.
<!--ID: 1619440544585-->



Dokaž nebo vyvrať následující tvrzení: $h(X^TX) = h(XX^T) = h(X)$ pro každou matici $X \in \mathbb{R}^{m, n}$ #flashcard 
![[h_symetricke_matice.png]]
$x$ je OG ke všem řádkům $X$
$\Rightarrow Xx=\theta$
$\Rightarrow X^TXx = \theta$
$\Rightarrow x^TX^TXx = \theta$
$x^TX^TXx = (Xx)^T(Xx) = ||Xx||^2=\theta$
-> řádky $X$ a $X^TX$ generují stejný prostor, jinak by existoval $x$ z jednoho obalu, co by byl OG k druhému obalu. No když mají matice stejné lin. obal řádků, tak mají stejnou hodnost.
<!--ID: 1619440544589-->



Dokaž nebo vyvrať, že je matice $X^TX$ pozitivně definitní ($X \in \mathbb{R}^{m, n}$) #flashcard 
v důkazu pro $h(X^TX) = h(XX^T) = h(X)$ jsme si ukázali, že platí
$\boldsymbol{x}^{T} \mathbf{X}^{T} \mathbf{X} \boldsymbol{x}=(\mathbf{X} \boldsymbol{x})^{T}(\mathbf{X} \boldsymbol{x})=\|\mathbf{X} \boldsymbol{x}\|^{2} \geq 0$ no a to znamená, že pro všechny $X^TX$ **neplatí**, že jsou vždy pozitivně definitní, ale že jsou vždy pozitivně semidefinitní.
<!--ID: 1619440544594-->



Kdy je $X^TX$ pozitivně definitní? ($X \in \mathbb{R}^{m, n}$) #flashcard 
Pokud $h(X^TX) = n$. 
Jelikož platí $h(X^TX) = h(X) = n \iff Xx = \theta \iff x = \theta$. a to (s tou hodností) platí, právě když jsou sloupce LN. 
No a pro nenulové $x$ je $||Xx||^2 \gt 0 \iff x^TX^TXx \gt 0$
<!--ID: 1619440544598-->



$S$ je symetrická. Jde udělat rozklad  $S=ABA^T$?. Jaký takový užitečný rozklad znáš a jaké dobré vlastnosti mají matice $A$ a $B$? #flashcard 
Typicky se používá značení $S=QDQ^T$, které vyzradí vlastnosti (proto není použito v otázce)
$Q$ je ortonormální.
$D$ je diagonální.
<!--ID: 1619440544602-->



Dej mi nějaký vlastnosti symetrické matice $S$ #flashcard 
* $S$ je diagonalizovatelná, její vlastní vektory lze volit tak, že tvoří ortonormální bázi.
* Existuje rozklad $S=QDQ^T$
* Všechna vlastní čísla matice $S$ jsou reálná
* Je-li $S$ pozitivně semidefinitní, jsou její vl. čísla nezáporná
* Je-li $S$ pozitivně definitní, jsou její vl. čísla kladná
* $h(s) = h(S^TS) = h(SS^T)$
* $S^TS$ a $SS^T$ jsou symetrické
* $S^TS$ a $SS^T$ jsou pozitivně semidefinitní
* $S^TS \in \mathbb{R}^{n, n}$ jsou pozitivně definitní $\iff$ $h(S) = n$.
* * $SS^T \in \mathbb{R}^{m, m}$ jsou pozitivně definitní $\iff$ $h(S) = m$.
<!--ID: 1619440544606-->


Je pravda že $det(A)=det(A^{-1})$, kde $A \in T^{n, n}$? #flashcard 
Není! - nevíme jestli má $A$ inverzi. A i kdyby měla, tak to neplatí. (btw existuje případ kdy to platí)
Platí ale toto: $det(A)=det(A^T)$ dokazuje se to rozepsáním na sumu atd atd
Pojďme najít nějaký případ, kdy platí $det(A)=det(A^{-1})$. Pokud je $A$ OG, tak $det(A)=1/det(A^{-1})$ No a pokud $x=1/x$, tak $x=1$. Jaká např. existuje OG matice, že její determinant je 1? Jednotková! Druhý přístup je najít matici $A$, pro kterou platí $A=A^{-1}$.
<!--ID: 1619440544610-->


Čemu je rovno $\mathbb{E}Y$ z LR? #flashcard 
$\mathbb{E}Y = Xw$
<!--ID: 1619440544613-->
