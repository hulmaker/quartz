TARGET DECK: Obsidian::math

[[NI-ZI-17]], [[NI-ZI-18]], [[NI-ZI-19]]


# QR rozklad
metody výpočtu, použití při výpočtu odhadu metodou nejmenších čtverců, QR algoritmus pro hledání vlastních čísel.


Popiš princip algoritmu pro QR rozklad - QR decomposition (neplést s QR algoritmus!). #flashcard 
![[QR_decomposition.png]]
Využívám toho, že násobení ortogonálních matic je ortogonální matice a že její inverze je její transpozice. Pro každou pozici v R, kde má být nula vyrobím jednu ortogonální matici, kterou když vynásobím X, tak mi vyrobí v R nulu. Ty matice potom spolu pronásobím a transponuju.
**Giwensovy rotace** - pro každou pozici jedna matice (skoro jednotková)
**Hausholdovy reflexe** - pro každý sloupec jedna matice
<!--ID: 1729010153977-->



Matice $\mathbb{Q}$ je ortogonální. Co je výsledkem $\mathbb{Q}^T \mathbb{Q}$ a proč? #flashcard 
**jednotková matice** - protože dělám dot produkt ortogonálních vektorů = 0, pouze pro ientitu na diagonále to bude 1
<!--ID: 1729010153978-->



Jak získám inverzní matici k ortogonální matici $\mathbb{Q}$? #flashcard 
transponuju ji, jelikož $\mathbb{Q}^T \mathbb{Q} = \mathbb{E}$
<!--ID: 1729010153979-->



Dokaž že $||\mathbb{Q}v||^2 = ||v||^2$, kde $\mathbb{Q}$ je ortogonální matice a $v$ je vektor příslušných rozměrů. #flashcard 
$$||\mathbb{Q}v||^2 = (\mathbb{Q} v)^T \mathbb{Q} v = v^T \mathbb{Q}^T \mathbb{Q} v = v^T \mathbb{E} v = v^T v = ||v||^2$$
<!--ID: 1729010153980-->




$\mathbb{B}, \mathbb{A}, \mathbb{P}$ jsou matice. Dokaž, že $\mathbb{B}$ a $\mathbb{A}$ mají stejná vlastní čísla pokud platí: $\mathbb{B}=\mathbb{P}\mathbb{A}\mathbb{P}^{-1}$ #flashcard 
$\mathbb{B}=\mathbb{P}\mathbb{A}\mathbb{P}^{-1}$
$$
\begin{aligned}
\det(\mathbb{P}\mathbb{A}\mathbb{P}^{-1}-\lambda\mathbb{E}) & =
\det(\mathbb{P}(\mathbb{A}-\lambda\mathbb{E})\mathbb{P}^{-1}) \\
& = \det(\mathbb{P})\det(\mathbb{A}-\lambda\mathbb{E}) \det(\mathbb{P}^{-1}) \\
& = \det(\mathbb{A}-\lambda\mathbb{E})
\end{aligned}
$$
$\mathbb{P}$ je regulární
<!--ID: 1729010153981-->



Kdy jsou si matice $A, B$ podobne? #flashcard 
Pokud existuje regulární $P \in \mathbb{C}^{n, n}$ takova, ze $A = P^{-1}BP$
1. A je podobná A,
2. pokud A je podobná B, pak B je podobná A,
3. pokud A je podobná B a B je podobná D, pak A je podobná D.
<!--ID: 1729010153982-->



Popiš zakladni myslenku QR algoritmu #flashcard 
Je to algoritmus pro hledani vlastnich cisel. Idealne v hustych maticich. Jelikoz je to slozite, tak si to iteracnim rozkladanim zjednodusujeme. A to si muzeme dovolit diky tomu, ze podobne matice maji stejna vlastni cisla.
![[EXTRAS/Media/QR_algorithm.png]]
```python
Aiter = A,
for i in range(N):,
    Q, R = np.linalg.qr(Aiter)  # QR rozklad
    Aiter = R.matmul(Q)
assert set(np.linalg.eigvals(Aiter)) == set(np.linalg.eigvals(A))
```
<!--ID: 1729010153983-->



