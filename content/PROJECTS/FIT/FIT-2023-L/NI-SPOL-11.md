TARGET DECK: NI-SPOL-2023::NI-KOP
FILE TAGS: NI-SPOL-2023 NI-SPOL-11 NI-KOP

prev::[[NI-SPOL-10]]
next::[[NI-SPOL-12]]

# Význam tříd NP a NPH pro praktické výpočty


Definujte horní a dolní asymptotickou mez a asymptotický odhad #flashcard 
Necht: $f, g: \mathbb{N} \to \mathbb{R}$
Horní mez: $f(n)=\mathcal{O}(g(n)) \Leftrightarrow \exists c>0, n_0 \in \mathbb{N}: \forall n>n_0: f(n) \leq c \cdot g(n)$
Dolní mez: $f(n)=\Omega(g(n)) \Leftrightarrow \exists c>0, n_0 \in \mathbb{N}: \forall n>n_0: f(n) \geq c \cdot g(n)$
Odhad: $f(n)=\Theta(g(n)) \Leftrightarrow f(n)=O(g(n)) \wedge f(n)=\Omega(g(n))$
<!--ID: 1691619404003-->



Definuj třídu složitosti P #flashcard 
Rozhodovací problém patří do třídy P, jestliže pro něj existuje program pro deterministický Turingův stroj, který jej řeší v čase $O(n^k)$, kde $n$ je velikost instance a $k$ konečné číslo.
<!--ID: 1691619404010-->



Co je exponential gap a jak souvisí počet kroků deter. TM a nedeter. TM? #flashcard 
Exponential gap je asymptotická mezera mezi polynomiální funkcí a exponenciální funkcí.
Jestliže nedeterministický Turingův stroj řeší problém $\Pi$ v čase $T(n)$, pak deterministický Turingův stroj řeší $\Pi$ v čase $2^{O(T(n))}$.
<!--ID: 1691619404014-->



Definuj třídu složitosti NP. #flashcard 
Rozhodovací problém $\Pi$ patří do třídy NP, jestliže pro něj existuje program pro nedeterministický Turingův stroj, který každou instanci $I \in \Pi_{ANO}$ problému $\Pi$ řeší v čase $O(n^k)$, kde $n$ je délka vstupních dat a $k$ konečné číslo.
<!--ID: 1691619404017-->



Co je turingův stroj? #flashcard 
Univerzální výpočetní model: Nekonečná páska s datovými buňkami, pohyblivá read/write hlava, stavové řízeni
Dělí se na:
* Deterministický TS: v každém kroku je jednoznačně určen další stav
* Nedeterministický TS: z daného stavu může vést více přechodů do jiných stavů (musí se simulovat použití všech)
<!--ID: 1691619404020-->



Definuj třídu složitosti PSPACE #flashcard 
Rozhodovací problém patří do třídy PSPACE, jestliže pro něj existuje program pro deterministický Turingův stroj, který jej řeší v paměti $O(n^k)$, kde $n$ je velikost instance  a $k$ konečné číslo.
<!--ID: 1691619404023-->



Definuj třídu složitosti EXPTIME #flashcard 
Rozhodovací problém patří do třídy EXPTIME, jestliže pro něj existuje program pro deterministický Turingův stroj, který jej řeší v čase $O(2^{P(n)})$, kde $P(n)$ je polynom ve velikosti  instance $n$.
<!--ID: 1691619404027-->



Jaká je hierarchie tříd složitosti rozhodovacích problémů? #flashcard 
NL $\subset$ P $\subset$ NP $\subset$ PSPACE $\subset$ EXPTIME $\subset$ EXSPACE $\subset$
![[complexity.png]]
<!--ID: 1691619404030-->




Co je to NP complete problem, co je to Cookova věta? #flashcard 
problém, na který lze redukovat všechny ostatní NP problémy (je nejtěžší z NP)
Cookova věta dokazuje, že SAT je NPC, tedy že množina NPC není prázdná
* Pokud je tedy SAT redukovatelný na nějaký problém, tak je daný problém NPC
* Zároveň jakýkoliv NP problém lze redukovat na SAT
<!--ID: 1691619404033-->



Co je to Karpova redukce? Jake jsou jeji dusledky? (NI-KOP) #flashcard 
Speciální případ Turingovy redukce co
* převede instanci NP problému na NPC v poly. čase.
* převede instanci P problému na jiný P v poly. čase.
* převede instanci NPC problému na jiný NPC v poly. čase.
* Dokazuje, že problém patří do NPC
* transitiva:  Pokud A na B a B na C, tak je i A redukovatelný na C
* Pokud je A redukovatelný na B a B na A, jsou ekvivalentní
Definice: Rozhodovací problém Γ1 je Karp-redukovatelný na Γ2 (Γ1 ∝ Γ2), jestliže existuje
polynomiální program pro (deterministický) Turingův stroj, který převede každou instanci I1
problému Γ1 na instanci I2 problému Γ2 tak, že výstup obou instancí je shodný.
<!--ID: 1691619404036-->



Co je to Turingova redukce? Jake jsou jeji dusledky? (NI-KOP) #flashcard 
možňuje převést P problém na P v polynomiálním čase.
* Umožňuje převést NPH problém na jiný NPH v polynomiálním čase.
* Dokazuje, že daný problém patří do třídy NPH.
* Převádí vzájemně mezi sebou rozhodovací problém a konstruktivní optimalizační problém.
* Problém A je Turing-redukovatelný na B, pokud existuje program pro TS, který řeší A tak, že používá program pro výpočet B jako podprogram
Definice: Rozhodovací problém Γ1 je Turing-redukovatelný na Γ2 (Γ1 ∝ Γ2), jestliže existuje
program pro (deterministický) Turingův stroj, který řeší každou instanci I1 problému Γ1 tak, že
používá program M2 pro problém Γ2 jako podprogram (jehož trvání považujeme za jeden krok).
<!--ID: 1691619404038-->
