TARGET DECK: NI-ZI-2023::NI-PDD
FILE TAGS: NI-ZI-2023 NI-ZI-05 NI-PDD

prev::[[NI-ZI-04]]
next::[[NI-ZI-06]]
# Algoritmy pro nahrazování chybějících hodnot

Jaké metody pro vypořádání se s chybějícími hodnotami znáš? (NI-PDD) #flashcard 
* Smazání řádku, který obsahuje chybějící hodnotu v některém z příznaků
* Nahrazení vhodnou hodnotou (0, -1, inf)...
* Pro každý příznak spočítám mean/median a tím je v každém sloupci nahradím
* Hodnoty na základě shlukové analýzy (kNN, k-means, hierarchical)
<!--ID: 1691432888782-->


# Detekce a ošetření odlehlých hodnot


Jak lze v datech detekovat odlehlé hodnoty? #flashcard 
Kouknu a vidim:
* Pohledem např. na graf vidím vzdálené hodnoty
Statistika:
* výpočty nad daty jako rozptyl, kolik standartních odchylek je bod vzdálen od středu atd.
Pomocí shlukové analýzy:
* Hierarchické shlukování: Ti co se spojí poslední jsou daleko
* K-means: nějaké skupiny obsahují výrazně méně vzorků, nebo jsou daleko od ostatních, nebo mají velký vnitřní rozptyl
* kNN průměrná vzdálenost sousedů je o dost větší...
<!--ID: 1691432888786-->



Jak se lze vypořádat s odlehlými hodnotami v datech? #flashcard 
* do nothing
* enforce upper and lower bounds
* let binning handle the problem
* Use cluster analysis
* Examine data statistics
<!--ID: 1691432888788-->



# undersampling/oversampling metody


Proč nám vadí nevybalancovaná data? Co s tím lze dělat? #flashcard 
Roziko overfittingu.
* under sampling - odeberu nějaké datové body z dominantních tříd
* over sampling - dogeneruju data do malých tříd - obecně lepší než undersampling.
* Bodům při učení přidělím váhy významnosti podle toho do jak velké třídy patří
<!--ID: 1691432888790-->



Jaké znáš undersampling metody? (NI-PDD) #flashcard 
Random: Náhodný výběr
Tomek links: Najdem tomkovy spoje a odstraníme z nich body z majoritní třídy
Condensing: retain points along the decision boundary
* Condensed Nearest Neighbor:  selects instances near the decision boundary
* Reduced NN: Remove a smple if doing so does not cause any incorrect classifications
* Proximity Graphs:  NN, min. spanning tree, Gabriel, Delaunay, RNG
Editing: 
* Wilson Editing: Remove points that do not agree with the majority of their kNN
* Multi-edit: repeatedly apply Wilson editing
Neighborhood Cleansing Rule: Třídy V (velká), M (malá), bod b, 3 neighbors. Odstraň $b$, pokud je z V a sousedi ho přehlasují. Odstraň sousedy, pokud jsou z V a b je z M.
Extended Nearest Neighbor: odebere jakýkoli bod, jehož třída se liší od třídy alespoň 2 ze 3 jeho NN
IB3: Odstraní špatně klasifikované body.
<!--ID: 1691432888792-->



Jaké znáš oversampling metody #flashcard 
SMOTE: Udělej kNN, vem náhodný pár z minoritní třídy a interpoluj
Najdi nejaky dalsi, to ze je jen SMOTE je trochu trapny.
<!--ID: 1691432888793-->