Dokaž, že jsou vlastní čísla symetrické matice z $\mathbb{R}$. #flashcard 
![[eigenvalues_symm_matrix.jpg]]
Alternativa: $x$ je vl. vektor
jelikož $(\mathbb{A}x, y) = (x, \mathbb{A} y)$, tak to jde i  takhle
$\lambda\|x\|^{2}=(x, \lambda x)=(x, \mathbb{A} x)=(\mathbb{A} x, x)=(\lambda x, x)=\bar{\lambda}\|x\|^{2}$
Z toho plyne $\bar{\lambda} = \lambda$. Jelikož $x \neq \theta, ||x||= neq 0$
<!--ID: 1729010153984-->



Dokaž pro $QR$ rozklad, že když rozdělíš matici $Q$ na $Q_1$ (p+1 sloupcu) a $Q_2$ (zbytek sloupcu), tak platí, že $X = QR = Q_1R$ #flashcard 
$R$ má od p+2 řádku až do konce jen nuly, takže když jí násobíme, tak stačí jen $Q_1$ a ten horní trojůhelník z R co nejsou nuly. Je to výpočetně i paměťově výhodný.
<!--ID: 1729010153985-->



Dokaž, že když násobím víc ortogonálních matic, tak je výsledek taky ortogonální #flashcard 
$$(Q_1 Q_2)^T Q_2 Q_1 = Q_1^T Q_2^T Q_2 Q_1 = Q_1^T E Q_1 = E$$
<!--ID: 1729010153986-->



Givens rotation (hint: QR decomposition) #flashcard 
Hledáme ortogonální matici $S \in \mathbb{R}^{2, 2}$, která otočí nenulový vektor $x = (a, b)^T$ tak, že
výsledný vektor leží na ose $x$ a jeho druhá složka je tak nulová.
$$
Sx=
\left(\begin{array}{cc}
\alpha & \beta \\
-\beta & \alpha
\end{array}\right)\left(\begin{array}{l}
a \\
b
\end{array}\right)=\left(\begin{array}{c} 
\pm\|\boldsymbol{x}\| \\
0
\end{array}\right)=\left(\begin{array}{c} 
\pm \sqrt{a^2+b^2} \\
0
\end{array}\right)$$
![[Givens_rotation.excalidraw.png]]
$$\alpha=\frac{a}{\sqrt{a^2+b^2}}=\cos \varphi \quad \text { a } \quad \beta=\frac{b}{\sqrt{a^2+b^2}}=\sin \varphi$$
<!--ID: 1729010153987-->




Householder reflection. (hing: QR decomposition) #flashcard 
Hledáme ortogonální matici $\mathbf{P}$ takovou, aby reflektovala vektor $\boldsymbol{x}$ na osu $x$ a tak vyrábíme nuly.
$$\mathbf{P} \boldsymbol{x}=\mathbf{P}\left(\begin{array}{c}
x_1 \\
x_2 \\
\vdots \\
x_m
\end{array}\right)=\left(\begin{array}{c} 
\pm\|\boldsymbol{x}\| \\
0 \\
\vdots \\
0
\end{array}\right)$$
Nakonec se dostaneme k výrazu $\mathbf{P} \boldsymbol{y}=\boldsymbol{y}-2 \boldsymbol{u} \boldsymbol{u}^T \boldsymbol{y}$
<!--ID: 1729010153988-->



Kdy je matice $A$ diagonalizovatelná? #flashcard 
$A$ je diagonalizovatelná, když je podobná nějaké diagonální matici. 
Diagonální matice je čtvercová a mimo diagonálu má nuly.
Marice $A$ je podobná matici $B$, právě když existuje invertibilní matice $P$ taková, že: $P^{-1}AP=B$
<!--ID: 1729010153989-->



Popis matic v SVD rozkladu. Rekni k cemu jednotlive matice slouzi a na co se daji pouzit #flashcard 
$A = U \Sigma V^T$, kde $U$ i $V^T$ jsou ortogonalni, $\Sigma$ je diagonalni matice, co ma na diagonale singular values $\sigma$, pro ktere plati, ze $\sigma^2$ je vl. cislo matice $AA^T, A^TA$.
Zaroven plati, ze $AA^T = U \Sigma^2 U^T$ a $A^TA = V \Sigma^2 V^T$.
pomoci SVD rozkladu se da resit homogeni LSS -> $Xw^T = \theta$ - takhle jsem napr hledal homografii v MPV
Kazda matice se da takhle rozlozit - $U$-rotace, $\Sigma$-stretch, $V^T$-rotace
<!--ID: 1729010153990-->



