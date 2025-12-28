
anki flashcards: [[PON_anki]]
test flashcards: [[PON_anki_test]]

## Lec 01 - 16.02.2021

### nechápu todo 
- [ ] 1:07 - co převádím na horní stupňovitý tvar a proč
- [ ] 1:13 - cvičení s polynomem co prochází body
- [ ] 2:06 - OLS rozklad - rozděluje $Q^T*Y$ na dva vektory $b_1, b_2$

### summary
Nejdřív rozcvička z lineární algebry. Potom jsme si ukázali výhody ortogonálních matic a jejich využití v úloze least squares. Představili jsme si princip QR rozkladu, ale jak ho přesně získat si ukážeme příště. 
**Hlavní myšlenka**: GEM je numericky pomalý, chceme pro inverzi použít ortogonální matice. 
**Důležitý bod**: násobení OG matice vektorem nemění normu vektoru.

## Lec 02 - 23.02.2021

### summary
- Připomenutí a odvození některých prinipů lingebry a vlastností QR rozkladu
	- násobení dvou ortogonálních matic dá ortogonální matici
	- hodnost X je stejná jako hodnost R
	- sloupce v X jsou lin. kombinace sloupců v Q
- popis principu algoritmu pro QR rozklad - vytváření nul OG maticemi a násobením
- QR rozklad - Giwensovy rotace a Hausholdovy reflexe

## Lec 03 - 02.03.2021

### nechápu
- všechno


Neměli jsme se z čeho učit, měli jsme slíbeno, že studijní materiály budou už druhý týden. Je čtvrtý a materiály nejsou. Místo toho ale máme chaotické poznámky bez popisu. (Které za 3. týden dokonce chybí.)


### summary
ukazali jsme si nejake vlastnosti metody nejmensich ctvercu. Hreb vecera byl gauss markov theorem. Z tehle přednášky nerozumím téměř ničemu. Ale Gauss Markov theorem nam říká něco ve smyslu že Wols je nejlepší nestranný odhad z dat. Nevím

## Lec 05 - 16.03.2021 - Maticove faktorizace 1
## Lec 06 - 23.03.2021 - Maticove faktorizace 2
## Lec 07 - 30.03.2021 - Maticove faktorizace 3

## Lec 08 - 06.04.2021 - Optimalizace 1
todo důkaz věty 3.2, vlatnosti do anki
todo důkaz věty 4.1

## Lec 09 - 13.04.2021 - Optimalizace 2
nevázaná optimalizace, konvexita pro konvexní optimalizacešl


# Zkouska
## (pod)otazky
### OT 1 - QR-Givensovy rotace
1) Definice QR rozkladu
2) myšlenka Givensových rotací
3) rovnice plynoucí z definice
4) odvození formule
5) aplikace a zřetězení

### OT 1 - QR-Householderovy reflexe
1) Definice QR rozkladu
2) myšlenka Householderovych reflexi
3) rovnice plynoucí z definice
4) odvození formule
5) aplikace a zřetězení

### OT 4 - SVD rozklad + vlastnosti
1) popis SVD rozkladu
2) rozklad $A^TA$, vlastní čísla, vlastní vektory
3) definice $u_i$, jejich ortogonalita, DK, že $u_i$ je vl. c. $AA^T$
4) doplnění na ON bázi
5) slepení matic dohromady = SVD
6) Rychý výpočet s Hessenbergovou maticí
7) vlastnosti

### OT 5 - SVD rozklad + pseudoinverze
1) body 1-5 z OT4
2) OLS - ztráta
3) pseudoinverze, vypocet $A^+A$

### OT 6 - SVD rozklad + total least squares
1) body 1-5 z OT4
2) definice, obrázek
3) odvozeni $\hat{w}_{TLS}$

### OT 7 - Totalni derivace, spadovy smer, myslenka spadovych metod
1) definice funkci (odkud kam)
2) definice totalni derivace + znaceni
3) chain rule
4) definice optimalizacniho problemu
5) spadove metody, volba smeru v line search