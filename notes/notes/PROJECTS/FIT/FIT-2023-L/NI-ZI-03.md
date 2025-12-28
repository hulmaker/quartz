TARGET DECK: NI-ZI-2023::NI-UMI
FILE TAGS: NI-ZI-2023 NI-ZI-03 NI-UMI

prev::[[NI-ZI-02]]
next::[[NI-ZI-04]]

# Splňování v logice

Systematické a lokální splňování v logice (DPLL, CDCL, WalkSAT, posílání zpráv). Automatické uvažování, rozhodování v teoriích prvního řádu, obecná rezoluce, princip SAT-modulovaných teorií (SMT). Zpracování přirozeného jazyka.

# DPLL


Co je to jednotková klauzule a jednotková propagace v kontextu splňování v logice? #flashcard 
Jednotková klauzule:
* je nerozhodnutá a všechny její literály až na jeden jsou pomocí $\alpha'$ nesplněné (poslední zbývající je neohodnocený)
* jediná šance, jak jednotkou klauzuli splnit, je zbývající neohodnocený literál l ohodnotit True
Jednotková propagace: klauzule: $(\lnot u \lor w) \land (u \lor v) \land (u) \land (\lnot w \lor z)$
* V každém kroku je klauzule jednotková, propagujeme
1.  $u$ musi byt true
2. $\lnot u$ musi byt true
3. $z$ musi byt true
<!--ID: 1691578042084-->



Popis algoritmu DPLL v kontextu splňování v logice #flashcard 
Backtracking s jednotkovou propagací a propagací čistých
proměnných (BT+UP+PURE)
čistá proměnná (pure variable): vyskytuje se buď pouze jako poz/neg, literál, lze ihned ohodnotit
todo: koukni na prednasku proc tam rika proc je to nahovno alg.
<!--ID: 1691578042085-->


# CDCL


Algoritmus CDCL (conflict driven clause learning, splňování v logice) #flashcard 
kombinuje BJ (backjumping), UP (unit propagation) a učení - učí se pomocí implikačního grafu, kde hledá konfliktní klausule. Je základem moderních řešičů.
DECIDE() - ohodnotí další neohodnocenou proměnnou
BCP() - jednotková propagace
BACKTRACK() - zruší rozhodnutí na úrovních > level
```python
def CDCL():
	if BCP() == "conflict": return "Unsatisfiable"
	while True:
		if not DECIDE():
			return "Satisfiable"
		while BCP() == "conflict":
			backtrack_level = analyze_conflict()
			if backtrack_level < 0:
				return "Unsatisfiable"
			BACKTRACK(backtrack_level)
```
Není nutné konstruovat implikační graf, stačí znát předchůdcovské klauzule.
Po t krocích se zavádějí restarty
Dole je CDCL pro sat-modulovane teorie (zobecneny SAT pro slozitejsi formule obsahujici veci jako cisla, datove struktury atd.)
![[smt.png]]
<!--ID: 1691578042087-->



Při splňování v logice hledáme konfliktní klauzule (nogood - např. v CDCL). Jake mají vlastnosti a jak na ně přijdeme? #flashcard 
Konfliktní klauzule lze získat hranovým řezem v implikačním grafu.
Vynucující konfliktní klauzule: obsahuje jeden literál z aktuální úrovně (po návratu způsobí jednotkovou propagaci)
UIP: unikátní implikační bod: artikulace různá od K. Víme že existuje a že jich může být více. Zajímá nás ten co je nejblíže ke K
Požadavky: Obsahuje první UIP jako jediný literál z aktuální úrovně (bude krátká a vynucující)
<!--ID: 1691578042088-->


# GSAT, WalkSAT


Popis algoritmu WalkSAT a GSAT #flashcard 
GSAT: Náhodné procházení úplných ohodnocení
* Vybere se proměnná, která když se flipne, tak se nejvíc zvětší počet sat. klauzulí
* často končí v lok. max. -> restarty
* Neúplný, nevíme jestli je vstupní formule splnitelná
WalkSAT: náhodná procházka s restarty
* s pstí p Střídá hladový krok a náhodný krok (únik z lok. max.)
<!--ID: 1691578042090-->


# Posílání zpráv


Posílání zpráv v kontextu splňování v logice #flashcard 
- Na jednotlivé klauzule formule pohlíží jako na paralelní funkční jednotky
- Zkoumá jak změna hodnoty proměnné ovlivní související klauzule
- Klauzule posílají proměnným zprávy (výstrahy), jak si přejí proměnnou nastavit, aby klauzule byla splněna (u_{i->x} = 1 … zpráva z c_i říkající x, aby nabyla správné hodnoty)
- VÝSTRAHAMI INSPIROVANÁ DECIMACE = Postupně zjednodušuje formuli dosazováním
<!--ID: 1691578042091-->


# Automatické uvažování, rozhodování v teoriích prvního řádu

## obecná rezoluce


