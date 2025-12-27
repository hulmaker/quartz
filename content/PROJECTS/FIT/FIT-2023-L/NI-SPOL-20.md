TARGET DECK: NI-SPOL-2023::NI-PDP
FILE TAGS: NI-SPOL-2023 NI-SPOL-20 NI-PDP

prev::[[NI-SPOL-19]]
next::[[NI-ZI-01]]

# Paralelní algoritmy pro redukci, prefixový součet a segmentový prefixový součet na PRAM, v ortogonálních, hyperkubických a obecných topologiích, aplikace.


Paralelní redukce - obecná implementace #flashcard
Vstupem je pole a asociativní binární operace. Výstupem je číslo.
Redukce je hyperkubický alg. složitost je vždy $\mathcal{O}(\log n)$ - pokaždé se půlí počet buněk.
Škálovatelnost: $\psi_1(p)= p \log p, \quad \psi_2(n) = n \log n$
<!--ID: 1692825194559-->



Paralelní redukce v MPI #flashcard 
`MPI_Reduce(sendbuf, recvbuf, count, datatype, operace, int root, MPI_Comm)`
MPI má 8 opercí, je dána parametrem, lze si definovat svoje
Lze provést in place: Reduce_IN_PLACE
`MPI_Allreduce()`: Je to stejné, ale výsledek se uloží ve všech procesech
<!--ID: 1692825194565-->



Paralelní redukce v OpenMP #flashcard 
U cyklu lze použít klausuli reduce, ve které se uvede proměnná a operace
* V každé iteraci se vypočte hodnota proměnné, která je postupně redukována
* Výsledek redukce se do proměnné v masteru
* Pro reduction lze použít pouze skalární proměnné a několik základních aritmetických a logických operátorů
* Redukce je buď lineární (vhodná pro málo vláken) nebo logaritmická
<!--ID: 1692825194568-->



Paralelní redukce v různých topologiích #flashcard 
![[par_redukce.png]]
<!--ID: 1692825194572-->



Paralelní prefixový součet (scan) - na EREW PRAM #flashcard 
Vstup: Pole a binární asociativní komutativní operace
Výstup: Pole prefixových součtů (poslední odpovídá výsledku paralelní redukce)
![[PPS.png]]
Na PRAM se počítá in-place v $\mathcal{O}(\log n)$
Na APRAM v $\mathcal{O}(\log n \cdot \log n)$ (po každém kroku voláme bariéru) $T(n, p)=\alpha n / p+\beta \log ^2 p$
<!--ID: 1692825194575-->



Paralelní prefixový součet ve stromu, motýlku, na mřížkách a v hyperkrychli #flashcard 
**Nepřímý strom**: $\mathcal{O}(\log n)$
* Data v listech, uzly počítají. Potřebujeme 2*výška kroků.
* Vzestupná vlna - sečtu potomky, pošlu nahoru.  Do pravého potomka uložim hodnotu levého potomka
* Sestupná vlna: Shora dorazí hodnota, tu pošlu do potomků, v listech se hodnoty sečtou. V každém listu bude všechno co je od něj nalevo.
**Přímý strom**: Hodnoty do uzlů umístíme postorder, použijeme alg. pro nepřímý strom.
**Motýlek**: Jde tam najít strom jako kostra. Proveď předchozí algoritmus.
**hyperkrychle**: počítáme prefixový součet podle lexikograficky seřazených vrcholů - postupně pro sousedy podle dimenze (oba změry). Každý vrchol má 2 hodnoty. Do jedné přičítá od všech, do druhé jen od těch s nižším id.
**SF Mřížka**: Iteruju a sčítám: vodorově, pak svisle, zas vodorovně a hotovo
**WH Mřížka**: Ve dvou fázích simuluju strom (vertikálně, horizontlně) (stejně jako pro hyperkrychli podle lexikograficky seřazených vrcholů přičítám nižší index)
<!--ID: 1692825194578-->



Škálovatelnost paralelního prefixového součtu #flashcard 
stejná jako paralelní redukce. procesory dostanou na začátku více čísel.
Nejdřív se udělá lokální prefixový součet a potom globální. 
prakticky je to součet na mřížce, ale řádek je lokální pole čísel.
$T(n, p)=O(n / p)+O(\log p)$
<!--ID: 1692825194581-->



Zhušťovací problém (Packing Problem) v kontextu paralelních redukcí #flashcard 
Výpočet pořadí v distribuované podmnožině. Na procesory jsou namapována nějaká data (my pro jednoduchost bereme čísla z {0, 1})
* Máme nějaké podmnožiny, procesory vědí, jestli do množiny patří (0/1), ale neví nic o sousedech ani ostatních procesorech
* Potřebujeme očíslovat prvky v rámci celého systému - to je prefixový součet nad binárním polem (nebo nad charakteristickou množinou jiných čísel)
<!--ID: 1692825194583-->



Paralelní radix sort #flashcard 
Mám čísla o n bitech, řadím je podle souřadnic - dělám dokola zhušťování pro všechny souřadnice (n-krát)
Na logaritmických sítích  (např. $oBF_n$) to jde v $\mathcal{O}\left(\log ^2 N\right)$
<!--ID: 1692825194588-->



Paralelní binární sčítačka s predikcí přenosu #flashcard 
Aplikace paralelního prefixového součtu.
Pro každý bit si napočítám $s, p, g$ (stop-dvě nuly, propagate - záleží, generate - dvě jedničky)
1. pro sčítance provedu AND, $\lnot$AND, XOR
2. Nad s, p, g dělám prefixový součet podle definované operace $\odot$
$$
\begin{array}{c|ccc}
\odot & s & p & g \\
\hline s & s & s & s \\
p & s & p & g \\
g & g & g & g
\end{array}
$$
<!--ID: 1692825194591-->



Tridiagonální systém rovnic v kontextu paralelních redukcí #flashcard 
přepíšu si řádek i-tý řádek $f_i x_{i-1}+g_i x_i+h_i x_{i+1}=b_i$ na rekurentní tvar:
$$
\left[\begin{array}{c}
x_{i+1} \\
x_i \\
1
\end{array}\right]=\mathcal{G}_i\left[\begin{array}{c}
x_i \\
x_{i-1} \\
1
\end{array}\right]
$$
$$
\mathcal{G}_i=\left[\begin{array}{ccc}
-\frac{g_i}{h_i} & -\frac{f_i}{h_i} & \frac{b_i}{h_i} \\
1 & 0 & 0 \\
0 & 0 & 1
\end{array}\right]
$$
a musíme aplikovat opakovaně substituci
<!--ID: 1692825194593-->



Segmentový paralelní prefixový součet (SPPS) #flashcard 
Vstup: pole rozdělené libovolně do segmentů
Výstup: prefixové součty uvnitř těchto segmentů izolovaně
Myšlenka: Počítám PPS, ale u čísel si držím příznak jestli jsou první v segmentu. Pokud ano, tak se do něj nepřenáší hodnota zleva. 
Implementace je tak jen v upravení binární operace.
<!--ID: 1692825194596-->



Aplikace segmentového paralelního prefixového součtu na paralelní quicksort #flashcard 
Rozdělování čísel podle pivota je zhušťování. Ale protože se při quicksortu pole dělí na segmenty, tak musí být zhušťování segmentové.
Kategorie pro zhušťování: 0 - menší než pivot, 1 - rovný pivotu, 2 - větší než pivot
<!--ID: 1692825194600-->