Jaky je vztah mezi matici $V$ a $U$ v SVD? #flashcard 
$A = U \Sigma V^T$
$u_i = \frac{1}{\sigma_i} Av_i$
kde $u_i$ je vektor z $U$ a $v_i$ je z $V$
<!--ID: 1729010153991-->



Dokaz, ze vektor $u_i$ z matice $U$ v SVD rozkladu je vlastni vektor matice $AA^T$ a ze je kolmy na vektor $u_j$ #flashcard 
Je vlastni vektor: $AA^Tu_i = expanduj = vyuzij\ vlastni\ vektor\ v_i = \sigma^2u_i$
Je kolmy: $u_i^Tu_j = expanduj = vyuzij\ vlastni\ vektor\ v_i = vykratit = \frac{\sigma_j}{\sigma_i} v_i^Tv_j  = 0$
<!--ID: 1729010153992-->



Jak ziskas SVD rozklad? #flashcard 
1) $A \in \mathbb{R}^{m, n} \rightarrow A^TA \in \mathbb{R}^{n, n}$
2) pro $A^TA$ hledame pomoci $QR$ alg. vlastni cisla $\sigma_i^2 \geq \sigma_r^2$ ($A^TA$ je positivne semi-definitni -> neostre usporadani)
3) najdeme vlastni vektor $v_i$ pro kazde vl. cislo $\sigma_i^2$. Vektory musime doplnit na ON bázi
4) $Av_i = \sigma_i u_i$, $u_i = \frac{1}{\sigma_i} Av_i$
Mame dokazano, ze $u_i$ jsou taky OG a ze jsou vlastni vektory.
<!--ID: 1729010153993-->



Definuj vlastní čísla #flashcard 
$\lambda \in \mathbb{C}$ je vlastní číslo operátoru $A \in L(V)$, právě když existuje $x \in V, x \neq \theta, tž, Ax=\lambda x$. x je pak vlastní vektor operátoru A příslušející vlastnímu číslu $\lambda$
<!--ID: 1729010153994-->



Pseudoinverze matice #flashcard 
Mějme tedy matici $A \in \mathbb{R}^{m,n}$. Matici $A^+ \in \mathbb{R}^{n,m}$ nazveme Mooreovou–Penroseovou pseudoinverzí matice $A$, jestliže splňuje následující tři vlastnosti:
* $\mathbf{A A}^{+} \mathbf{A}=\mathbf{A}$
* $\mathbf{A}^{+} \mathbf{A} \mathbf{A}^{+}=\mathbf{A}^{+}$,
* matice $\mathbf{A} \mathbf{A}^{+}$a $\mathbf{A}^{+} \mathbf{A}$ jsou symetrické.
Pokud pomocí SVD rozkladu získáme $\mathbf{A}=\mathbf{U} \boldsymbol{\Sigma} \mathbf{V}^T$, pak $\mathbf{A}^{+}=\mathbf{V} \boldsymbol{\Sigma}^{+} \mathbf{U}^T$, kde $\boldsymbol{\Sigma}^{+}$ má na diagonále inverze seřazených singulárních hodnot $(\sigma_1^{-1}, \sigma_2^{-1}, ..., \sigma_r^{-1})$ a jinde nuly.
$A^T$ je skutečně pseudoinverze, jelikož platí:
$\mathbf{A} \mathbf{A}^{+} \mathbf{A}=\mathbf{U} \boldsymbol{\Sigma} \mathbf{V}^T \mathbf{V} \boldsymbol{\Sigma}^{+} \mathbf{U}^T \mathbf{U} \boldsymbol{\Sigma} \mathbf{V}^T=\mathbf{U} \boldsymbol{\Sigma} \boldsymbol{\Sigma}^{+} \boldsymbol{\Sigma} \mathbf{V}^T=\mathbf{U} \boldsymbol{\Sigma} \mathbf{V}^T=\mathbf{A}$
<!--ID: 1729010153995-->


# Hladka optimalizace 

