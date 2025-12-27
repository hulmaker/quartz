TARGET DECK: NI-SPOL-2023::NI-MPI
FILE TAGS: NI-SPOL-2023 NI-SPOL-01 NI-MPI
# Teorie Grup - Grupoidy, Pologrupy, Monoidy a Grupy

Popiš hierarchiii struktur v teorii grup. #flashcard 
**Grupoid** -  je uspořádaná dvojice $(M, \circ)$, kde $M$ je libovolná neprázdná množina a $\circ$ je binární operace na $M$.
**Pologrupa** - je grupoid $(M, \circ)$, pro který je $\circ$ asociativní operace
**Monoid** - je pologrupa $(M, \circ)$, ve které existuje neutrální prvek $e \in M$ takový, že $\forall a \in M$ plati $e \circ a = a \circ e = a$
**Grupa** - je monoid $(M, \circ)$, ve kterém ke každému $a \in M$ existuje inverzní prvek $a^{−1} \in M$ takový, že $a^{−1} \circ a = a \circ a^{−1} = e$
**Komutativni (abelovska) grupa** - je grupa $(M, \circ)$, kde $\circ$ je komutativní operace.
<!--ID: 1691141660931-->


Rozhodni o $(\mathbb{Z}, +)$ je to Grupoid, pologrupa, monoid, grupa, abelovska grupa? #flashcard 
platí asociativní i komutativní zákon, neutrálním prvkem je 0 a inverze k prvku b je $b^{−1} = −b$, součet dvou celých čísel je celé číslo, jedná se tedy o abelovskou grupu.
<!--ID: 1691144079419-->



Rozhodni o $(\mathbb{R} \text{\\} \{0\}, \cdot)$ je to Grupoid, pologrupa, monoid, grupa, abelovska grupa? #flashcard 
platí asociativní i komutativní zákon, neutrálním prvkem je 1 a inverze k (automaticky nenulovému) prvku $b$ je $b^{−1} = 1/b$, součin dvou nenulových reálných čísel je nenulové reálné číslo, jedná se tedy o abelovskou grupu
<!--ID: 1691144079423-->



Kolik je v monoidu neutrálních prvků? Tvrzení podpořte důkazem. #flashcard 
V monoidu existuje právě jeden neutrální prvek.
Buď $(G, \circ)$ monoid a $e$ nějaký neutrální prvek (z definice víme, že tam alespoň jeden je!). Dokážeme sporem, že $e$ je jediný neutrální prvek.
Pro spor předpokládejme, že v monoidu existuje další neutrální prvek $\bar{e}$ různý od $e$. Potom platí $\bar{e} = \bar{e} = e = e$. Tím dostáváme spor s tím, že e a e jsou různé.
<!--ID: 1691144079427-->



Najděte grupu, ve které existuje prvek bez inverzního prvku. Najděte grupu, ve které existuje prvek s více inverzními prvky. #flashcard 
V grupě má každý prvek právě jeden inverzní prvek. Dokazuje se sporem, že $b$ je jediny inverzni prvek. Predpokladejme, ze c je jiny inverzni prvek ruzny od b. Potom plati:
$c = c \circ e = c \circ (a \circ b) = (c \circ a) \circ b = e \circ b = b$, kde $e$ je neutralni prvek. Mame spor ze c a b jsou ruzne.
<!--ID: 1691144079429-->



Cayleyho tabulka grupy - vlstnosti #flashcard 
* Pokud má množina konečný počet prvků $n$, lze zachytit v Cayleyho tabulce.
* Z tabulky lze odvodit uzavřenost, asociativita, neutrální prvek, inverzní prvek a komutativita.
* Tabulka pak tvoří latinský čtverec $n \times n$ (sloupce i řádky obsahují všechny prvky množiny) Dokazuje se to pres jednoznacnost deleni.
<!--ID: 1691144079432-->


## Podgrupy

Definuj podgrupu #flashcard 
$G=(M, \circ)$ je grupa. Podgrupa grupy $G$ je libovolna dvojice $H=(N, \circ)$ takova, ze:
* $N \subset M$
* $(N, \circ)$ je grupa
<!--ID: 1691144079435-->



