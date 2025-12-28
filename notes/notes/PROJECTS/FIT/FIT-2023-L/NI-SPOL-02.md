TARGET DECK: NI-SPOL-2023::NI-MPI
FILE TAGS: NI-SPOL-2023 NI-SPOL-02 NI-MPI

prev::[[NI-SPOL-01]]
next::[[NI-SPOL-03]]

# Tělesa a okruhy

Definuj okruh (teorie grup) #flashcard 
Buďte M neprázdná množina a + a · binární operace na této množině. Řekneme,
že trojice R = (M, +, ·) je okruh, pokud platí:
* (M, +) je abelovská grupa,
* (M, ·) je monoid,
* platí (levý a pravý) distributivní zákon: $(\forall a, b, c \in M)(a \cdot(b+c)=a \cdot b+a \cdot c \wedge (b+c) \cdot a=b \cdot a+c \cdot a)$
<!--ID: 1691160648517-->


Definuj Těleso (teorie grup) #flashcard 
Okruh T = (M, +, ·) se nazývá těleso, jestliže $(M \text{\\} \{0\}, ·)$ je abelovská grupa. Tuto grupu nazýváme multiplikativní grupou tělesa T.
(Dej pozor na to, ze musis vyjmout nulovy prvek!!!)
<!--ID: 1691168777776-->


## Základní definice a vlastnosti

Napiš příklady okruhů (teorie grup) #flashcard 
* $(\{0\}, +, \cdot)$ je trivialni okruh
* $(\mathbb{Z}, +, \cdot)$ je okruh, (ale $(\mathbb{N}, +, \cdot)$ neni okruh, neb $(\mathbb{N}, +)$ neni grupa)
* nožina $(\mathbb{R}^{n,n}, +, ·)$ čtvercových reálných matic se sčítáním po prvcích a maticovým násobením je okruh, nulový prvek je nulová matice (podobně pro komplexní matice)
* množina všech polynomů (s komplexními / reálnými / celočíselnými koeficienty) je okruh, nulový prvek je nulový polynom, tj. polynom splňující $p(x) = 0$ pro každé $x$
<!--ID: 1691168777786-->



Jaké jsou základní vlastnosti okruhu? (teorie grup) #flashcard 
* $(\forall a \in M): a \cdot 0 = 0 \wedge 0 \cdot a = 0$
* $(\forall a \in M): (-a)\cdot b = -a \cdot b$
* $(\forall a, b, c \in M): c(b-a)=cb-ca$
<!--ID: 1691168777792-->



Co je obor integrity? (klicova slova: teorie grup, okruh, integral domain) #flashcard 
Nenulové prvky a, b ∈ M z okruhu (M, +, ·) nazýváme dělitelé nuly, právě když a · b = b · a = 0. Obor integrity je komutativní okruh, ve kterém neexistují dělitelé nuly.
<!--ID: 1691168777796-->



Napiš příklady těles (teorie grup) #flashcard 
* kruh racionálních čísel $(\mathbb{Q}, +, \cdot)$ je těleso. Dokonce nejmenší číselné těleso (s obvyklými aritmetickými operacemi).
* kruh celých čísel $(\mathbb{Z}, +, \cdot)$ není těleso, neb $(\mathbb{Z} \text{\\} \{0\}, \cdot)$ není grupa (chybí inverzní prvky).
* Nejmenší těleso je tzv. triviální těleso ({0, 1}, +, ·)
<!--ID: 1691168777799-->



Dokaž: Pokud pro $a, b$ z tělesa $T$ platí $ab = 0$ potom $a = 0$ nebo $b = 0$. #flashcard 
Důkaz. Sporem: kdyby $a \neq 0$ a $b \neq 0$ potom $ab \neq 0$, protože multiplikativní grupa $(T \text{\\} \{0\}, ·)$ je uzavřená na násobení.
<!--ID: 1691168777802-->


## Konečná Tělesa

Definuj konečné těleso (teorie grup) #flashcard 
Těleso, které má konečný počet prvků, se nazývá konečné.
Řádem tělesa se, podobně jako u grup, označuje počet prvků tělesa. Tedy konečná tělesa jsou tělesa konečného řádu.
<!--ID: 1691168777804-->