Popiš jak vypadá standartní optimalizační problém #flashcard 
minimalizuj $f(x)$,
za podmínek $g(x)=0, h(x) \leq 0$ atd...
kde $f: D \to \mathbb{R}, g: D \to \mathbb{R}^p, h: D \to \mathbb{R}^m$, kde $D \subset \mathbb{R}^n$
<!--ID: 1729010153996-->



Do jakých kategorií rozdělujeme optimalizační úlohy? (minimalizuj $f(x)$, za podmínek $g(x)=0, h(x) \leq 0$) #flashcard 
minimalizuj $f(x)$, za podmínek $g(x)=0, h(x) \leq 0$
1) **nelineární programování** (nonlinear programming - NLP): předpokládáme spojitou diferencovatelnost (někdy i dvojitou)
2) **lineární programování** (linear programming - LP): $f, g$ a h jsou afinní funkce
3) **kvadratické programování** (quadratic programming LP): $f$ je kvadratická (tj.$f(x) = a^T\cdot x +\frac{1}{2}x^T\cdot B\cdot x$), kde $g, h$ jsou afinní funkce)
4) **konvexní optimalizace** (convex optimization): $f$ je konvexní na $M$ - množina přípustných řešení
5) **nehladká optimalizace** (non-smooth optimization): některá z funkcí není diferencovatelná)(smíšené) celočíselné programování a jeho varianty
<!--ID: 1729010153997-->



Co za vlastnost (souvisí s derivací) by měla mít funkce, kterou optimalizujeme? #flashcard 
Měla by být dvakrát spojitě diferencovatelná. Abychom mohli použít ty oblíbené iterační metody. Dál často používáme Taylorův rozvoj druhého řádu.
<!--ID: 1729010153998-->



Uvažuj libovolnou optimalizační metodu, kdy iterujeme přes posloupnost aproximací konvergující k nějakému minimu. Jaké základní metody pro počítání následující aproximace máme? #flashcard 
**line-search** - Následující aproximaci hledáme v nějakém daném směru $p_k$, směr se dá volit např. jako směr největšího spádu, newtonova metoda atd.
**region-trust** - Na okolí bodu $x_k$ vytvoříme nějakou aproximaci funkce $f$, označené $m_k$, a hledáme minimum této aproximace $m_k$ na okolí bodu $x_k$ 
<!--ID: 1729010153999-->


Jaké jsou možné podmínky pro volbu délky kroku v line-search optimalizaci? #flashcard 
**Armijova podmínka** - next step musí být pod klesající přímkou (můžu si dovolit velký krok, jen musí být dost dobrý) $\phi\left(\alpha_k\right) \leq \phi(0)+\alpha_k c \phi^{\prime}(0)$
**Goldsteinova podmínka** - Jako Armijova podmínka, jen mám přímku i pro lower boud. - můžu tak minout minimum co bude pod hranicí, ale nedělám miniaturní kroky. $\phi(0)+\alpha_k(1-c) \phi^{\prime}(0) \leq \phi\left(\alpha_k\right) \leq \phi(0)+\alpha_k c \phi^{\prime}(0)$
**Wolfeho slabá podmínka** - přímka shora a derivace v next step je větší, než v bodě kde teď jsem (svah není moc strmý), 
**Wolfeho silná podmínka** - přímka shora, sklon je v absolutní hodnotě = krom spádu kouká i na růst
<!--ID: 1729010154000-->



Popiš metodu line-search pro optimalizační úlohu #flashcard 
Následující aproximaci hledáme v nějakém daném směru $p_k$.
$x_{k+1} = x_k + \alpha_kp_k$, kde $p_k$ je směr a $\alpha$ je délka kroku.
<!--ID: 1729010154001-->



Jak se dá volit směr v optimalizační úloze při metodě line-search? #flashcard 
line search $x_{k+1} = x_k + \alpha_kp_k$, kde $p_k$ je směr a $\alpha$ je délka kroku.
Častá volba směru: směr spádu: $p_k = -B_k^{-1}\nabla f(x_k)$
$Bk = I$ - metoda největšího spádu
$B_k = \nabla^2 f(x_k)$ - Newtonova metoda
$B_k \approx \nabla^2 f(x_k)$ - kvazi-Newtonova metoda
<!--ID: 1729010154002-->



