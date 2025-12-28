#note/tidy , #note/develop 
[[NI-ZI-05]], [[NI-PDD]]


# Algoritmy pro nahrazování chybějících hodnot
* Smazání řádku, který obsahuje chybějící hodnotu v některém z příznaků
* Nahrazení vhodnou hodnotou (0, -1, inf)...
* Pro každý příznak spočítám mean/median a tím je v každém sloupci nahradím
* Hodnoty na základě shlukové analýzy (kNN, k-means, hierarchical)