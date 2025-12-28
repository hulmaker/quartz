TARGET DECK: Obsidian::math
[[NI-SPOL-01]], [[NI-SPOL-02]], [[NI-SPOL-03]], [[NI-SPOL-04]], [[NI-SPOL-05]]

# Teorie Grup - Grupoidy, Pologrupy, Monoidy a Grupy

Popiš hierarchiii struktur v teorii grup. #flashcard 
**Grupoid** -  je uspořádaná dvojice $(M, \circ)$, kde $M$ je libovolná neprázdná množina a $\circ$ je binární operace na $M$.
**Pologrupa** - je grupoid $(M, \circ)$, pro který je $\circ$ asociativní operace
**Monoid** - je pologrupa $(M, \circ)$, ve které existuje neutrální prvek $e \in M$ takový, že $\forall a \in M$ plati $e \circ a = a \circ e = a$
**Grupa** - je monoid $(M, \circ)$, ve kterém ke každému $a \in M$ existuje inverzní prvek $a^{−1} \in M$ takový, že $a^{−1} \circ a = a \circ a^{−1} = e$
**Komutativni (abelovska) grupa** - je grupa $(M, \circ)$, kde $\circ$ je komutativní operace.
<!--ID: 1729010154118-->



Rozhodni o $(\mathbb{Z}, +)$ je to Grupoid, pologrupa, monoid, grupa, abelovska grupa? #flashcard 
platí asociativní i komutativní zákon, neutrálním prvkem je 0 a inverze k prvku b je $b^{−1} = −b$, součet dvou celých čísel je celé číslo, jedná se tedy o abelovskou grupu.
<!--ID: 1729010154119-->


## Cyklické Grupy a Jejich Generátory.

Co značí řád grupy, jaký platí vztah mezi řádem grupy a podgrupy? #flashcard 
Řád grupy $G = (M, \circ)$ nazýváme počet prvků množiny $M$ .
Je-li $M$ nekonečná množina, je i řád nekonečný. Podle řádu rozlišujeme konečné a nekonečné grupy.
Řád grupy $G$ značíme symbolem $\#G$
Buď $H$ podgrupa konečné grupy $G$. Potom řád $H$ dělí řád $G$. (Lagrangeova věta)
<!--ID: 1729010154120-->



Definuj cyklickou grupu. Definuj co je generátor cyklické grupy. #flashcard 
Grupa G = (M, ◦) se nazývá cyklická, pokud existuje prvek a ∈ M
takový, že ⟨a⟩ = G. Tomuto prvku se říká generátor cyklické grupy G
<!--ID: 1729010154121-->



Malá Fermatova věta (Klíčová slova: grupa, řád grupy, neutrální prvek) #flashcard 
Pro libovolné prvočíslo $p$ a libovolné $1 \leq a < p$ platí: $a^{p-1} \equiv 1$ (mod p)
Důkaz:
* V grupě $G = (M, ◦)$ řádu $n$ platí pro všechny prvky $a \in M$ , že $a^n = e$, kde $e$ je neutrální prvek.
* Gupa $\mathbb{Z}^{\times}_p$ má řád $p − 1$ a už víme, že je cyklická.
* Aplikováním předchozí věty na tuto grupu získáme malou Fermatovu větu
<!--ID: 1729010154122-->



Jaké aplikace má teorie grup v kryptografii? #flashcard 
1. Problém diskrétního logaritmu: Hledání celého čísla $1\leq k \leq n$ v cyklické grupě řádu $n$, kde $\alpha$ je generator a $\beta$ je nejaky prvek. . Lze uvažovat dva případy:
*  Grupa $(M, \cdot)$, kde $k$ splňuje:  $\alpha^k=\beta$
*  Grupa $(M, +)$, kde $k$ splňuje:  $k\times\alpha=\beta$
2. Diffie-Hellman Key Exchange: Mocnění v $\mathbb{Z}_p^\times$ je snadné, ale jeho inverze (diskrétní logaritmus) náročná.
$$
	\begin{aligned}
	& k_{A B} \equiv\left(\alpha^b\right)^a \equiv \alpha^{a b} \\
	& k_{A B} \equiv\left(\alpha^a\right)^b \equiv \alpha^{a b}
	\end{aligned}
$$
<!--ID: 1729010154123-->



Kolik je generátorů v cyklické grupě řádu $n$? #flashcard 
Je jich $\varphi(n)$, kde $\varphi$ je Eulerova funkce, která každému přirozenému číslu n přiřazuje počet přirozených čísel menších než n, která jsou s ním nesoudělná.
* pro prvočíslo $p$ je $\mathbb{Z}^{\times}_p$ cyklická grupa řádu $p − 1$ a má tedy $\varphi(p-1)$ generátorů.
<!--ID: 1729010154124-->



