# Algoritmy data miningu

anki flashcards: [[ADM_anki]]
test flashcards: [[ADM_anki_test]]

2 marast kvízy (5b)
písemka
soutěž - rekomendační úloha na reálných datech. relativní bodování (autoencoder)
semestrálka - (vyzkoušej protlačit klasifikátor otočení)

## Lec 01 - 18.02.2021 - Evaluace modelů

### nechápu 
- [ ] 54min - na co nejde pouzit gradientni sestup? nedaval jsem pozor
- [ ] k čemu je coefficient determinationQ

### summary 
Přehled principů trénování, vyhodnocování, testování a vybírání modelů. Probrali jsme různé ztrátové funkce pro klasifikaci i regresi a řekli si intuici co se za nimi skrývá. Dále metody testování a principy dělení dat na trénovací, validační a testovací množiny tak, aby nebyl do výsledků zanesen bias.

## Lec 02 - 25.02.2021 - metriky pro vyhodnocování modelů

### summary
Metriky pro vyhodnocování modelů, confusion matrix, rates, precision, acc, recall, F1 score, MCC atd. Dále ROC curve a metrika AUC. Díky ROC umíme zvolit vhodný threshold pro parametr v bin. klas. Cross validation, reprezentace vysledku cross validation a take bootstraping, diky kteremu mame distribuci ocekavane chyby.

## Lec 03 - 04.03.2021 - Boosting, gradient boosting
https://www.youtube.com/watch?v=3CC4N4z3GJc
## Lec 04 - 11.03.2021 - Boosting, gradient boosting

XGBoost

## Lec 05 - 18.03.2021 - Bias variance decomposition, Negative correlation learning

### summary
Celá přednáška byla o bias a variance. Ukázali jsme si co bias a variance cca dělá a s jakými hodnotami statisticky souvisí. Dále jsme si odvodili formuli pro bias variance decomposition a nastínili problém, kdy se jednotlivé weak learners učí a jejich predikce korelují. Negative correlation learning zajišťije, že jsou predikce nekorelované a tudíž máme méně redundantní informace a correlace neovlivňuje negativně výsledek v hlasování.

## Lec 06 - 25.03.2021 - Úvod do jádrových metod