Co je to logika prvního řádu a co formule prvního řádu? (NI-UMI) #flashcard 
Logika 1. radu:
1. Jazyk (promenne, spojky, kvantifikatory, pomocne symobly)
2. Signatura (nelogicke symboly - symboly pro funkce (f, g, +, * - transformace individui) a predikáty( vlastnosti individui - R, S, <, =))
- Formule 1. radu: termy, atomy, formule je slovo (konecna posloupnost symbolu)
POJMY V LOGICE 1. ŘÁDU:
1. Teorie (množina flí)
2. Důkaz formule φ z teorie T (posloupnost formulí, která končí formulí φ a každá formule posloupnosti buď patří do T, nebo je z nějakých předchozích formulí v posloupnosti odvozena odvozovacím pravidlem)
3. Pravdivost (validita) (T ⊧ φ (φ je pravdivá (validní, platná) v T)
4. Struktura (interpretace, realizace) signatury
<!--ID: 1691578042093-->



Obecná rezoluce: Rezoluční metoda, rezoluční pravidlo #flashcard 
Rezoluční metoda je metoda pro klauzální zamítací dokazování.
Rezoluční pravidlo: $\frac{(x_1 \lor ... \lor x_n \lor z), (y_1 \lor ... \lor y_m \lor \lnot z)}{(x_1 \lor y_1 \lor ... \lor x_n \lor y_m)}$ (ten zlomek je [log. důsledek](https://en.wikipedia.org/wiki/Logical_consequence))
Příklad: X not rich or Ken is unhappy, Ken is rich then Ken is unhappy
<!--ID: 1691578042094-->



Máme logickou formuli. Chceme provádět automatické uvažování a rozhodování v teoriích prvního řádu. Jak musíme upravit formuli aby na ní mohl být spuštěn algoritmus? #flashcard 
Převod na CNF:
1. eliminace spojek jiných než $\lnot, \lor, \land$
2. Propagace negace $\lnot$ dovnitř k atomům: $\lnot(a \land \lnot b) \vdash \lnot a \lor b$
3. Standardizace proměnných: jména proměnných musí být globálně unikátní
4. Skolemizace: Odstranění kvantifikátorů
5. Distribuce skrz ∧ a ∨
Dostaneme teorii T' ve tvaru CNF a formuli C' jako CNF, jejíž platnost chceme vzhledem k T' ověřovat
<!--ID: 1691578042095-->



## princip SAT-modulovaných teorií (SMT). 


Princip SAT-modulovaných teorií (SMT) (NI-UMI) #flashcard 
Determining whether a [mathematical formula](https://en.wikipedia.org/wiki/Well-formed_formula "Well-formed formula") is [satisfiable](https://en.wikipedia.org/wiki/Satisfiability "Satisfiability") by generalizing the [SAT](https://en.wikipedia.org/wiki/Boolean_satisfiability_problem "Boolean satisfiability problem") to more complex formulas involving [real numbers](https://en.wikipedia.org/wiki/Real_numbers "Real numbers"), [integers](https://en.wikipedia.org/wiki/Integers "Integers"), and/or various [data structures](https://en.wikipedia.org/wiki/Data_structure "Data structure") such as [lists](https://en.wikipedia.org/wiki/List_(computing) "List (computing)"), [arrays](https://en.wikipedia.org/wiki/Array_data_structure "Array data structure"), [bit vectors](https://en.wikipedia.org/wiki/Bit_vector "Bit vector"), and [strings](https://en.wikipedia.org/wiki/String_(computer_science) "String (computer science)")
Spolupráci SATu a DECIDE lze zabudovat přímo do CDCL.
![[smt.png]]
<!--ID: 1691578042097-->


## Zpracování přirozeného jazyka

Chomského hierarchie gramatik a jazyků #flashcard 
regulární: $X \to x, X \to xY, x \in T$
bezkontextové: $X \to w$
kontextové: $\alpha X \beta \to \alpha w \beta$, $X\in N, \alpha, \beta$ libovolny, w neprazdny
rekurzivně spočetné: pravidla bez omezení
<!--ID: 1691578042098-->


Jaké jsou fáze komunikace? (NI-UMI, NLP) #flashcard 
* záměr: sdělit skutečnost P
* generování: přesvědčivého sdělení o skutečnosti P → věta
* syntéza:  sdělení, hlasový syntetizátor → zvuk
* vnímání: rozpoznání hlasu → věta
* analýza: věta → derivační strom
* odstranění dvojsmyslů: určení správné interpretace (pravděpodobnostně)
* začlenění: budeme věřit, či nikoli
<!--ID: 1691578042099-->


Jak lze parsovat přirozený jazyk? Podle jakého algoritmu? Popiš ten algoritmus. #flashcard 
Algoritmus [CYK](https://en.wikipedia.org/wiki/CYK_algorithm) $\mathcal{O}(n^3)$, (bezkontextová (pravděpodobnostní) gramatika v Chomského normální formě)
```
**let** the input be a string _I_ consisting of _n_ characters: _a_1 ... _a__n_.
**let** the grammar contain _r_ nonterminal symbols _R_1 ... _R__r_, with start symbol _R_1.
**let** _P_[_n_,_n_,_r_] be an array of booleans. Initialize all elements of _P_ to false.
**let** _back_[_n_,_n_,_r_] be an array of lists of backpointing triples. Initialize all elements of _back_ to the empty list.
**for each** _s_ = 1 to _n_
    **for each** unit production _R__v_ → _a__s_
        **set** _P_[_1_,_s_,_v_] = true
**for each** _l_ = 2 to _n_ _-- Length of span_
    **for each** _s_ = 1 to _n_-_l_+1 _-- Start of span_
        **for each** _p_ = 1 to _l_-1 _-- Partition of span_
            **for each** production _R__a_    → _R__b_ _R__c_
                **if** _P_[_p_,_s_,_b_] and _P_[_l_-_p_,_s_+_p_,_c_] **then**
                    **set** _P_[_l_,_s_,_a_] = true, 
                    append <p,b,c> to _back_[_l_,_s_,_a_]
**if** _P_[n,_1_,_1_] is true **then**
    _I_ is member of language
    **return** _back_ -- by _retracing the steps through back, one can easily construct all possible parse trees of the string._
**else**
    **return** "not a member of language"
```
<!--ID: 1691578042101-->


todo jestli v tom uvidis smysl, tak to dodelej...