Je průnik podgrup grupa? #flashcard 
Ano, výsledná podgrupa zůstane uzavřená vůči operaci. Operace zůstane asociativní, neutrální prvek zůstane stejný.
<!--ID: 1691144079437-->



Máme grupu $G=(M, \circ)$ a $N \subset M$. Jak v $\mathcal{O}(n)$, popř. v $\mathcal{O}(n^2)$ krocích rozhodneme, zda-li je $H=(N, \circ)$ podgrupa $G$? #flashcard 
$H$ je podgrupa $G$, právě když pro každé $a, b \in N$ platí $a \circ b^{-1} \in N$. Pokud známe inverze, tak stačí $\mathcal{O}(n)$. Pokud inverze nemáme, tak můžeme proiterovat pro každý prvek celou množinu $\mathcal{O}(n^2)$ .
<!--ID: 1691144079438-->



V grupe $G=(M, \circ)$ jsou alespon dva prvky. Kolik je v takove grupe minimalne podgrup. #flashcard 
Alespon dve:
* pouze neutralni prvek $(\{e\}, \circ)$
* grupa samotna $G=(M, \circ)$
Tyto grupy jsou trivialni podgrupy, ostatni jsou netrivialni nebo vlastni podgrupy.
<!--ID: 1691144079440-->



$G=(M, \circ)$ je grupa a $N\subset M$ je neprazdna mnozina. Dokaz, ze dvojice $H = (N, \circ)$ je podgrupa grupy $G$ prave kdyz $\forall a,b \in N: a \circ b^{-1} \in N$ #flashcard 
* Implikace zleva doprava je zřejmá. Ověřme implikaci zprava doleva.
* Operaci $\circ$ jsme nijak nezměnili a její asociativita je tedy zachována.
* Vezměme $a ∈ H$, potom $e = a \circ a^{−1} ∈ H$.
* Uvažme $a ∈ H$, potom $a^{−1} = e \circ a^{−1} ∈ H$.
* Pro $a, b ∈ H$ platí $a \circ b = a \circ (b^{−1})^{−1} ∈ H$.
<!--ID: 1691144079441-->


## Cyklické Grupy a Jejich Generátory.


Řád grupy #flashcard 
Řád grupy $G = (M, \circ)$ nazýváme počet prvků množiny $M$ . Je-li $M$ nekonečná
množina, je i řád nekonečný. Podle řádu rozlišujeme konečné a nekonečné grupy. Řád grupy $G$ značíme symbolem $\#G$
<!--ID: 1691145187995-->



Naznačte důkaz Lagrangeovy věty. (Klíčová slova: grupa, podgrupa, řád grupy, dělitelnost) #flashcard 
Buď $H$ podgrupa konečné grupy $G$. Potom řád $H$ dělí řád $G$.
1. V grupě $G$ definujeme relaci: $x \sim y$ pokud existuje $h \in H$ tak, že $x = yh$.
2. Ukážeme, že se jedná o ekvivalenci, tedy o reflexivní, symetrickou a tranzitivní relaci.
3. Jelikož se jedná o ekvivalenci, tvoří prvky $G$, které jsou v relaci $\sim$, třídy ekvivalence (viz např. předmět ZDM).
4. Jednou z těchto tříd ekvivalence je podgrupa $H$ (plyne z uzavřenosti $H$ vůči binární operaci).
5. Ukážeme-li, že všechny třídy ekvivalencí mají stejný počet prvků, je důkaz hotov, neb třídy ekvivalencí (jak známo) tvoří disjunktní rozklad množiny prvků grupy $G$.
6. Buďte $[a]_{\sim}$ a $[b]_{\sim}$ dvě různé třídy ekvivalence s reprezentanty $a$ a $b$. Definujeme zobrazení z $[a]_{\sim}$ do $[b]_{\sim}$ jako: $f(x) = ba^{−1}x$
7. Jelikož toto zobrazení má inverzi (viz vlastnost ”v grupě lze jednoznačně dělit“) $f^{−1}(y) = ab^{−1}y$, jedná se o bijekci a tedy $[a]_{\sim}$ a $[b]_{\sim}$ jsou skutečně stejně mohutné (mají stejně prvků).
* Tato věta spojuje abstraktní strukturu grupy s pojmem dělitelnosti a tedy i s pojmem prvočísla!
* Důsledek: Grupa s prvočíselným řádem má pouze triviální podgrupy!
<!--ID: 1691145188005-->


