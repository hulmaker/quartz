TARGET DECK: NI-SPOL-2023::NI-PDP
FILE TAGS: NI-SPOL-2023 NI-SPOL-18 NI-PDP

prev::[[NI-SPOL-17]]
next::[[NI-SPOL-19]]

Programování nad distribuovanou pamětí, programový model MPI (vícevláknové procesy, komunikátory, 2-bodové blokující a neblokující komunikační operace, kolektivní operace), paralelní násobení hustých matic, paralelní mocninná metoda.


#  programový model MPI (vícevláknové procesy, komunikátory, 2-bodové blokující a neblokující komunikační operace, kolektivní operace)


Programový model MPI: dvoubodové komunikační operace: parametry, stavové objekty #flashcard 
* `MPI_Send(*data, size, MPI_Datatype, int dest, int tag, MPI_Comm)`
* *`MPI_Recv(*data, size, MPI_Datatype, int source, int tag, MPI_Comm, MPI_Status*)`
size: velikost zprávy, MPI_Datatype: datový typ, dest/source: proces, tag: značka, MPI_Comm: komunikátor, MPI_Status: stavový objekt
<!--ID: 1691601081126-->



Programový model MPI: blokující komunikační operace a jejich komunikační módy #flashcard 
* návrat po odeslání/překopírování dat
* u Send se vrací po přijetí dat/překopírování dat do bufferu cílem
* MPI_Bsend: uloží do bufferu - nezávisí na připravenosti příjemce
* MPI_Ssend: návrat po přijetí příjemcem
* MPI_Rsend: pokud příjemce nečeká při odeslání, vrátí se chyba
<!--ID: 1691601081127-->



Programový model MPI: neblokující komunikační operace a způsoby zjištění jejich dokončení #flashcard 
Mají extra parametr, který je ukazatel na MPI_request. Slouží k testování, čekání na dokončení
* MPI_Isend: Buffer nejde modifikovat před explicitním testem
* MPI_Ibsend, MPI_Irsend. 
* Dokončení neblokujících volání lze udělat hromadně: MPI_Testall, MPI_Waitall
funkce MPI_Sendrecv, MPI_Sendrecv_replace: stejný buffer pro odeslání i příjem, testování příchodu zprávy pomocí MPI_Probe, MPI_Iprobe
<!--ID: 1691601081128-->



Programový model MPI: návratové hodnoty funkcí a ošetření chyb #flashcard 
Předpokládáme, že je komunikace spolehlivá. Neošetřuje běhové, SW, HW chyby
Typy chyb: chybný argument, neexistující cílový proces, malý buffer, přetečení sys. bufferu, mnoho zpráv ...
MPI_funkce nemají návratovou hodnotu *MPI_Status
* MPI_SUCCESS, MPI_ERR_COUNT, MPI_ERR_COMM, MPI_ERR_TAG
Obsluha chyb, nastavení:
* MPI_ERRORS_ARE_FATAL: násilné ukončení, vlákna volají MPI_ABORT
* MPI_ERRORS_RETURN: běh se neukončí, zjistíme kód chyby, můžem/nemusíme pokračovat
* MPI_ERRORS_ABORT: násilně ukončí procesy spojené s daným komunikátorem
* vlastní implementace....
MPI_Comm_set_errhandler(MPI_COMM_WORLD, MPI_ERRORS_RETURN)
<!--ID: 1691601081130-->



Programový model MPI: řešení pro permutaci cyklický posuv #flashcard 
MPI_Send, MPI_Ssend, vede vždy na zamrznutí. řešení:
* MPI_Bsend: uloží do bufferu a zahájí návrat
* MPI_Isend: neblokující volání, následné testování (MPI_Test, MPI_Wait)
* MPI_Sendrecv: nejlepší a nejjednodušší
<!--ID: 1691601081131-->



