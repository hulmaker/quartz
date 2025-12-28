TARGET DECK: Obsidian::CS

[[NI-SPOL-16]], [[NI-SPOL-17]], [[NI-SPOL-18]], [[NI-SPOL-19]], [[NI-SPOL-20]]

Popište následující výkonnostní měřítka paralelních algoritmů pro $p$ procesorů: Paralelní čas, zrychlení, cena, efektivnost a paralelní optimalita výkonnosti #flashcard 
Horní sekvenční časová složitost: $SU(n)$
Paralelní:
* čas: $T(n, p)$ čas od začátku do konce paralelního výpočtu (výpočetní + komunikační kroky)
* cena: $C(n, p) = p\cdot T(n, p)$. Cenová optimalita pokud $C(n, p)=\mathcal{O}(SU(n))$
* zrychlení: $S(n, p) = \frac{SU(n)}{T(n, p)} \leq p$
* efektivnost: $E(n, p)=\frac{SU(n)}{C(n, p)} \leq 1$ je konstantní iff. $E(n, p) = \Omega(1)$
alg. je par-optimální, iff. má lin zrychlení iff. má konstantní efektivnost.
<!--ID: 1729010154090-->



Jaké znáte synchronizační direktivy? Odpověď je formulována v programovém modelu OpenMP. Stačí ale intuice. #flashcard 
* **barrier**: paralelní vlákna daného regionu zde čekají na ostatní.
* **master**: blok kódu smí provést pouze master
* **single**: blok kódu smí provést pouze jedno libovolné vlákno.
* **critical**: vytvoření kritické sekce (mutex), lze ji pojmenovat
* **atomic**: atomic. mutex nad paměťovou buňkou (jednovláknově a nepřerušitelně)
* **flush()**: propsání aktuálních hodnot sdílených proměnných do sdílené paměti
* **taskwait**: synchronizace synovských úloh s rodičovskou v task paralelismu
<!--ID: 1729010154091-->



Jaké známe implementace bariery (synchronizační primitivum) #flashcard 
- **Centrální čítač**: Proces dorazí k bariéře a inkrementuje centrální čítač. Pokud je hodnota čítaře stejná jako množství vláken, tak probudí ostatní. Jinak usne.
- **binární redukční strom**: Je to v případě, že se provádí nějaká redukce. Proces dorazí k bariéře a čeká na výsledek redukce ve svém podstromu (signál od obou potomků). Pak se probudí a pošle signál rodiči.
<!--ID: 1729010154092-->



jaký je rozdíl mezi datovým a funkčním paralelismem? (data a task parallelism) Kontext: paralelní a distribuované programování #flashcard 
**Data parallelism**:
- Procesory provádí výpočet na nějaké prostorové subdoméně - bloku paměti.
- Na konci cyklu je bariera a redukce výsledků.
**Task parallelism**:
Program je rozdělen na úkoly (task pool, tvoří graf (DAG))
* vhodné pro rekurzi - producent, konzument
<!--ID: 1729010154093-->



Co je falešné sdílení (false sharing) v kontextu paralelního a distribuovaného programování? Jaké má řešení? #flashcard 
Vlákna sice zapisují na různé adresy, ale adresy jsou si tak blízké, že jsou ve stejném bloku cache. Zápis způsobí výpadek cache a program je mnooohem pomalejší z důvodu delšího přístupu do paměti.
řešení 1: při paralel for se přiděluje dost velký blok prvků pole
řešení2: umělé navýšení velikosti zapisovaných dat tak, aby obsadila celý blok.
<!--ID: 1729010154094-->



Do jakých kategorií dělíme přímé propojovací sítě paralelních počítačů vlastnosti? #flashcard 
**Ortogonální topologie**: Konstruktor je kartézský součin.
* Binární hyperkrychle - hypercube
* Mřížky - mesh
* Toroidy (zabalená mřížka) - tori
**Hyperkubické topologie**.
* motýlek - Řídká hyperkubická sít
* Tlusté stromy
**Closova topologie**
**Dragonfly topologie**
<!--ID: 1729010154095-->



Vyjmenujte důležité vlastnosti přímých propojovacích sítí paralelních počítačů. Jaké chceme aby ty vlastnosti byly a proč? #flashcard 
- **hustota**: řídké topologie jsou stupně uzlů omezeny konstantou. U husté rostou stupně společně s $n$.
- **diam**: nejdelší vzdálenost
- **bisekční šířka**: min cut - tedy min. počet disjunktních cest mezi vrcholy
- chceme aby byla síť hierarchicky rekurzivní
- konstatní stupeň uzlu s velikostí sítě (snadný routing)
<!--ID: 1729010154096-->