Co je metoda největšího spádu při optimalizaci? #flashcard 
typ line-search metody, kdy směr následujícího kroku volíme jako směr, ve kterém funkce nejvíce klesá. To odpovídá směru -gradient v bodě kde právě jsem
<!--ID: 1729010154003-->



Jaká je obecná myšlenka Newton method v kontextu optimalizace? #flashcard 
Předpokládá komplikovanou ztrátovou funkci. Aproximuje jí Taylorem 2. řádu a hledá minimum. Jelikož to je polynom, tak tu rovnici zvládneme vyřešit relativně snadno.
parciální derivace, gradient = 0, normální rovnice atd.
<!--ID: 1729010154004-->



Napiš vzorec pro Taylorův polynom 2. stupně pro funkci $f(x_k + p)$ #flashcard 
$f\left(x_{k}+p\right) \approx f\left(x_{k}\right)+\nabla f\left(x_{k}\right)^{T} p+\frac{1}{2} p^{T} \nabla^{2} f\left(x_{k}\right) p=m_{k}\left(x_{k}+p\right)$
<!--ID: 1729010154005-->



Pomocí Newtonovy metody minimalizujeme funkci. Jsme v iteraci $k$, máme tedy parametry $x_k$ a potřebujeme určit směr dalšího kroku $p_k$. Odvoď jej. #flashcard 
Taylorův polynom 2. stupně funkce $f\left(x_{k}+p\right)$
$m_{k}\left(x_{k}+p\right) = f\left(x_{k}\right)+\nabla f\left(x_{k}\right)^{T} p+\frac{1}{2} p^{T} \nabla^{2} f\left(x_{k}\right) p$
hledáme $p_{k}=\underset{p}{\operatorname{argmin}} m_{k}\left(x_{k}+p\right)$
parciální derivace, gradient
$\nabla m_{k}\left(x_{k}+p\right)=0 \quad \Longleftrightarrow \quad \nabla f\left(x_{k}\right)+\nabla^{2} f\left(x_{k}\right) p=0$
směr dostaneme takto
$p_k = -(\nabla^2(fx_k))^{-1}\nabla f(x_k)$
Předpokládáme, že $\nabla^2(fx_k)$ je regulární
<!--ID: 1729010154006-->



Hlavní myšlenka Kvazinewtonových metod? K čemu jsou užitečné? (optimalizace) #flashcard 
Kvazinewtonovské metody nějakým způsobem aproximují matici $\nabla^2(fx_k)$ a snaží se tak vylepšit celkově algoritmus, například tím, že matice $B_{k+1}$ se napočítává aktualizací matice $B_k$.
Je to další aproximace, ale velmi výrazně snižuje koplexitu algoritmu. Dá se ukázat, že má podobné vlastnosti jako Newtonova metoda a že konverguje.
<!--ID: 1729010154008-->



Definuj konvexní množinu $\Omega \in \mathbb{R}^n$ a konvexní funkci $f: \Omega  \to \mathbb{R}$ (optimalizace) #flashcard 
Množina je konvexní, pokud $\alpha x + (1-\alpha)y \in \Omega$
pro $\forall x, y \in \Omega$ a $\forall \alpha \in [0, 1]$ (pro každé dva body lezí všechny body na úsečce mezi nimi v množině. (kružnice, elipsa atd))
funkce je konvexni, pokud $\Omega$ jek onvexni a pokud $f(\alpha x + (1-\alpha )y) \leq \alpha f(x) + (1-\alpha)f(y)$
funkce je ryze konvexni, pokud je tam ostra nerovnost.
<!--ID: 1729010154012-->


Jaké jsou charakteristické vlastnosti konvexních množin  (optimalizace) #flashcard 
* $c \in \mathbb{R}, \{x \in \Omega | f(x) \leq c \}$ je konvexní (sublevel set), kde konvexní $f:\Omega \to \mathbb{R}$
* Průnik (ne)konečně mnoha konv. množin je konvexní
* Afinní zobrazení konvexní množiny je konvexní
* Afinní transformace proměnných zachovává konvexitu funkce
* Je-li f konvexní a g konvexní a monotónní funkce, pak je g složeno s f konvexní
<!--ID: 1729010154013-->


#note/develop  - extrapoluj informace s konvexni optimalizace - k cemu je atd, nejake principy. To same pro lagrangeovy funkce atd.