Programový model MPI: Skupinové operace #flashcard 
Všechny funkce mají i neblokující verze s I na začátku
ONE-TO-ALL:
* MPI_Bcast(): root vysílá zprávu všem v komunikátoru
* MPI_Gather(): všechny procesy vysílají nějakou zprávu ze send bufferu, root zprávy přijímá do rec. bufferu
* MPI_Gatherv(): jako gather, ale zprávy mají jinou délku, root musí znát délky a zajistit poskládání do rec. bufferu
* MPI_Scatter(): obrácený gather, všichni přijímají a jen root vysílá
* MPI_Scatterv(): obrácený gatherv
ALL-TO-ALL: Všechny uzly jsou zdroje i cíle
* MPI_Allgather(): jako gather, ale všichni přijmou všechny zprávy
* MPI_Allgatherv(): lze určit velikosti zpráv a offsety
* MPI_Alltoall(): všichni odesílají a všichni přímají, ale každému lze poslat něco jiného
* MPI_Alltoallv(): lze určit velikosti zpráv a odkud je načíst
<!--ID: 1691601081132-->


# paralelní násobení hustých matic,  paralelní mocninná metoda.

Paralelní násobení hustých matic - matice vektorem #flashcard 
Máme matici $A_{n,n}$ a vektor $x_n$, pak $y=Ax$ co mapuje mezi procesy - řádky, sloupce, šachovnice
Řádkové mapování:
* proces má řádek a příslušný prvek z $x$ - broadcastuje všem
* Všichni mají nově vektor $x$ a počítají 1 $y$ prvek - rychlost závisí na broadcastu
Sloupcové mapování:
* proces má sloupce a prvek z $x$ - počítá vlastní příspěvek do vektoru $y$ ($y$ zatím jako matice)
* matice sčítanců v řádcích, po sloupcích v procesech -> řádková redukce
Šachovnicové mapování:
* co buňka to proces, sloupec potřebuje prvek $x$ s indexem sloupce
* jako při řádku (distr. dle sloupce)
* jako při sloupci - tvorba příspěvků a pak redukce
<!--ID: 1691601081133-->



Paralelní násobení hustých matic - matice maticí #flashcard 
Šachovnicové mapování
Cannonův alg.:
- dvě matice – optimální jsou 2-D toroidy
- jednu matici v řádkách cyklicky posouváme o její index doleva (tyrkysová)
- druhou cyklicky posouváme po sloupcích nahoru (červená)
Foxův algoritmus
- 1. matice rotuje řádky
- druhá v každém kroku broadcastuje unikátní L-to-R diagonálu do celého řád
Paralelní mocninná metoda:
todo Je to prednaska 12, mas tu mezery a chybi ti otazky, dostuduj to
<!--ID: 1691601081134-->



Paralelní mocninná metoda #flashcard 
Sekvenční řešení pro výpočet největšího vlastního čísla $\lambda$: $Ax=\lambda x$ ($x$ je vlastni vektor)
1) Inicializuj libovolný, nenulový vektor $x$, díky němu dostanem $y$: $Ax=y$
2) nahradím $x$ normalizovanym $y/\alpha$
3) ukončíme podle kritéria konvergence, jinak opakujeme od bodu 1)
4) $y$ pak konverguje k vlastnímu vektoru a norma $\alpha$ konverguje k $\lambda$
Řádkové mapování: co řádek, to proces
* procesy si rozdělí $x$ a spočítají část $y$
* $y$ se posbírá (gather), norma $\alpha$, $x$ se rozdistribuuje
Libovolné mapování: prvky se rozdělí mezi procesy
* proces umí spočítat jen část y prvku.
* gather - u shromažďování se i sčítají parciální $y$
Šachovnice: virtuální 2D mřížka (řádek, sloupec, diag)
* sloupcová propaguje $x$ do procesů
* řádkové redukují diagonály (v diagonále $y$)
* v diagonále se vymění čísla a normalizuje se $y$
<!--ID: 1691601081136-->
