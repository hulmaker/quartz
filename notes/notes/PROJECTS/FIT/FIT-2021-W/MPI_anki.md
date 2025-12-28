xxx TARGET DECK: ni-mpi-anki
xxx FILE TAGS: ni-mpi-anki

Existuje nad konečným tělesem polynom $p(x)$ (řádu většího jak 1) co má kořen a je ireducibilní? Pokud ano, jaký? #flashcard 
Pokud $deg(p(x)) > 1$, pak neexistuje. Polynom co má kořen nemůže být ireducibilní. Polynomial factor theorem:  $p(x)=(x-k)g(x)$, platí právě když $k$ je kořen $p(x)$ a $deg(f) = deg(g(x))+1$.  No a protože $deg(p(x)) > 1$, tak $deg(g(x)) > 0$ a tím pádem máme rozklad polynomu p(x).
<!--ID: 1643366720731-->



Polynom $p(x) \in T[x]$ stupně $n$ nemá kořen. V jakém případě platí $p(x) = (x-k)g(x)$, kde $g(x) \in T[x]$ je polynom stupně $n-1$ a $k \in T$ . A proč tomu tak je? #flashcard 
**V žádném**. Polynomial factor theorem nám říká, že takový rozklad existuje právě když je $k$ kořenem polynomu $p(x)$.
<!--ID: 1643366720737-->



$f(x), g(x) \in T[x]$ jsou nenulové polynomy z tělesa $T$. Platí $deg(f(x)) = 42$. Jakého stupně musí být polynom $g(x)$, aby měl polynom $f(x) \cdot g(x)$ stupeň 708? #flashcard 
$deg(g(x))=666$, protože podle lemma o násobení polynomů platí $deg(f(x) \cdot g(x))=deg(f(x)) + deg(g(x))$
<!--ID: 1643366720743-->



Jak budete postupovat, když budete chtít zjistit, zda-li je polynom $p(x) \in T[x]$ ireducibilní? #flashcard 
1. Pokud $deg(p(x)) > 1$ a $p(x)$ má kořen, pak není ireducibilní.
2. Podle lemma o násobení polynomů najdu možné stupně faktorů $q(x), g(x)$.
3. Většinou zbydou tak 2 dvojice možných stupňů.
4. Pro ty stupně si najdeme ireducibilní polynomy (většinou lehké) a dělíme $p(x)$.
5. Pokud žádný z nich nedělí $p(x)$ beze zbytku, pak je $p(x)$ ireducibliní.
<!--ID: 1643366720749-->



Polynom $p(x) \in T[x]$ nemá kořen. Je ireducibilní? #flashcard 
Záleží na stupni $p(x)$. Pokud má $p(x)$ stupeň 2 nebo 3 a nemá kořen, tak je ireducibilní. (Vyzkoušej dokázat)
Jinak **nevíme**. Když kořen nemá, tak to nutně neznamená, že je ireducibilní. Víme ale, že kdyby kořen měl a jeho stupeň by byl větší něž jedna, pak by ireducibilní nebyl.
<!--ID: 1643366720754-->


Musí platit, že každý polynom nad tělesem T, který má stupeň menší nebo roven třem a není ireducibilní, má nutně kořen? #flashcard 
Ano, musí. Vychází to z tvrzení: $p(x)$ má stupeň 2 nebo 3 a nemá kořen, pak je ireducibilní. (Vyzkoušej dokázat, to tvrzení pak obměnou implikace dokazuje proč to tak je. Až na polynomy stupně 1)
<!--ID: 1643366720760-->



Vyjmenuj hierarchii množin s jednou binární operací (grup) #flashcard 
Abelovská grupa (komutativita) $\subset$ grupa (inverze) $\subset$ monoid (neutrál) $\subset$ pologrupa (asociativita) $\subset$ grupoid (uzavřenost).
<!--ID: 1643366720769-->



Dejte předpis pro integrál funkce nad oblastí definované na obrázku. ![[MPI_integral_oblast.png]] #flashcard 
![[MPI_integral_oblast_reseni.png]]
<!--ID: 1643366720782-->



Popište Bézoutovu rovnost pro polynomy. #flashcard 
$f(x), g(x) \in T[x]$ jsou nenulové polynomy nad tělesem T. Pak existují $u(x), v(x) \in T[x]$ tak, že $gcd(f(x), g(x)) = u(x)f(x) + v(x)g(x)$
<!--ID: 1643366720792-->




Popište polynomial factor theorem. #flashcard 
$p(x) \in T[x]$ je polynom stupně n z tělesa $T$. Prvek $k \in T$ je kořen polynomu $p$ právě tehdy, když $p(x) = (x-k)g(x)$, kde $g(x) \in T[x]$ je supně $n-1$.
<!--ID: 1643366720802-->




Popište jak najít $(2x)^{-192}$ v $GF(3^4)$ s násobením mod $p(x)$. #flashcard 
1. Zjednodušit: $(2x)^{192} = 2^{192} \cdot x^{192} = 1 \cdot x^{2\cdot80} \cdot x^{32} = x^{32}$.
2. Pro výraz $x^{32}$ najdeme pomocí čtverců základní tvar. Pomůžeme si tak, že spočítáme $x^6, x^5, x^4$, to potom dosazujeme a nemusíme pokaždé dělit.
3. Pomocí EEA najdeme inverzi k základnímu tvaru $x^{32}$.
<!--ID: 1643366720811-->




Je průnik podgrup grupa? #flashcard 
Ano, výsledná podgrupa zůstane uzavřená vůči operaci. Operace zůstane asociativní, neutrální prvek zůstane stejný.
<!--ID: 1643366720820-->



Máma grupu $G=(M, \circ)$ a $N \subset M$. Jak v $\mathcal{O}(n)$, popř. v $\mathcal{O}(n^2)$ krocích rozhodneme, zda-li je $H=(N, \circ)$ podgrupa $G$? #flashcard 
$H$ je podgrupa $G$, právě když pro každé $a, b \in N$ platí $a \circ b^{-1} \in N$. Pokud známe inverze, tak stačí $\mathcal{O}(n)$. Pokud inverze nemáme, tak můžeme proiterovat pro každý prvek celou množinu $\mathcal{O}(n^2)$ .
<!--ID: 1643366720830-->


