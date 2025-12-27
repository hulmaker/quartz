#  Předzpracování dat

anki flashcards: [[PDD_anki]]

course links: [courses](https://courses.fit.cvut.cz/NI-PDD/index.html)

## Přednášky
| no. | check      | téma                                                                       | slidy                                                                                                                                            |
| --- | ---------- | -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | 21.09.2021 | Úvod, KDDM, CRISP-DM, DM software                                          | [pdd-01.pdf](https://courses.fit.cvut.cz/NI-PDD/lectures/files/pdd-01.pdf)                                                                       |
| 2   | 05.10.2021 | Vizualizace a průzkum dat                                                  | [pdd-02.pdf](https://courses.fit.cvut.cz/NI-PDD/lectures/files/pdd-02.pdf)                                                                       |
| 3   |            | Metody určování významnosti příznaků                                       | [pdd-03.pdf](https://courses.fit.cvut.cz/NI-PDD/lectures/files/pdd-03.pdf)                                                                       |
| 4   | 19.10.2021 | Problémy v datech - reprezentace, validace, čištění, konverze              | [pdd-04.pdf](https://courses.fit.cvut.cz/NI-PDD/lectures/files/pdd-04.pdf)                                                                       |
| 5   |            | Problémy v datech - binning, outliers, shluková analýza, vyvažování skupin | [pdd-05.pdf](https://courses.fit.cvut.cz/NI-PDD/lectures/files/pdd-05.pdf)                                                                       |
| 6   |            | Redukce dat                                                                | [pdd-06.pdf](https://courses.fit.cvut.cz/NI-PDD/lectures/files/pdd-06.pdf)                                                                       |
| 7   |            | Redukce dat - další metody                                                 | [pdd-07.pdf](https://courses.fit.cvut.cz/NI-PDD/lectures/files/pdd-07.pdf)                                                                       |
| 8   |            | Projekční metody PCA, ICA, LDA                                             | [pdd-08.pdf](https://courses.fit.cvut.cz/NI-PDD/lectures/files/pdd-08.pdf), [pca.pdf](https://courses.fit.cvut.cz/NI-PDD/lectures/files/pca.pdf) |
| 9   |            | Předzpracování časových řad                                                | [pdd-09.pdf](https://courses.fit.cvut.cz/NI-PDD/lectures/files/pdd-09.pdf)                                                                       |
| 10  |            | Předzpracování textu                                                       | [pdd-10.pdf](https://courses.fit.cvut.cz/NI-PDD/lectures/files/pdd-10.pdf)                                                                       |
| 11  |            | Předzpracování obrazu                                                      | [pdd-11.pdf](https://courses.fit.cvut.cz/NI-PDD/lectures/files/pdd-11.pdf)                                                                       |
| 12  |            | Předzpracování obrazu (pokračování)                                        | [pdd-12.pdf](https://courses.fit.cvut.cz/NI-PDD/lectures/files/pdd-12.pdf)                                                                       |


### 01 - KDDM, CRISP-DM, DM software
Úvod do problematiky, představení celého procesu analýzy, zpracování a dodání výsledku. Řešení problému je často závislé na perfektním pochopení dat. Následně z dat vytěžujeme vzorce, nové poznatky a souvislosti.


### 02 - Vizualizace a průzkum dat
Víceméně jen předváděčka různých typů vizualizace. Grafy můžou být hodně divoké, jejich účel je rychlé vytvoření intuice toho, jaké jsou v datech souvislosti atd. Můžou být různých dimenzí atd.

### 04 - Problémy v datech - reprezentace, validace, čištění, konverze
Hodně generické povídání. Mluvilo se obecně o problémech v datech, o případech co můžou nastat v praxi a co by mohl žadavatel chtít. Probíraly se například různé formáty datumu a jaké s nimi mohou být problémy. Jak reprezentovat data a kdy se vyplatí např. vektorizovat. Zmínila se nevyváženost dat.


1.  [x] Download the dataset MetObjects.csv from the repository [https://github.com/metmuseum/openaccess/](https://github.com/metmuseum/openaccess/).
2.  [ ] Check consistency (i.e. that same things are represented in the same way) of at least **three features** where you expect problems (include "Object Name" feature). You can propose how to clean the selected features, however do not apply cleaning (in your interest) 🙂 _(1.5 points)_
3.  [x] Select at least **two features** where you expect integrity problems (describe your choice) and check integrity of those features. By integrity we mean correct logical relations between features (e.g. female names for females only). _(2 points)_
4.  [x] Convert at least **five features** to a proper data type. Choose at least one numeric, one categorical and one datetime. _(1.5 points)_
5.  [x] Find some outliers and describe your method. _(3 points, depends on creativity)_
6.  [x] Detect missing data in at least **three features**, convert them to a proper representation (if they are already not), and impute missing values in at least **one feature**. _(1 + 3 points, depends on creativity)_
7.  [ ] Focus more precisely on the cleaning of the "Medium" feature. As if you were to use it in KNN algorithm later. _(2 points)_
8.  [ ] Focus on the extraction of physical dimensions of each item (width, depth and height in centimeters) from the "Dimensions" feature. _(2 points)_