Definuj řád prvku v cyklické grupě. #flashcard 
Buď $g$ prvek grupy $G$. Pokud existuje kladné přirozené číslo $m$ splňující $g^m = e$, pak nejmenší $m$ s touto vlastností nazýváme řádem prvku $g$. Pokud takové $m$ neexistuje, pak řekneme, že řád prvku $g$ je nekonečno. Řád prvku $g$ značíme $ord(g)$.
Řád prvku $g$ je roven řádu grupy ⟨g⟩.
<!--ID: 1729010154125-->


# Tělesa a okruhy

Definuj okruh (ring) a těleso (field) z teorie grup #flashcard 
Buďte M neprázdná množina a + a · binární operace na této množině. Řekneme,
že trojice R = (M, +, ·) je okruh, pokud platí:
* (M, +) je abelovská grupa,
* (M, ·) je monoid,
* platí (levý a pravý) distributivní zákon: $(\forall a, b, c \in M)(a \cdot(b+c)=a \cdot b+a \cdot c \wedge (b+c) \cdot a=b \cdot a+c \cdot a)$
Okruh T = (M, +, ·) se nazývá těleso, jestliže $(M \text{\\} \{0\}, ·)$ je abelovská grupa. Tuto grupu nazýváme multiplikativní grupou tělesa T.
(Dej pozor na to, ze musis vyjmout nulovy prvek!!!)
<!--ID: 1729010154126-->


## Konečná Tělesa, Okruhy Polynomů

Definuj okruh polynomů (teorie grup ) #flashcard 
Buď okruh $R$ a $a_i \in R, i = 0, 1, ..., n$. Potom množina všech polynomů nad okruhem $R$ spolu s operacemi sčítání a násobení definovanými předpisy
$$
\begin{aligned}
\sum_{i=0}^n a_i x^i+\sum_{i=0}^n b_i x^i & :=\sum_{i=0}^n\left(a_i+b_i\right) x^i \\
\left(\sum_{j=0}^n a_j x^j\right) \cdot\left(\sum_{k=0}^m b_k x^k\right) & :=\sum_{i=0}^{n+m}\left(\sum_{j+k=i} a_j b_k\right) x^i
\end{aligned}
$$
kde $a_i, b_i \in R$ pro všechny hodnoty i, tvoří okruh polynomů nad okruhem R. Tento okruh značíme $R[x]$.
<!--ID: 1729010154127-->



Popište polynomial factor theorem. (teorie grup) Uvažujme polynom $p(x) \in T[x]$ stupně $n$. #flashcard 
$p(x) \in T[x]$ je polynom stupně n z tělesa $T$. Prvek $k \in T$ je kořen polynomu $p$ právě tehdy, když $p(x) = (x-k)g(x)$, kde $g(x) \in T[x]$ je supně $n-1$.
Zároveň platí: $p(k) = 0$
<!--ID: 1729010154128-->



Popište lemma o násobení polynomů a lemma o dělění polynomů (teorie grup) #flashcard 
$f(x), g(x) \in T[x]$ jsou nenulové polynomy z tělesa $T$. Pak platí:
* $deg(f(x) \cdot g(x))=deg(f(x)) + deg(g(x))$
* Existují jednoznačně určené polynomy ($q(x), r(x) \in T[x]): f(x) = q(x)g(x)+r(x)$
<!--ID: 1729010154129-->



# Funkce více proměnných: gradient, Hessián, definitnost matic, extrémy funkcí více proměnných bez omezení a s rovnostními omezeními.


Derivace ve směru $v \in \mathbb{R}^{n, 1}$ v bodě $b = (b_1, \ldots b_n) \in D_f$ #flashcard 
Nechť $v \in \mathbb{R}^{n, 1} = \mathbb{R}_n, ||v|| = 1$. Derivace funkce $f$ ve směru $v$ v bodě $b \in D_f$ takovém, že
 $\exists H(b) \subset D_f$, je
$$\nabla_{\mathbf{v}} f(\mathbf{b})=\lim _{h \rightarrow 0} \frac{f(\mathbf{b}+h \mathbf{v})-f(\mathbf{b})}{h}$$
Pokud jsou všechny parciální derivace funkce $f$ na nějakém okolí bodu $b$ spojité, tak navíc platí:
$\nabla_{\mathbf{v}} f(\mathbf{b})=\nabla f(\mathbf{b}) \cdot \mathbf{v}$
<!--ID: 1729010154130-->



Definujte gradient funkce $f$ v bodě $b \in D_f$ #flashcard 
Gradient funkce $f$ v bodě $b \in D_f$ je vektor
$$\nabla f(\mathbf{b})=\left(\frac{\partial f}{\partial x_1}(\mathbf{b}), \frac{\partial f}{\partial x_2}(\mathbf{b}), \ldots, \frac{\partial f}{\partial x_n}(\mathbf{b})\right)$$
<!--ID: 1729010154131-->



