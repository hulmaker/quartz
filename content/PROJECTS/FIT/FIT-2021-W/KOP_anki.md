TARGET DECK: FIT-2021-W
FILE TAGS: KOP FIT-2021-W

# 01 - Kombinatorické problémy a algoritmy

Co je konfigurace, řešení a optimální řešení v kombinatorickém problému? #flashcard 
* konfigurace  - ohodnocení konfiguračních proměnných
* řešení  - konfigurace, která vyhovuje omezujícím podmínkám
* optimální řešení - řešení, které má nejlepší hodnotu optimalizačního kritéria
* suboptimální řešení  - řešení, které má přijatelnou hodnotu optimalizačního kritéria
<!--ID: 1633690648815-->


# 02 - Třídy P a NP,  co-NP, polynomiální hierarchie

Definuj třídu složitosti P #flashcard 
Rozhodovací problém patří do třídy P, jestliže pro něj existuje program pro deterministický Turingův stroj, který jej řeší v čase $O(n^k)$, kde $n$ je velikost instance a $k$ konečné číslo.
<!--ID: 1633690648819-->



Definuj třídu složitosti PSPACE #flashcard 
Rozhodovací problém patří do třídy PSPACE, jestliže pro něj existuje program pro deterministický Turingův stroj, který jej řeší v paměti $O(n^k)$, kde $n$ je velikost instance  a $k$ konečné číslo.
<!--ID: 1633690648823-->



Definuj třídu složitosti EXPTIME #flashcard 
Rozhodovací problém patří do třídy EXPTIME, jestliže pro něj existuje program pro deterministický Turingův stroj, který jej řeší v čase $O(2^{P(n)})$, kde $P(n)$ je polynom ve velikosti  instance $n$.
<!--ID: 1633690648827-->



PSPACE, EXPTIME - co je podmnožinou čeho? #flashcard 
PSPACE $\subset$ EXPTIME
<!--ID: 1633690648831-->



Co je exponential gap a jak souvisí počet kroků deter. TM a nedeter. TM? #flashcard 
Exponential gap je asymptotická mezera mezi polynomiální funkcí a exponenciální funkcí.
Jestliže nedeterministický Turingův stroj řeší problém $\Pi$ v čase $T(n)$, pak deterministický Turingův stroj řeší $\Pi$ v čase $2^{O(T(n))}$.
<!--ID: 1633690648835-->


Definuj třídu složitosti NP. #flashcard 
Rozhodovací problém $\Pi$ patří do třídy NP, jestliže pro něj existuje program pro nedeterministický Turingův stroj, který každou instanci $I \in \Pi_{ANO}$ problému $\Pi$ řeší v čase $O(n^k)$, kde $n$ je délka vstupních dat a $k$ konečné číslo.
<!--ID: 1633690648838-->



Co je to komplementární problém? #flashcard 
Problém je charakterizován konfiguracemi, co patří do množiny ANO. Komplementární problém je charakterizován doplňkem této množiny. Vytvoříme ho De Mogranovým pravidlem. Potom to je co-problém.
<!--ID: 1633690648842-->

# Evoluční techniky

Genetické algoritmy (1960) #flashcard 
kódování: binární řetězec, permutace, řetězec **intů**
operátory: křížení, mutace, inverze
řízení populace: en bloc - koncentrák
<!--ID: 1643302120980-->


 Řízení populace - popis strategii #flashcard 
* Náhrada en bloc (koncentrák) - nová populace nahradí starou
* částečná náhrada - do staré populace velikosti N přidáme novou a vybereme N jedinců
* ustálená populace (stone age) - po každém křížení nahradí potomek nejslabšího jedince
<!--ID: 1643302120990-->


Genetické programování (1988) #flashcard 
kódování: strom
operátory: křížení, mutace, editace
řízení populace: en bloc - koncentrák
<!--ID: 1643302121000-->


Cartesian Genetic Programming (200) #flashcard 
kódování: logické obvody (reprezentovany mrizkou)
operátory: mutace (zmena brany, vystupu atd)
řízení populace: 1 nejlepsi ze stare populace + N potomku
<!--ID: 1643302121009-->


Evoluční programovíání (1960) #flashcard 
kódování: automat
operátory: Změna výstupního symbolu, změna přechodu, přidání-vypuštění stavu, změna počátečního stavu
řízení populace: částečná náhrada
<!--ID: 1643302121018-->


Evoluční strategie (1960) #flashcard 
kódování: vektor **reálných** čísel, parametry mutace
operátory: křížení, mutace
řízení populace: částečná náhrada
<!--ID: 1643302121028-->


Co je globální prohledávání a jaké algoritmy znáš? #flashcard 
Takové prohledávání, které umí uniknout z lokálního minima. 
Deterministicke: B&B, dynamic programming etc.
Stochasticke: Monte-Carlo sampling
Heuristiky: SA, GA, Tabu, 
<!--ID: 1643302121038-->


Přibližná dekompozice #flashcard 
Instance $I$ má podinstance $I_1, I_2$. Pokud má $I$ řešení, značíme ho $Y$. (Analogicky $Y_1, Y_2$)
Potom pokud $Y_1, Y_2$:
 * jsou optimálním řešením instancí $I_1, I_2 \implies$ $Y$ je řešení $I$
 * neexistují, pak nevíme nic
<!--ID: 1643302121047-->


Čistá dekompozice #flashcard 
Instance $I$ má podinstance $I_1, I_2$. Pokud má $I$ řešení, značíme ho $Y$. (Analogicky $Y_1, Y_2$)
Potom pokud $Y_1, Y_2$:
 * jsou optimálním řešením instancí $I_1, I_2 \implies$ $Y$ je řešení $I$
 * neexistují, pak $Y$ neexistuje.
Z každých optimálních $Y_1, Y_2$ se dá složit **nějaké** optimální $Y$
<!--ID: 1643302121055-->


Přesná dekompozice #flashcard
Instance $I$ má podinstance $I_1, I_2$. Pokud má $I$ řešení, značíme ho $Y$. (Analogicky $Y_1, Y_2$)
Z každých optimálních $Y_1, Y_2$ se dají složit **všechny** optimální $Y$
<!--ID: 1643302121063-->


Kdy je prohledávací strategie kompletní? #flashcard 
Když každý stav navštíví **alespoň** jednou. (krom stavů co nemůžou být optimální)
<!--ID: 1643302121071-->


Kdy je prohledávací strategie systematická? #flashcard 
Když každý stav navštíví **právě** jednou. (krom stavů co nemůžou být optimální)
<!--ID: 1643302121079-->


Popiš strategii prvého zlepšení (first improvement) #flashcard 
```python
def try(state):
	""" První soused co je lepší se vrátí (záleží na pořadí) """
	for op in operators:
		current = op(state)
		if C(state) < C(current):
			return current
```
<!--ID: 1643302121089-->


Popiš strategii pouze nejlepší (best only) #flashcard 
```python
def try(state):
	""" Nejlepší soused (nezáleží na pořadí) """
	best = None
	for op in operators:
		current = op(state)
		if C(best) < C(current):
			best = current
	return best if C(state) < C(best) else None
```
<!--ID: 1643302121097-->