Sylowova věta (Klíčová slova: grupa, podgrupa, řád grupy, dělitelnost, prvčísla) #flashcard 
Buď $G$ grupa konečného řádu $n$ a číslo $p$ prvočíselný dělitel čísla $n$. Pokud $p^k$ dělí $n$
(pro $k$ přirozené), pak grupa $G$ obsahuje podgrupu řádu $p^k$.
<!--ID: 1691145937959-->



Definuj cyklickou grupu a její generator #flashcard 
Grupa G = (M, ◦) se nazývá cyklická, pokud existuje prvek a ∈ M
takový, že ⟨a⟩ = G. Tomuto prvku se říká generátor cyklické grupy G
<!--ID: 1691145937965-->


Definuj řád prvku v cyklické grupě. #flashcard 
Buď $g$ prvek grupy $G$. Pokud existuje kladné přirozené číslo $m$ splňující $g^m = e$, pak nejmenší $m$ s touto vlastností nazýváme řádem prvku $g$. Pokud takové $m$ neexistuje, pak řekneme, že řád prvku $g$ je nekonečno. Řád prvku $g$ značíme $ord(g)$.
Řád prvku $g$ je roven řádu grupy ⟨g⟩.
<!--ID: 1691160648528-->



Kdy je $\mathbb{Z}^{\times}_n$ cyklická? #flashcard 
$\mathbb{Z}^{\times}_n$ je cyklická, právě když $n$ je $2, 4, p^k$, nebo $2p^k$, kde $p$ je liché prvočíslo a $k$ je kladné přirozené číslo.
<!--ID: 1691160648531-->



(G, ◦) je cyklická grupa řádu $n$. A $a$ je nějaký její generátor. Za jakého předpokladu je $a^k$ také generátor? #flashcard 
Tehdy, a jen tehdy, když $k$ a $n$ jsou nesoudělná (tj. $gcd(k, n) = 1$). Víme, že $a^k$ je generátor, neb jím jde vygenerovat jiný generátor.
Důkaz pomocí lemma: Buď $D = \{mk + \ell n | m, \ell ∈ Z\}$ a $d = min\{|x| | x \in D \text{\\} \{0\}\}$, potom $d = gcd(k, n)$.
<!--ID: 1691160648534-->



Existuje podgrupa cyklické grupy, která není opět cyklické podgrupa? Pokud ano, nalezněte příklad #flashcard 
Ne, Libovolná podgrupa cyklické grupy je opět cyklická grupa.
Buď $G = ⟨a⟩$ cyklická grupa a $H$ její vlastní podgrupa. Buď $q \in N$ nejmenší nenulové číslo takové, že $a^q \in H$. Platí $⟨a^q⟩ \subset H$ a platí $H \subset ⟨a^q⟩$, potom $H = ⟨a^q⟩$. 
Buď $x$ nějaký prvek $H$ a $p$ takové, že $x = a^p$. Jistě existují $u, v$ tak, že $d = gcd(q, p) = uq + vp$. Potom $a^d \in H$ a tedy $d \geq q$, ale současně $d \leq q$, proto $d = q$ a existuje $k$ tak, že $p = kq$. Odtud konečně dostáváme $x = a^p = (a^q)^k \in ⟨a^q⟩$ 
<!--ID: 1691160648537-->



Malá Fermatova věta (Klíčová slova: grupa, řád grupy, neutrální prvek) #flashcard 
Pro libovolné prvočíslo $p$ a libovolné $1 \leq a < p$ platí: $a^{p-1} \equiv 1$ (mod p)
Důkaz:
* V grupě $G = (M, ◦)$ řádu $n$ platí pro všechny prvky $a \in M$ , že $a^n = e$, kde $e$ je neutrální prvek.
* Gupa $\mathbb{Z}^{\times}_p$ má řád $p − 1$ a už víme, že je cyklická.
* Aplikováním předchozí věty na tuto grupu získáme malou Fermatovu větu
<!--ID: 1691160648540-->



