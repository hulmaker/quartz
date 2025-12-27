TARGET DECK: Obsidian::ML

## Teorie složitosti
[[NI-SPOL-11]], [[NI-SPOL-12]], [[NI-SPOL-13]], [[NI-SPOL-14]], [[NI-SPOL-15]]

Definujte horní a dolní asymptotickou mez a asymptotický odhad #flashcard 
Necht: $f, g: \mathbb{N} \to \mathbb{R}$
Horní mez: $f(n)=\mathcal{O}(g(n)) \Leftrightarrow \exists c>0, n_0 \in \mathbb{N}: \forall n>n_0: f(n) \leq c \cdot g(n)$
Dolní mez: $f(n)=\Omega(g(n)) \Leftrightarrow \exists c>0, n_0 \in \mathbb{N}: \forall n>n_0: f(n) \geq c \cdot g(n)$
Odhad: $f(n)=\Theta(g(n)) \Leftrightarrow f(n)=O(g(n)) \wedge f(n)=\Omega(g(n))$
<!--ID: 1729010154138-->



Definuj třídu složitosti P a NP #flashcard 
**P**: Rozhodovací problém patří do třídy P, jestliže pro něj existuje program pro deterministický Turingův stroj, který jej řeší v čase $O(n^k)$, kde $n$ je velikost instance a $k$ konečné číslo.
**NP**: Rozhodovací problém $\Pi$ patří do třídy NP, jestliže pro něj existuje program pro nedeterministický Turingův stroj, který každou instanci $I \in \Pi_{ANO}$ problému $\Pi$ řeší v čase $O(n^k)$, kde $n$ je délka vstupních dat a $k$ konečné číslo.
<!--ID: 1729010154139-->



Jaká je hierarchie tříd složitosti rozhodovacích problémů? #flashcard 
NL $\subset$ P $\subset$ NP $\subset$ PSPACE $\subset$ EXPTIME $\subset$ EXSPACE $\subset$
![[complexity_class_hierarchy.png]]
<!--ID: 1729010154140-->




Co je to NP complete problem, co je to Cookova věta? #flashcard 
problém, na který lze redukovat všechny ostatní NP problémy (je nejtěžší z NP)
Cookova věta dokazuje, že SAT je NPC, tedy že množina NPC není prázdná
* Pokud je tedy SAT redukovatelný na nějaký problém, tak je daný problém NPC
* Zároveň jakýkoliv NP problém lze redukovat na SAT
<!--ID: 1729010154141-->



## Randomizované algoritmy

Jaké jsou typy randomizovaných algoritmů podle doby běhu, správnosti výsledku... #flashcard 
Monte Carlo: stanovená doba běhu, kvalita náhodná (rejection sampling)
Las Vegas: stanovená kvalita výsledků, doba náhodná (quicksort)
Atlantic City: Doba běhu náhodná, výsledek náhodný (správný s 75% pstí)
<!--ID: 1729010154142-->



Při heuristickém prohledávání stavového prostoru mohou optimalizační algoritmy uváznout v lokálním extrému. Jaké metody lze použít proti uváznutí? #flashcard 
* **Návrat**: vycouvání z minima (může být čas. náročné). Když si pamatujeme historii, lze skočit o více kroků (backtracking)
* **Použití většího k-okolí** (může být náročné)
* **Restarty**: Spuštění z více poč. stavů
* **Možnost úniku** - odskok (simulované ochlazování)
* **Zpracování více stavů najednou** (genetické algoritmy)
* **Restriktivní opatření**, které se jim vyhýbá (tabu search)
<!--ID: 1729010154143-->


# Simulovaná evoluce

Jaké známe typy algoritmů simulované evoluce? #flashcard 
* **Genetické algoritmy** – pracují nad binárním řetězcem, hledají obecně ideální konfiguraci
* **Genetické programování** – pracuje nad rozkladovým stromem výrazu, hledá ideální vzorec
* **Evoluční programování** – pracuje nad automatem, sestavuje ideální program
* **Evoluční strategie** – pracuje nad vektorem reálných čísel
<!--ID: 1729010154144-->
