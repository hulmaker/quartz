TARGET DECK: NI-ZI-2023::NI-UMI
FILE TAGS: NI-ZI-2023 NI-ZI-02 NI-UMI

prev::[[NI-ZI-01]]
next::[[NI-ZI-03]]
# Splňování omezení s konečnými doménami (CSP)


Definuj splňování omezení s konečnými doménami (CSP) jako usporadanou ntici a vysvětli základní pojmy. #flashcard 
trojice (X,D,C):
- X – konečná množina proměnných - popisují vlastnosti rozhodující o řešení
- D – konečná doména (obor hodnot) pro proměnné - možnosti, které při určitém rozhodnutí máme
- C – množina podmínek nad X určují omezení pro rozhodnutí
Základní pojmy:
- stav S – částečné přiřazení hodnot proměnným
	- konzistentní stav – přiřazené hodnoty neporušují podmínky
	- počáteční stav – prázdné přiřazení
- akce – přiřazení hodnoty proměnné z její domény
- cílový stav – všechny proměnné ohodnoceny a navíc je konzistentní
<!--ID: 1691225318495-->


# Filtrace domén a lokální konzistenční techniky


Popiš filtraci domén v CSP, k čemu je dobrá a jak se provádí #flashcard 
Platnost podmínky testujeme až po jejím úplném ohodnocení. Filtrace domén kontroluje její splnitelnost ještě dříve.
**Dopředná kontrola** (FC - Forward checking): Pro proměnné držíme seznam možných hodnot, které updatujeme po každém ohodnocení. Podmínka s prázdným seznamem je neuspokojitelná. Lze vynutit ohodnocení když zbývá pouze jedna možná hodnota a opakovat kontrolu.
**Hranová konzistence** (AC - arc-consistency): Filtrujeme seznam možných ohodnocení i na základě relací mezi proměnnými. Opakovaně vynucujeme konzistenci na hranách. Pokud pro hodnotu z proměnné a neexistuje možná hodnota proměnné b, tak hodnotu z a odebereme.
<!--ID: 1691225318500-->


# pokročilé prohledávání (backjumping, dynamický backtracking)


Popište princip backjumpingu pro CSP (Conflict-based backjumping) #flashcard 
Based on checking whether the constraint caused inconsistency. Algorithm collects one of the violated constraints in every leaf. At every node, the highest index of a variable that is in one of the constraints collected at the leaves is a safe jump. Pro proměnné evidujeme konfliktní množiny proměnných, kvůli kterým nelze uspokojit podmínka žádnou hodnotou v současné proměnné. Vracíme se na proměnnou s nejvyšším indexem v konfliktní proměnné. Abychom neskákali tak moc zpátky, heuristicky vybíráme podmínky s proměnnými co jsou hluboko abychom při konfliktu neztratili tolik práce.
<!--ID: 1691225318504-->



Popište princip dynamického backtrackingu pro CSP #flashcard 
Dynamický backtracking ponechává část ohodnocených proměnných při skoku zpět. U každé nepřiřazené hodnoty si pamatuje důvody (konfliktní proměnné).
<!--ID: 1691225318507-->



# Globální Omezení a Rozhodovací Heuristiky


Jaké jsou rozhodovací heuristiky pro výběr proměnné v CSP? #flashcard 
Hodnoty vybíráme tak, abychom co nejdříve narazili na řešení:
* ***nejvíce omezené proměnné** - ohodnocujeme proměnnou, v jejíž pracovní doméně je nejméně hodnot (neodkládáme těžká rozhodnutí)
* **klíčové proměnné** - ohodnocujeme proměnnou, jež se účastní nejvíce podmínek (neodkládáme důležitá rozhodnutí)
<!--ID: 1691225318510-->



Jaká máme globální omezení/podmínky v CSP? #flashcard 
* Zobecněná hranová konzistence (GAC) - Hranovou konzistenci nevynucujeme pro dvojice, ale n-tice
* all-Different(x1, x2, ..., xk) - podmínka vynucující vzájemě různé hodnoty v proměnných. Je to příklad párování řešitelného pomocí toků v sítích.
<!--ID: 1691225318512-->