Dokažte následující větu: V grupě $G = (M, ◦)$ řádu $n$ platí pro všechny prvky $a \in M$ , že $a^n = e$, kde $e$ je neutrální prvek. #flashcard 
* Uvažujme tuto posloupnost prvků z $M : a, a^2, a^3, ...$
* Označme $q$ nejmenší číslo takové, že $a^q = e$. Jistě platí $q \leq n$ (Rozmyslet!).
* Množina $a, a^2, ... , a^q$ tvoří podgrupu $⟨a⟩$ řádu $q$. Dle Lagrangeovy věty tedy platí, že $q$ dělí $n$, tzn. že existuje $k \in N$ takové, že $n = qk$
* Máme tedy $a^n = a^{qk} = (a^q)^k = e^k = e$. 
<!--ID: 1691160648543-->



Kolik je generátorů v cyklické grupě řádu $n$? #flashcard 
Je jich $\varphi(n)$, kde $\varphi$ je Eulerova funkce, která každému přirozenému číslu n přiřazuje počet přirozených čísel menších než n, která jsou s ním nesoudělná.
* pro prvočíslo $p$ je $\mathbb{Z}^{\times}_p$ cyklická grupa řádu $p − 1$ a má tedy $\varphi(p-1)$ generátorů.
<!--ID: 1691160648547-->



Zadfinujte homomorfismus $G$ do $H$ pro grupoidy $G=(M, \circ_G)$ a $H=(M, \circ_H)$ #flashcard 
Je to zobrazeni $h: M \to N$, kde $\forall  x, y \in M$ platí $h(x \circ_G y) = h(x) \circ_H h(y)$
Je-li navíc $h$ injektivní, resp. surjektivní, resp. bijektivní, říkáme že $h$ je monomorfismus, resp. epimorfismus, resp. izomorfismus.
<!--ID: 1691160648550-->



Buď $h$ homomorfismus grupy $G = (M, \circ_G)$ do grupoidu $H = (N, \circ_H)$. Do jaké úrovně hierarchie struktur patří $h(G) \coloneqq (h(M ), \circ_H)$? #flashcard 
$h(G)$ je grupa. 
V důkazu se postupně ukáže, že v $h(G)$ platí asoc. zákon, existuje neutrální prvek a každý prvek má inverzi.
<!--ID: 1691160648553-->



Je pravda, že libovolné dvě nekonečné cyklické grupy jsou izomorfní? Je pravda, že pro  $\forall n \in N$ jsou libovolné dvě cyklické grupy řádu $n$ izomorfní? #flashcard 
Obě tvrzení jsou pravdivá.
Důkaz: náznak – doladit za domácí úkol. Buď 4 cyklická grupa s generátorem $a$. Ukážeme, že libovolná nekonečná cyklická grupa je izomorfní s grupou $(\mathbb{Z}, +)$ a že libovolná cyklická grupa řádu $n$ je izomorfní s $\mathbb{Z}_n^+$ Zbytek už plyne z tranzitivity relace ”být izomorfní“. 
Hledaný izomorfismus je bijekce $h(k) = a^k$ ...
<!--ID: 1691160648555-->



Je pravda, že libovolná konečná grupa je izomorfní s každou grupou permutací? #flashcard 
Není. Libovolná konečná grupa je izomorfní pouze s nějakou grupou permutací, ale neplatí to nutně pro všechny. Je to Cayleyova věta a důkaz je jen naznačen pro zájemce.
<!--ID: 1691160648558-->



Jaké aplikace má teorie grup v kryptografii? #flashcard 
1. Cyklická grupa řádu $n$, kde $\alpha$ je generator a $\beta$ je nejaky prvek. Hledání celého čísla $1\leq k \leq n$ je problem diskretniho logaritmu. Lze uvažovat dva případy:
*  Grupa $(M, \cdot)$, kde $k$ splňuje:  $\alpha^k=\beta$
*  Grupa $(M, +)$, kde $k$ splňuje:  $k\times\alpha=\beta$
2. Diffie-Hellman Key Exchange: Mocnění v $\mathbb{Z}_p^\times$ je snadné, ale jeho inverze (diskrétní logaritmus) náročná.
$$
	\begin{aligned}
	& k_{A B} \equiv\left(\alpha^b\right)^a \equiv \alpha^{a b} \\
	& k_{A B} \equiv\left(\alpha^a\right)^b \equiv \alpha^{a b}
	\end{aligned}
$$
<!--ID: 1691160648561-->
