TARGET DECK: NI-SPOL-2023::NI-KOP
FILE TAGS: NI-SPOL-2023 NI-SPOL-12 NI-KOP

prev::[[NI-SPOL-11]]
next::[[NI-SPOL-13]]

# Experimentální vyhodnocení algoritmů, zejména randomizovaných.


Co nás rámcově zajíma při experimentálním vyhodnocení algoritmů? #flashcard 
Složitost:
* teoretická - asymptotické meze
* praktická - při nasazení na reálnou instanci se může typicky chovat jinak
Kvalita řešení
Neočekávané chování na konkrétních instancích
Závislost něčeho na něčem:
* výpočetní čas na velikosti instance
* kvalita řešení na parametrech algoritmu
<!--ID: 1691966314112-->



Jaké jsou fáze experimentu, kterým chceme vyhodnotit algoritmus? #flashcard 
![[experiment.png]]
<!--ID: 1691966314113-->



Jak probíhá provedení experimentu? Uvažujme scénář, kdy experimentálně vyhodnocujeme obecný a randomizovaný algoritmus. #flashcard 
Získávání testovacích dat:
* lze generovat a sbírat
* Chceme zajistit pravděpodobnostní proporcionalitu mezi vzorky a metrikou
Algoritmus:
* zpracuje instanci, pozorujeme proměnné na nichž závisí výsledek
* Pokud je alg. randomizovaný, tak pomocí generátoru náhodných čísel spouští algoritmus s konkrétním seedem
Statistické zpracování dat: - zákon velkých čísel potlačí varianci výsledků. Variance vzniká při sběru dat, ale i při běhu.
<!--ID: 1691966314114-->



Měření robustnosti při experimentálnám vyhodnocení algoritmů. #flashcard 
Vybere se 1 instance a pro ní vytvoří různé, stejně pravděpodobné perturbační variance. Pak měříme varianci vyvolanou perturbací.
Pokud je algoritmus randomizovaný a používá nějakou heuristiku, chceme vyhodnotit robustnost i té heuristiky a zjistit tak její limitace. Příkladem perturbací může být:
Zpřeházení proměnných ve formuli (SAT), Přeházení pořadí deklerace proměnných v programu.
Algoritmus se proti tomuto může bránit lexikografickým uspořádáním před během.
<!--ID: 1691966314115-->



Jak vypadá striktura IMRaD v odborném článku? Popište jednotlivé části. #flashcard 
Introduction: Kontext, účel, otázka, hypotéza, outline of the study
Methods: kdy, kde, jak provedeno. Proč tahle metoda, ověření korektnosti, experimenty
Results: Výsledky, odpověď, hypotéza potvrzena, relevantní data
Discussion: interpretace, vztah k dosavadnímu výzkumu, future work, summary, conclusion
<!--ID: 1691966314116-->



Jaké jsou typy randomizovaných algoritmů podle doby běhu, správnosti výsledku... #flashcard 
Monte Carlo: stanovená doba běhu, kvalita náhodná (rejection sampling)
Las Vegas: stanovená kvalita výsledků, doba náhodná (quicksort)
Atlantic City: Doba běhu náhodná, výsledek náhodný (správný s 75% pstí)
<!--ID: 1691966314117-->



Co je whtebox/blackbox fáze při experimentálním vyhodnocení randomizovaných algoritmů? #flashcard 
Fáze, které souvisejí s vývojem algoritmu. Nejdříve pomocí trénovací sady ladíme a na testovací sadě testujeme hotový algoritmus.
WhiteBox fáze: na n známých instancích ladíme pro náhodný běh
BlackBox fáze: spuštění odladěného algoritmu na nových, neznámých instancích.
<!--ID: 1691966314118-->
