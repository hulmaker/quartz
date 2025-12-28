TARGET DECK: Obsidian::ML

[[NI-ZI-01]], [[NI-ZI-02]], [[NI-ZI-03]]

Co je to automatické plánování (automated planning)? Jaké algoritmy ho mohou řešit? #flashcard 
Hledání sekvencí akcí vedoucí z počátečního stavu do konečného stavu v nějakém stavovém prostoru. [wiki](https://en.wikipedia.org/wiki/Automated_planning_and_scheduling)
**Dělení**:
* **Klasické** - deterministické ve statickém konečném prostoru
* **stochastické** - akce jsou vykonávány s určitou pravděpodobností
* **dynamické prostředí** - prostředí se mění ne nutně kvůli agentovi
Lze použít path finding algoritmy. Lze převést na SAT, příp. CSP, nebo použít [[Reinforcement Learning]]. Můžeme použít hierarchické plánování, plánování v prostoru plánů. V robotice vede na [[Simultaneous localization and mapping (SLAM)]]
<!--ID: 1729010154065-->



Definuj splňování omezení s konečnými doménami (CSP) - stačí intuitivně a vysvětli základní pojmy. #flashcard 
**trojice (X,D,C)**:
- X – konečná množina proměnných - popisují vlastnosti rozhodující o řešení
- D – konečná doména (obor hodnot) pro proměnné - možnosti, které při určitém rozhodnutí máme
- C – množina podmínek nad X určují omezení pro rozhodnutí
**Základní pojmy**:
- stav S – částečné přiřazení hodnot proměnným
	- konzistentní stav – přiřazené hodnoty neporušují podmínky
	- počáteční stav – prázdné přiřazení
- akce – přiřazení hodnoty proměnné z její domény
- cílový stav – všechny proměnné ohodnoceny a navíc je konzistentní
<!--ID: 1729010154066-->



Co je to backtracking a backjumping v kontextu CSP? Znáte nějaké heuristiky co urychlí prohledávání? #flashcard 
Backtracking: prakticky DFS, vrací se jen o 1 level když narazí
Backjumping: Umí se vracet o víc úrovní.  Based on checking whether the constraint caused inconsistency. Algorithm collects one of the violated constraints in every leaf. At every node, the highest index of a variable that is in one of the constraints collected at the leaves is a safe jump.
Heuristiky, triky:
* ***nejvíce omezené proměnné** - ohodnocujeme proměnnou, v jejíž pracovní doméně je nejméně hodnot (neodkládáme těžká rozhodnutí)
* **klíčové proměnné** - ohodnocujeme proměnnou, jež se účastní nejvíce podmínek (neodkládáme důležitá rozhodnutí)
* **Učení no-good**: Když najdeme slepou, vytváříme podmínky pro detekci podobné situace.
* **dynamic backtracking**: necháváme část ohodnocených proměnných při skoku z5.
* **Forward checking**: u proměnných máme seznam možných hodnot. Když je prázdný, podmínka nelze uspokojit.
* **Arc-consistency**: filtrujeme možná ohodnocení i na základě relací mezi proměnnými.
* unit-propagation: jednotkové klauzule v SAT ohodnocujeme jako první
<!--ID: 1729010154067-->
