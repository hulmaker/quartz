TARGET DECK: NI-SPOL-2023::NI-VSM
FILE TAGS: NI-SPOL-2023 NI-SPOL-07 NI-VSM

prev::[[NI-SPOL-06]]
next::[[NI-SPOL-08]]

# Základy teorie informace a kódování


Co je střední délka kódu v teorii informace a kódování? #flashcard 
Střední délka kódu je střední hodnota délek zpráv z X.
Množina zpráv X, zpráva má pravděpodobnost výskytu p(x), $l(x)$ je délka kódového slova pro zprávu x
$$L(C)=\mathrm{E} l(X)=\sum_{x \in X} l(x) \cdot \mathbb{P}(X=x)$$
<!--ID: 1691601081137-->



Typy kódů - Nesingulární kód (teorie informace a kódování) #flashcard 
Kód je nesingulární, pokud je $C$ prosté zobrazení: $\forall x, x' \in X: x\neq x' \implies C(x) \neq C(x')$
Díky tomu lze kazde kodove slovo jednoznacne dekodovat.
Pokud budeme mit retez kodovych slov bez oddelovacu, tak jej dekodovat jednoznacne nejde
<!--ID: 1691601081139-->



Typy kódů - Jednoznačně dekódovatelný kód (teorie informace a kódování) #flashcard 
$X^∗$: množin všech možných řetězců složených ze zpráv v X
$C^∗$ zobrazení z množiny $X^∗$ do $D^∗$, (kód kóduje celé řetězce, nikoliv znaky)
C je jednoznačně dekódovatelný, pokud je $C^∗$ nesingulární
Platí pro něj $L(C) \geq H_D(X)$
$L(C) = H_D(X) \iff P(X=x)=D^{-l(x)}$
<!--ID: 1691601081140-->



Typy kódů - Instantní kód (teorie informace a kódování) #flashcard 
• V instantním kódu není žádné kódové slovo prefixem jiného kódového slova
• Dokážeme tedy v řetězci kódových slov jednoznačně identifikovat jednotlivá kódová slova
• Tudíž dokážeme řetězec dekódovat postupně, znak po znaku, bez nutnosti přijetí celé zprávy
<!--ID: 1691601081141-->



Kraftova nerovnost (teorie informace a kodování) #flashcard 
Pro libovolný instantní kód nad abecedou velikosti $D$ a délky kódových slov $l_1, ..., l_n$ musí platit
$$\sum_i D^{-l_i} \leq 1$$
(McMillan). Pro libovolný jednoznačně dekódovatelný kód toto platí taky.
* Ukazuje, že množina jednoznačně dekódovatelných kódů nenabízí žádné další možnosti délek kódových slov oproti množině instantních kódů. 
* Ke každému jednoznačně dekódovatelnému kódu lze sestrojit instantní kód, který má stejně dlouhá kódová slova.
* Budeme-li se tedy zabývat optimalitou instantních kódů, získáme zároveň optimalitu mezi jednoznačně dekódovatelnými kódy.
<!--ID: 1691601081142-->



Huffmanovo kódování (teorie informace a kódování) #flashcard 
Alg. k sestrojení optimálního kódu pro zprávy s danými pravděpodobnostmi
Pro kód navíc platí: $H_D(X) \leq L\left(C^*\right) \leq H_D(X)+1$
Tvoříme strom od listů:
1. uzly pro všechny zprávy. ohodnotíme je pstěmi.
2. Vyrábíme rodičovský uzel pro dva uzly s nejmenší pstí. (jeho pst je součet)
3. Každé hraně přiřadímo 0 nebo 1
4. cesta od listu ke kořenu je kód pro odpovídající zprávu
<!--ID: 1691601081144-->


Popište hierarchii kódů - základy teorie kódování a informace (NI-MPI) #flashcard 
**Instantní**: (prefixový) žádné kódové slovo není prefixem jiného kódového slova
**Jednoznačně dekódovatelný**: Kód $C$ je jednoznačně (též unikátně) dekódovatelný, pokud je $C^*$ nesingulární.  Kde $C^*$ je rozšíření kódu $C$. (Je-li např. $C(x_1) = 0$ a $C(x_2) = 001$, tak $C^∗(x_1x_2) = 0001$)
**Nesingulární**: $C$ prosté zobrazení. Tj. $x \neq x^{\prime} \Rightarrow C(x) \neq C\left(x^{\prime}\right)$
![[Pasted image 20230818202702.png]]
<!--ID: 1692383640291-->


# Entropie


Entropie diskrétní náhodné veličiny #flashcard 
Míra neurčitosti, Nulová entropie znamená jistý jev, S klesající pravděpodobností jevu roste hodnota jeho entropie, entropie je nezáporná.
$$H(X)=-\mathrm{E} \log (p(X))=-\sum_{x \in X} p(x) \cdot \log (p(x))$$
<!--ID: 1691601081145-->



Sdružená entropie dvou sdružených náhodných veličin #flashcard 
$$H(X, Y)=-\mathrm{E} \log (p(X, Y))=-\sum_{x \in X} \sum_{y \in Y} p(x, y) \cdot \log (p(x, y))$$
<!--ID: 1691601081146-->



Podmíněná entropie dvou sdružených náhodných veličin #flashcard 
$$H(Y \mid X)=-\mathrm{E} \log (p(Y \mid X))=-\sum_{x \in X} \sum_{y \in Y} p(x, y) \cdot \log (p(y \mid x))$$
kde $$p(y \mid x)=\frac{\mathbb{P}(X=x, Y=y)}{\mathbb{P}(X=x)}$$
<!--ID: 1691601081147-->


Relativní entropie jakožto vzdálenost mezi dvěmi diskrétními veličinami #flashcard 
$$D(p \| q)=-\sum_{x \in X} p(x) \cdot \log \left(\frac{p(x)}{q(x)}\right)$$
<!--ID: 1691601081148-->



Řetězové pravidlo entropie a souvislost podmíněné, sdružené a marginální entropie #flashcard 
Pravidlo: $H(X, Y)=H(X)+H(Y \mid X)$
* Neboli $H(Y \mid X)=H(X, Y)-H(X)$, tedy $H(Y \mid X)$určuje, jaká informace je navíc v Y oproti X
* $H(X)$ určuje informaci pouze v $X$
* $H(X, Y)$ určuje sjednocení informace v $X$ a $Y$
* $H(Y \mid X)$ určije informaci v $Y$ co není v $X$
* $I(X, Y)$ určuje průnik informací v $X$ a $Y$
* pro nezávislé $X, Y$ platí: $H(X, Y)=H(X)+H(Y)$
<!--ID: 1691601081149-->



Vzájemná informace (MI) mezi dvěmi náhodnými veličinami + souvislost s entropii #flashcard 
$$
I(X, Y)=\sum_{x \in X} \sum_{y \in Y} p(x, y) \cdot \log \left(\frac{p(x, y)}{p(x) \cdot p(y)}\right)
$$
Vlastnosti:
$$
\begin{aligned}
	& I(X ; Y)=I(Y ; X) \\
	& I(X ; Y)=H(X)-H(X \mid Y) \\
	& I(X ; Y)=H(Y)-H(Y \mid X) \\
	& I(X ; Y)=H(X)+H(Y)-H(X, Y) \\
	& I(X ; X)=H(X)
\end{aligned}
$$
<!--ID: 1691601081150-->

