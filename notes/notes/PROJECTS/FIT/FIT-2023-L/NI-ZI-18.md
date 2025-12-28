TARGET DECK: NI-ZI-2023::NI-PON
FILE TAGS: NI-ZI-2023 NI-ZI-18 NI-PON

prev::[[NI-ZI-17]]
next::[[NI-ZI-19]]

# Maticové faktorizace pomocí SVD
její výpočet, vlastnosti a použití ve strojovém učení: souvislost s metodou hlavních komponent (PCA) a úplným problémem nejmenších čtverců (TLS).


Kdy je matice $A$ diagonalizovatelná? #flashcard 
$A$ je diagonalizovatelná, když je podobná nějaké diagonální matici. 
Diagonální matice je čtvercová a mimo diagonálu má nuly.
Marice $A$ je podobná matici $B$, právě když existuje invertibilní matice $P$ taková, že: $P^{-1}AP=B$
<!--ID: 1692394444395-->


Popis matice v SVD rozkladu. Rekni k cemu je a na co se da toreticky pouzit #flashcard 
$A = U \Sigma V^T$, kde $U$ i $V^T$ jsou ortogonalni, $\Sigma$ je diagonalni matice, co ma na diagonale singular values $\sigma$, pro ktere plati, ze $\sigma^2$ je vl. cislo matice $AA^T, A^TA$.
Zaroven plati, ze $AA^T = U \Sigma^2 U^T$ a $A^TA = V \Sigma^2 V^T$.
pomoci SVD rozkladu se da resit homogeni LSS -> $Xw^T = \theta$ - takhle jsem napr hledal homografii v MPV
Kazda matice se da takhle rozlozit - $U$-rotace, $\Sigma$-stretch, $V^T$-rotace
<!--ID: 1692383640264-->



Jaky je vztah mezi matici $V$ a $U$ v SVD? #flashcard 
$u_i = \frac{1}{\sigma_i} Av_i$
<!--ID: 1692383640268-->



Dokaz, ze vektor $u_i$ z matice $U$ v SVD rozkladu je vlastni vektor matice $AA^T$ a ze je kolmy na vektor $u_j$ #flashcard 
Je vlastni vektor: $AA^Tu_i = expanduj = vyuzij\ vlastni\ vektor\ v_i = \sigma^2u_i$
Je kolmy: $u_i^Tu_j = expanduj = vyuzij\ vlastni\ vektor\ v_i = vykratit = \frac{\sigma_j}{\sigma_i} v_i^Tv_j  = 0$
<!--ID: 1692383640271-->



Jak ziskas SVD rozklad? #flashcard 
1) $A \in \mathbb{R}^{m, n} \rightarrow A^TA \in \mathbb{R}^{n, n}$
2) pro $A^TA$ hledame pomoci $QR$ alg. vlastni cisla $\sigma_i^2 \geq \sigma_r^2$ ($A^TA$ je positivne semi-definitni -> neostre usporadani)
3) najdeme vlastni vektor $v_i$ pro kazde vl. cislo $\sigma_i^2$. Vektory musime doplnit na ON bázi
4) $Av_i = \sigma_i u_i$, $u_i = \frac{1}{\sigma_i} Av_i$
Mame dokazano, ze $u_i$ jsou taky OG a ze jsou vlastni vektory.
<!--ID: 1692383640274-->


Definuj vlastní čísla #flashcard 
$\lambda \in \mathbb{C}$ je vlastní číslo operátoru $A \in L(V)$, právě když existuje $x \in V, x \neq \theta, tž, Ax=\lambda x$. x je pak vlastní vektor operátoru A příslušející vlastnímu číslu $\lambda$
<!--ID: 1692383640277-->


Pseudoinverze matice #flashcard 
Mějme tedy matici $A \in \mathbb{R}^{m,n}$. Matici $A^+ \in \mathbb{R}^{n,m}$ nazveme Mooreovou–Penroseovou pseudoinverzí matice $A$, jestliže splňuje následující tři vlastnosti:
* $\mathbf{A A}^{+} \mathbf{A}=\mathbf{A}$
* $\mathbf{A}^{+} \mathbf{A} \mathbf{A}^{+}=\mathbf{A}^{+}$,
* matice $\mathbf{A} \mathbf{A}^{+}$a $\mathbf{A}^{+} \mathbf{A}$ jsou symetrické.
Pokud pomocí SVD rozkladu získáme $\mathbf{A}=\mathbf{U} \boldsymbol{\Sigma} \mathbf{V}^T$, pak $\mathbf{A}^{+}=\mathbf{V} \boldsymbol{\Sigma}^{+} \mathbf{U}^T$, kde $\boldsymbol{\Sigma}^{+}$ má na diagonále inverze seřazených singulárních hodnot $(\sigma_1^{-1}, \sigma_2^{-1}, ..., \sigma_r^{-1})$ a jinde nuly.
$A^T$ je skutečně pseudoinverze, jelikož platí:
$\mathbf{A} \mathbf{A}^{+} \mathbf{A}=\mathbf{U} \boldsymbol{\Sigma} \mathbf{V}^T \mathbf{V} \boldsymbol{\Sigma}^{+} \mathbf{U}^T \mathbf{U} \boldsymbol{\Sigma} \mathbf{V}^T=\mathbf{U} \boldsymbol{\Sigma} \boldsymbol{\Sigma}^{+} \boldsymbol{\Sigma} \mathbf{V}^T=\mathbf{U} \boldsymbol{\Sigma} \mathbf{V}^T=\mathbf{A}$
<!--ID: 1692898577922-->


todo total least squares
