TARGET DECK: NI-SPOL-2023::NI-KOP
FILE TAGS: NI-SPOL-2023 NI-SPOL-13 NI-KOP

prev::[[NI-SPOL-12]]
next::[[NI-SPOL-14]]

# Princip lokálních heuristik, pojem globálního a lokálního minima, obrana před uváznutím v lokálním minimu.


# Stavovy prostor

Definujte pojem stavový prostor jako uspořádanou ntici. Jaké máme základní pojmy? (NI-KOP) #flashcard 
$S=\{s_i\}$ je množina všech stavů algoritmu $A$ řešícího instanci $I$. Nechť $Q = \{q_j\}$ je množina operátorů $S \to S$ takových, že $q_j (s_i) \neq s_i$ pro všechna $s_i, q_j$. Pak dvojici $(S, Q)$ nazveme stavovým prostorem algoritmu $A$ řešícího instanci $I$.
* stav - sjednocení hodnot konfigurace a vnitřních proměnných algoritmu
* akce - aplikace operátoru na stav
* $k$-okolí stavu - stavy dosažitelně s aplikací nejvýše $k$ akcí
* Inverzní operátor - operator neutralizující efekt původního operátoru
<!--ID: 1691316773655-->



Co je to úplná a systematická strategie v kontextu prohledávání stavového prostoru? #flashcard 
**Úplná strategie**: navštíví všechny stavy kromě těch, o kterých víme, že nedávají (optimální) řešení
* Do not leave any stone unturned, unless you are sure there is nothing under it (Pearl)
* Úplná strategie je strategie pohybu stavovým prostorem lokální heuristiky.
* Úplný algoritmus (úplný řešič) dokáže odpovědět, že instance nemá řešení
**Systematická strategie**: úplná strategie, která navštíví každý stav nejvýše jednou
* Do not turn any stone more than once (Pearl)
* Naleznou řešení, existuje-li 
* Naleznou optimální řešení, existuje-li
<!--ID: 1691316773661-->



Co jsou lokální a globální heuristické metody v kontextu prohledávání stavového prostoru? #flashcard 
**Lokální metody** – Práce vždy a pouze s aktuálním stavem. Může uvažovat i blízké okolí (sousední stavy).
**Globální metody** – Dekompozice instance na menší instance téhož problému
<!--ID: 1691316773664-->



Popište konstruktivní, iterativní a dvojfázové heuristiky v kontextu prohledávání stavového prostoru. #flashcard 
**Konstruktivní heuristika** – Začne z triviální konfigurace a postupnými kroky konstruuje řešení.
• **Iterativní heuristika** – Začne z nějakého (i neplatného) řešení a to postupně vylepšuje.
• **Dvojfázové heuristiky** – První fáze slouží k získání řešení (konstruktivně, náhodné řešení), ve druhé fázi iterativní vylepšování
<!--ID: 1691316773666-->



# Globalni a Lokalni minimum


Co je globální a lokální minimum? Jaký lokální minima představují problém? Uvažujme kontext prohledávání stavového prostoru. #flashcard 
**Globální optimum** – stav, ve kterém je hodnota opt. kritéria nejlepší v rámci všech možných stavů
**Lokální optimum** – stav, ve kterém je hodnota opt. kritéria nejlepší v rámci jeho okolí
Lokální heuristiky, které neřeší problém lokálních minim, uváznou hned v prvním. To se projevuje tím, že výsledné řešení silně závisí na startovacím stavu a má potenciál být lepším.
<!--ID: 1691316773668-->



# Princip lokálních heuristik, obrana pred uviznutim

Jaké jsou vlastnosti lokálních heuristik v kontextu prohledávání stavového prostoru? #flashcard 
U složitých problémů je systematické prohledávání pomalé
* Lok. heuristiky predikují cestu k optimu (známe vlastnosti problému)
* Většinou nenaleznou optimální řešení, ale dokáží nalézt dostatečně dobré řešení
* k-okolí aktuálního stavu je ohodnoceno heuristickou funkcí. Podle hodnoty se rozhoduje jaké se prozkoumají.
* Musí mít mechanismus pro únik z lokálního minima. Např. setrvačnost, restarty atd.
<!--ID: 1691316773669-->



Popište kroky, kterými se řídí jednoduché lokální heuristiky jako je náhodná procházka. Jak jí vylepšit? (NI-KOP) #flashcard 
1. Kontrola kritéria ukončení (optimalizační kritérium splněno, maximální počet kroků, atd)
2. náhodně vyber nějaký stav z okolí a udělej krok.
3. Pokud je lepší, označí jej jako BEST.
4. Pokud není, vrací se do prvního kroku bez nalezení BEST
Když použijeme heuristickou funkci, zmenšování kroků a restarty, tak máme simulované ochlazování.
<!--ID: 1691316773671-->



Vyjmenuj nějaké jednoduchá lokální heuristiky a urči jejich vlastnosti (NI-KOP) #flashcard 
Náhodná procházka: není úplná, není systematická
Best only: greedy, není úplná, možnost uvíznutí
<!--ID: 1691316773672-->



Jaké metody se používají proti uváznutí v lokálním minimu? (NI-KOP) #flashcard 
* Návrat: vycouvání z minima (může být čas. náročné). Když si pamatujeme historii, lze skočit o více kroků (backtracking)
* Použití většího k-okolí (může být náročné)
* Restarty: Spuštění z více poč. stavů
* Možnost úniku (simulované ochlazování)
* Zpracování více stavů najednou (genetické algoritmy)
* Restriktivní opatření, které se jim vyhýbá (tabu search)
<!--ID: 1691316773674-->