Napiš nějaké základní informace o tělese $(\mathbb{Z}_p, +, \cdot)$ #flashcard 
Aditivní grupa $\mathbb{Z}_p^+$ má řád p, každý nenulový prvek je generátor a má tedy řád p. (to platí pro všechny grupy s prvočíselným řádem (ale $(\mathbb{Z}_p, +$) je grupa i presto ze p neni prvocislo)
Multiplikativní grupa $\mathbb{Z}_p^\times$ má řád p-1 (s výjimkou p=3 není p-1 prvočíslo (je sudé)). $\mathbb{Z}_p^\times$ je cyklická, existuje v ní $\varphi(p-1)$ generátorů.
<!--ID: 1691168777807-->



Co víme o řádu konečného tělesa? (teorie grup) #flashcard 
Řádem konečného tělesa musí být mocnina prvočísla, tedy číslo zapsatelné jako $p^n$, kde $p$ je prvočíslo a $n$ je kladné celé číslo. Navíc platí, že všechna tělesa řádu $p^n$ jsou **navzájem izomorfní**. Těleso s $p^n$ prvky nazýváme Galois field.
<!--ID: 1691168777810-->



Napište příklad tělesa se šesti prvky (teorie grup) #flashcard 
takové těleso neexistuje, jelikož všechna konečná tělesa mají jako řád mocninu prvočísla.
<!--ID: 1691168777814-->



## Okruhy Polynomů

Definuj polynom nad okruhem (teorie grup) #flashcard 
Okruh $R$ a $a_i \in R, i = 0, 1, ..., n$. Nasledujici vyraz je polynom nad okruhem $R$.
$$P(x) = \sum^n_{i=0}a_ix^i$$
<!--ID: 1691168777817-->


Definuj okruh polynomů (teorie grup ) #flashcard 
Buď R okruh. Potom množina všech polynomů nad okruhem $R$ spolu s operacemi sčítání a násobení definovanými předpisy
$$
\begin{aligned}
\sum_{i=0}^n a_i x^i+\sum_{i=0}^n b_i x^i & :=\sum_{i=0}^n\left(a_i+b_i\right) x^i \\
\left(\sum_{j=0}^n a_j x^j\right) \cdot\left(\sum_{k=0}^m b_k x^k\right) & :=\sum_{i=0}^{n+m}\left(\sum_{j+k=i} a_j b_k\right) x^i
\end{aligned}
$$
kde $a_i, b_i \in R$ pro všechny hodnoty i, tvoří okruh polynomů nad okruhem R. Tento okruh značíme $R[x]$.
<!--ID: 1691168777819-->



Existuje nad konečným tělesem polynom $p(x)$ (řádu většího jak 1) co má kořen a je ireducibilní? Pokud ano, jaký? #flashcard 
Pokud $deg(p(x)) > 1$, pak neexistuje. Polynom co má kořen nemůže být ireducibilní. Polynomial factor theorem:  $p(x)=(x-k)g(x)$, platí právě když $k$ je kořen $p(x)$ a $deg(f) = deg(g(x))+1$.  No a protože $deg(p(x)) > 1$, tak $deg(g(x)) > 0$ a tím pádem máme rozklad polynomu p(x).
<!--ID: 1691168777822-->



Polynom $p(x) \in T[x]$ stupně $n$ nemá kořen. V jakém případě platí $p(x) = (x-k)g(x)$, kde $g(x) \in T[x]$ je polynom stupně $n-1$ a $k \in T$ . A proč tomu tak je? #flashcard 
**V žádném**. Polynomial factor theorem nám říká, že takový rozklad existuje právě když je $k$ kořenem polynomu $p(x)$.
<!--ID: 1691168777825-->



$f(x), g(x) \in T[x]$ jsou nenulové polynomy z tělesa $T$. Platí $deg(f(x)) = 42$. Jakého stupně musí být polynom $g(x)$, aby měl polynom $f(x) \cdot g(x)$ stupeň 708? #flashcard 
$deg(g(x))=666$, protože podle lemma o násobení polynomů platí $deg(f(x) \cdot g(x))=deg(f(x)) + deg(g(x))$
<!--ID: 1691168777828-->



Popište lemma o násobení polynomů a lemma o dělění polynomů (teorie grup) #flashcard 
$f(x), g(x) \in T[x]$ jsou nenulové polynomy z tělesa $T$. Pak platí:
* $deg(f(x) \cdot g(x))=deg(f(x)) + deg(g(x))$
* Existují jednoznačně určené polynomy ($q(x), r(x) \in T[x]): f(x) = q(x)g(x)+r(x)$
<!--ID: 1691168777831-->



Popište Bézoutovu rovnost pro polynomy. #flashcard 
$f(x), g(x) \in T[x]$ jsou nenulové polynomy nad tělesem T. Pak existují $u(x), v(x) \in T[x]$ tak, že $gcd(f(x), g(x)) = u(x)f(x) + v(x)g(x)$
<!--ID: 1691168777834-->



Popište polynomial factor theorem. (teorie grup) #flashcard 
$p(x) \in T[x]$ je polynom stupně n z tělesa $T$. Prvek $k \in T$ je kořen polynomu $p$ právě tehdy, když $p(x) = (x-k)g(x)$, kde $g(x) \in T[x]$ je supně $n-1$.
<!--ID: 1691168777837-->



Popište jak najít $(2x)^{-192}$ v $GF(3^4)$ s násobením mod $p(x)$. (teorie grup) #flashcard 
1. Zjednodušit: $(2x)^{192} = 2^{192} \cdot x^{192} = 1 \cdot x^{2\cdot80} \cdot x^{32} = x^{32}$.
2. Pro výraz $x^{32}$ najdeme pomocí čtverců základní tvar. Pomůžeme si tak, že spočítáme $x^6, x^5, x^4$, to potom dosazujeme a nemusíme pokaždé dělit.
3. Pomocí EEA najdeme inverzi k základnímu tvaru $x^{32}$.
<!--ID: 1691168777840-->


## Ireducibilní Polynom.


Definujte ireducibilni polynom nad okruhem K #flashcard 
Buď $P(x) \in K[x]$ stupně alespoň 1. Řekneme, že $P(x)$ je ireducibilní nad okruhem $K$, jestliže pro každé dva polynomy $A(x)$ a $B(x)$ z $K[x]$ platí: 
$$
A(x) \cdot B(x) = P(x) \implies (deg(A(x)) = 0 \lor deg(B(x)) = 0)
$$
<!--ID: 1691168777843-->



Jak budete postupovat, když budete chtít zjistit, zda-li je polynom $p(x) \in T[x]$ ireducibilní? #flashcard 
1. Pokud $deg(p(x)) > 1$ a $p(x)$ má kořen, pak není ireducibilní.
2. Podle lemma o násobení polynomů najdu možné stupně faktorů $q(x), g(x)$.
3. Většinou zbydou tak 2 dvojice možných stupňů.
4. Pro ty stupně si najdeme ireducibilní polynomy (většinou lehké) a dělíme $p(x)$.
5. Pokud žádný z nich nedělí $p(x)$ beze zbytku, pak je $p(x)$ ireducibliní.
<!--ID: 1691168777846-->



Polynom $p(x) \in T[x]$ nemá kořen. Je ireducibilní? #flashcard 
Záleží na stupni $p(x)$. Pokud má $p(x)$ stupeň 2 nebo 3 a nemá kořen, tak je ireducibilní. (Vyzkoušej dokázat)
Jinak **nevíme**. Když kořen nemá, tak to nutně neznamená, že je ireducibilní. Víme ale, že kdyby kořen měl a jeho stupeň by byl větší něž jedna, pak by ireducibilní nebyl.
<!--ID: 1691168777848-->



Musí platit, že každý polynom nad tělesem T, který má stupeň menší nebo roven třem a není ireducibilní, má nutně kořen? #flashcard 
Ano, musí. Vychází to z tvrzení: $p(x)$ má stupeň 2 nebo 3 a nemá kořen, pak je ireducibilní. (Vyzkoušej dokázat, to tvrzení pak obměnou implikace dokazuje proč to tak je. Až na polynomy stupně 1)
<!--ID: 1691168777851-->

