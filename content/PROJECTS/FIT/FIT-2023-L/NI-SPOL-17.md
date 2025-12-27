TARGET DECK: NI-SPOL-2023::NI-PDP
FILE TAGS: NI-SPOL-2023 NI-SPOL-17 NI-PDP

prev::[[NI-SPOL-16]]
next::[[NI-SPOL-18]]

# Programování nad sdílenou pamětí

## programový model OpenMP


Programový model OpenMP a vlastnosti proměnných #flashcard 
`#pragma omp parallel num_threads(p)`
Explicitní model paralelního výpočtu (plná odpovědnost za běh). Vlákna komunikují přes sdílenou paměť. V sekvenčním kódu definujeme paralelní regiony, máme master vlákno.
Vlastnosti proměnných:
* shared - skalární proměnná je sdílena
* private - lokální, neinicializovaná instance
* firstprivate - lokální, inicializováno na hodnotu z masteru
* lastprivate - lokální, pouze cyklus, hodnota na konci se uloží do masteru
* reduction - po skončení regionu se hodnoty z vláken redukují (+, -, *, |,||, &, &&, ... )
* thread private - hodnota se přenáší mezi paralelními regiony (konst. poč. vláken)
<!--ID: 1691251771760-->



Programový model OpenMP - synchronizační direktivy #flashcard 
* barrier: paralelní vlákna daného regionu zde čekají na ostatní.
* master: blok kódu smí provést pouze master
* single: blok kódu smí provést pouze jedno libovolné vlákno.
* critical: vytvoření kritické sekce (mutex), lze ji pojmenovat
* atomic: atomic. mutex nad paměťovou buňkou (jednovláknově a nepřerušitelně)
* flush(): propsání aktuálních hodnot sdílených proměnných do sdílené paměti
* taskwait: synchronizace synovských úloh s rodičovskou v task paralelismu
<!--ID: 1691251771764-->


## datový a funkční paralelismus, synchronizace vláken


Programový model OpenMP - datový paralelismus #flashcard 
`#pragma omp parallel for schedule(...) shared(...)`
Prostředky jsou přidělené procesorům nezávisle. Na konci cyklu je bariera.
Klauzule:
* collapse(): paralelizace vnořených cyklů. Defaultne se vztahuje pouze na cyklus nejvyšší úrovně
* ordered: pořadí provádění iterací je stejné jako při sekvenčním provádění
* nowait: vlákna po dokončení svých iterací nečekají na bariéře.
* schedule(): 
	* static - bloky definovane velikosti pridel rovnomerne
	* dynamic - prideluj bloky o velikosti chunk-size dynamicky
	* auto - do magic
	* runtime - definovano env. promennou OMP_SCHEDULE
	* guided - Dynamicke prideleni, pocet bloku se meni podle toho kolik jich zbyva. Nejdriv hodne, potom malo.
<!--ID: 1691251771769-->



Programovy model OpenMP - taksovy paralelismus #flashcard 
`#pragma omp task if (cond)`
program je rozdelen na ukoly (task pool, tvori graf)
* vhodne pro rekurzi - producent, konzument
Direktivy: 
* taskwait - rodicovska uloha ceka na podukoly
* single - volani provede pouze jedno vlakno
<!--ID: 1691251771775-->


## vícevláknové algoritmy (násobení polynomů, násobení matic, řazení).


Co je falešné sdílení v kontextu paralelního a distribuovaného programování? Jaké má řešení? #flashcard 
Vlákna sice zapisují na různé adresy, ale adresy jsou si tak blízké, že jsou ve stejném bloku cache. Zápis způsobí výpadek cache.
řešení 1: při paralel for se přiděluje dost velký blok prvků pole
řešení2: umělé navýšení velikosti zapisovaných dat tak, aby obsadila celý blok.
<!--ID: 1691251771780-->



Vícevláknový algoritmus násobení polynomů #flashcard 
```cpp
int A[m+1],B[n+1],C[n+m+1];
for (int k = 0; k <= m + n, k++)
	C[k] = 0;
for (int i = 0; i <= m; i++)
	for (int j = 0; j <= n; j++)
		C[i+j] += A[i]*B[j];
```
Paralelizace:
* vnějšího cyklu - kritická sekce, synchronizace
* vnitřního cyklu - zmizí kritická sekce, vysoká režie, bariéra na konci každého cyklu, flešné sdílení.
* výpočtu disjunktních oblastí - paralelizujeme podle součtu indexů. V řádku jsou kombinace co dávají i+j (udělá to diamant). Přiděluje se pak několik řádků. chunk-size lze volit aby nedošlo k falešnému sdílení, plánujem dynamicky nebo střídavě.
<!--ID: 1691251771786-->



Vícevláknový algoritmus násobení matic #flashcard 
Paralelizujeme:
* i - po řádkách - nedochází k false sharing (jiný řádek zápisu), 1 bariera
* j - po sloupcích - dojde k false sharing (zápis do stejného řádku), bariera na konci každého i
* k - paralelní násobení, cyklus s redukcí (sčítání), nejvyšší režie vůbec
<!--ID: 1691251771792-->



Vícevláknový algoritmus řazení - QuickSort #flashcard 
Řeší se task paralelismem. rozdělení podle:
* Lomutov - i,j jde obojí zleva
* Hoare - i,j jdou proti sobě
Vylepšení:
* místo dvou volání zajistit koncovou rekurzi
* pro malé pole řešit sekvenčně
* použiji Hoare rozdělování, které lze paralelizovat
Paralelní rozdělování: lze paralelizovat po prvcích/blocích
* Vlákno dostane 2 bloky, které vzájemně vyčistí. Výsledkem jsou 1-2 čisté bloky
* Zbylé špinavé bloky se čistí sekvenčně.
* Nižší režie, min synch. min false sharing
<!--ID: 1691251771797-->



Vícevláknový algoritmus řazení - MergeSort #flashcard 
rozděluje a pak panuje na dost malých instancích - false sharing
Zajistíme minimální velikost pole, rozděl a půlku si nech (binomiální)
Paralelizace merge 2-cestne slucovani:
Udelam matici, rozmistim rovnomerne diagonaly, průsečíky s křivkou rozdělí prvky na stejně velké skupiny. Průsečíky najdem binomiálním dělením $\mathcal{O}(\log n)$
$T(n, p) = \mathcal{O}(\frac{n}{p}\log\frac{n}{p}+p\log\frac{n}{p}\log n + \frac{n}{p} \log p)$ = O(sekvenci razeni + p*bin search + ...)
p-cestné slučování: Přidáme barieru za seq_sort a za hledání rozdělovačů
<!--ID: 1691251771802-->