Jaká je nutná podmínka existence lokálního extrému funkce $f$ v bodě $b$. Jak poznáme co za extrém to je? #flashcard 
**Nutná podmínka existence lok. extrému:**
Nechť má funkce $f : D_f \to \mathbb{R}, D_f \subset \mathbb{R}^n$, v bodě $b$ parciální derivaci podle i-té proměnné. Pokud $f$ má v bodě $b$ lokální extrém, potom:
$$\frac{\partial f}{\partial x_i}(\mathbf{b})=0$$
**Typ extrému:**
Platí nutná podmínka existence lokálního extrému. Necht $\mathbf{b} \in D_f$ je stacionární bod funkce $f: D_f \rightarrow \mathbb{R}, D_f \subset$ $\mathbb{R}^n$. Necht existuje okolí $H(\mathbf{b}) \subset D_f$ takové, že $f$ má na $H(\mathbf{b})$ spojité všechny druhé parciální derivace, potom
- je-li b lokální minimum, pak $\nabla^2 f(\mathbf{b})$ je pozitivně semidefinitní;
- je-li b lokální maximum, pak $\nabla^2 f(\mathbf{b})$ je negativně semidefinitní.
<!--ID: 1729010154132-->



Rozepiš definitivnost matic. Pozitivně/negativně (semi)definitní #flashcard 
Definice 4.5 - Definitnost matic. Mějme $\mathbf{A} \in \mathbb{R}^{n, n}$. Řekneme, že matice $\mathbf{A}$ je
1. pozitivně semidefinitní, pokud $\mathbf{x}^T \mathbf{A x} \geq 0$ pro $\forall \mathbf{x} \in \mathbb{R}^{n, 1}$;
2. pozitivně definitní, pokud $\mathbf{x}^T \mathbf{A x}>0$ pro $\forall \mathbf{x} \in \mathbb{R}^{n, 1}, \mathbf{x} \neq 0$;
3. negativně semidefinitní, pokud $\mathbf{x}^T \mathbf{A x} \leq 0$ pro $\forall \mathbf{x} \in \mathbb{R}^{n, 1}$;
4. negativně definitní, pokud $\mathbf{x}^T \mathbf{A x}<0$ pro $\forall \mathbf{x} \in \mathbb{R}^{n, 1}, \mathbf{x} \neq 0$;
5. indefinitní, pokud není pozitivně ani negativně semidefinitní.
<!--ID: 1729010154133-->



Souvislost definitivnosti matic a jejich vlastních čísel. #flashcard 
Buď $A \in R^{n,n}$ symetrická matice. Potom platí následující:
* Matice $A$ je pozitivně semidefinitní právě tehdy, když všechna její vlastní čísla jsou nezáporná.
* Matice $A$ je pozitivně definitní právě tehdy, když všechna její vlastní čísla jsou kladná.
* Matice $A$ je negativně semidefinitní právě tehdy, když všechna její vlastní čísla jsou nekladná.
* Matice $A$ je negativně definitní právě tehdy, když všechna její vlastní čísla jsou záporná.
* Matice $A$ je indefinitní právě tehdy, když má alespoň jedno kladné a alespoň jedno záporné vlastní číslo.
<!--ID: 1729010154134-->



Matice je indefinitní. Má pak na diagonále dva prvky s různým znaménkem? #flashcard 
Ne nutně. Ta implikace funguje obráceně.
Má li matice na diagonále dva prvky s různým znaménkem, pak je indefinitní.
<!--ID: 1729010154135-->



Postačující podmínka existence lokálního extrému a sedlového bodu. #flashcard 
Nechť $\mathbf{b} \in D_f$ je stacionární bod funkce $f: D_f \rightarrow \mathbb{R}, D_f \subset \mathbb{R}^n$. Nechť existuje okolí $H(\mathbf{b}) \subset D_f$ takové, že $f$ má na $H(\mathbf{b})$ spojité všechny druhé parciální derivace, potom:
- je-li $\nabla^2 f(\mathbf{b})$ pozitivně definitní, pak **b** je ostré lokální minimum;
- je-li $\nabla^2 f(\mathbf{b})$ negativně definitní, pak **b** je ostré lokální maximum;
- je-li $\nabla^2 f(\mathbf{b})$ indefinitní, pak **b** je sedlový bod.
<!--ID: 1729010154136-->



Co je to krácení v kontextu strojových čísel? Lze se mu vyhnout? #flashcard 
Krácení je ztráta platných cifer, kde které dochází typicky při odčítání. Má nejhorší vliv na chybu ze všech možných jiných ztrát.
Nechť $x$ a $y$ jsou normalizovaná strojová čísla a platí $x > y > 0$. Pokud $2^{−p} \leq 1 − \frac{y}{x} \leq 2^{−q}$ pro nějaká kladná celá $p$ a $q$, tak platí, že nejvíce $p$ a nejméně $q$ platných binárních bitů je ztraceno při provedení odečítání $x − y$.
Krácení se lze vyhnout několika technikami: (teoreticky se jím můžeme zbavit jiné chyby :D )
* přeformulováním problému tak, aby nedocházelo k odečítání
* použitím rozvojů funkcí do řad (např. do Taylorovy řady)
* použitím jiných rovností …
* (použitím přesné aritmetiky)
<!--ID: 1729010154137-->
