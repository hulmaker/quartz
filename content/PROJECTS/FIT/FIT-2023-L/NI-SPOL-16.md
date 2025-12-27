TARGET DECK: NI-SPOL-2023::NI-PDP
FILE TAGS: NI-SPOL-2023 NI-SPOL-16 NI-PDP

prev::[[NI-SPOL-15]]
next::[[NI-SPOL-17]]

## Výkonnostní měřítka paralelních algoritmů, PRAM model, APRAM model, škálovatelnost

# PRAM, APRAM

Popište výpočetní model Paralelní RAM (PRAM) #flashcard 
p procesorů s lokální pamětí + m sdílených paměťových buňek
Plně synchronizovaná SIMD - synchronně (všichni najednou, nebo čekej) READ/WRITE/LOCAL
Konflikty: řeší se jako podtřída PRAM modelu
* EREW: Exclusive Read Exclusive Write
* CREW: Concurrent R Exclusive W (současné čtení)
* CRCW: Concurrent R Concurrent W
	* Priority: Výsledná hodnota podle vlákna s nejvyšší prioritou
	* Arbitrary: náhodný výsledek
	* Common: zápis pouze pokud jsou zapisované hodnoty stejné ve všech vláknech
<!--ID: 1691578042103-->



Popište výpočetní model Asynchronní Paralelní RAM (APRAM) #flashcard 
Stejný jako PRAM, ale bez centrálních hodin
Je nutná explicitní synchronizace barierou v čase B(p) - (že se procesy nepřepisují musíme zajistit softwarem)
Doba přístupu do paměti **není jednotková**.
Lokální operace je v čase 1, globální READ/WRITE v čase d
Vyplatí se posílat sekvenci k po sobě jdoucích READ/WRITE, to je v čase d+k-1
<!--ID: 1691578042104-->



Jaké známe implementace bariery (synchronizační primitivum) #flashcard 
Centrální čítač: Proces dorazí k bariéře a inkrementuje centrální čítač. Pokud je hodnota čítaře stejná jako množství vláken, tak probudí ostatní. Jinak usne.
binární redukční strom: Je to v případě, že se provádí nějaká redukce. Proces dorazí k bariéře a čeká na výsledek redukce ve svém podstromu (signál od obou potomků). Pak se probudí a pošle signál rodiči.
<!--ID: 1691578042105-->



Paralelní čas, zrychlení, cena, efektivnost a paralelní optimalita výkonnosti #flashcard 
Horní sekvenční časová složitost: $SU(n)$
Paralelní:
* čas: $T(n, p)$ čas od začátku do konce paralelního výpočtu (výpočetní + komunikační kroky)
* cena: $C(n, p) = p\cdot T(n, p)$. Cenová optimalita pokud $C(n, p)=\mathcal{O}(SU(n))$
* zrychlení: $S(n, p) = \frac{SU(n)}{T(n, p)} \leq p$
* efektivnost: $E(n, p)=\frac{SU(n)}{C(n, p)} \leq 1$ je konstantní iff. $E(n, p) = \Omega(1)$
alg. je par-optimální, iff. má lin zrychlení iff. má konstantní efektivnost.
<!--ID: 1691578042106-->



# škálovatelnost


Amdalův zákon v kontextu paralelní škálovatelnosti #flashcard 
sekvenční alg. s časem $T_A(n)$ má sekvenční podíl $fs$ a paralelizovatelný podíl $1-fs$
Pro zrychlení platí ideálně:
$$S(n, p)=\frac{T_A(n)}{fs\cdot T_A(n) + \frac{1-fs}{p} \cdot T_A(n)}=\frac{1}{fs+\frac{1-fs}{p}}\leq \frac{1}{fs}$$
<!--ID: 1691578042108-->



Gustafsonův zákon v kontextu paralelní škálovatelnosti #flashcard 
udržováním správného poměru mezi p/n dosáhneme limitně lineárního zrychlení
$$\lim_{n \to +\infty} S(n, p)=\frac{SU(n)}{T(n, p)}=p$$
když budeme takhle škálovat, t_seq bude konstantní, kdežto t_par bude škálovat lineárně.
Kde $S(n, p)$ je par. zrychleni, $SU$ je sekvencni a $T$ paralelni slozitost
<!--ID: 1691578042109-->



Paralelní škálovatelnost: co to je? Silná a slabá škálovatelnost #flashcard 
Schopnost algoritmu držet si svou efektivitu při různých n a p
Silná škálovatelnost: jak rychle klesá par. efektivita s rostoucím p a fixním n
Slabá škálovatelnost: definuje, jak se mění paralelní čas pro fixní n/p. Alternativně: měřítko růstu n takového, že při rostoucím p zůstává efektivnost stejná
<!--ID: 1691578042110-->



Co jsou izoefektivní funkce v kontextu paralelního škálování? #flashcard 
Je-li dána konstanta $0<E_0<1$, pak izoefektivni funkce:
$\psi_1(p)$ je asymptoticky minimální fce. tž. $\forall n_p=\Omega\left(\psi_1(p)\right): E\left(n_p, p\right) \geq E_0$
$\psi_2(n)$ je asymptoticky maximální fce. tž. $\forall p_n=\mathcal{O}\left(\psi_2(n)\right): E\left(n, p_n\right) \geq E_0$
 Pozn.
$\psi_1(p)$ - do jaké velikosti problému budu s p proc. dobře škálovat. Efektivnost klesne pod E0
$\psi_2(n)$ - kolik musím mít proc. abych dobře škáloval. Kolik nejvíc proc můžu mít, abych nesnížil efektivnost
<!--ID: 1691578042111-->
