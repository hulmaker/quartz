TARGET DECK: NI-ZI-2023::NI-UMI
FILE TAGS: NI-ZI-2023 NI-ZI-01 NI-UMI

prev::[[NI-SPOL-20]]
next::[[NI-ZI-02]]
# Automatické plánování


Automatické plánování - definice, vyjadřovací prostředky, vlastnosti prostředí #flashcard 
Hledání sekvence akcí ze stavu s0 do stavu g v deterministickém konečném prostoru.
Vyjadřovací prostředky plánování:
- jazyk: konstanty a predikátové symboly
- stavy: konečné množiny základní atomů, aneb predikátových symbolů s dosazenými konstantami, kde neplatí co není zmíněno (uzavřený svět)
- cíl: částečná specifikace stavu konečnou množinou literálů.
Vlastnosti:
- plně pozorovatelné
- deterministické (akce se vždy úspěšně povede a její výsledek je pevně daný)
- konečné
- statické (mění se jen konáním agenta)
- diskrétní
- offline (nejdřív naplánujeme, pak vykonáme)
<!--ID: 1691174966067-->



Automatické plánování - dělení, strategie #flashcard 
Dělení:
* Klasické - deterministické ve statickém konečném prostoru
* stochastické - akce jsou vykonáványs určitou pravděpodobností
* dynamické prostředí - prostředí se mění ne nutně kvůli agentovi
Strategie:
* Dopředné - Hledá se sekvence akcí z počátečního stavu do konečněho
* Zpětné - Hledá se sekvence akcí od konce pomocí inverze akcí
<!--ID: 1691174966072-->



Popis prostoru pro automatické plánování pomocí standardu STRIPS (Fikes, Nillsson, 1971) #flashcard 
Máme proměnné=objekty, stavy a operace.
Operátor o je trojice (name, precond, effects):
- name(o) – n(x1,x2,…,xk): jméno operátoru n se seznamem parametrů (proměnných),
- precond(o): množina literálů, které musí být ve stavu splněny, aby operátor bylo možné aplikovat
- effect(o): 
	- množina literálů, které budou platit po provedení operátoru,
	- pozitivní literály přidáváme do stavu,
	- negativní literály ze stavu odebíráme.
Akce je základní instance operátoru, jež vzniká substitucí: take(k, l, c) (crane k takes c on location l). Pomocí liftování zmenšujeme prostor (místo literálů co nás nezajímají dáme proměnné)
<!--ID: 1691174966075-->



Definujte plánovací problém jakožto uspořádanou trojici. (automatické plánování) #flashcard 
Trojice $(\Sigma, S_0, S_g)$, kde $\Sigma = (S, A, y)$ je stavový prostor s přechody, S0 start, Sg cil.
S - množina všech podmnožin základních atomů
A - množina všech instanciovaných operátorů
$y: S \times A \to S$ - funkce následníka
<!--ID: 1691174966079-->


# Plánovací graf


Plánovací graf v kontextu automatického plánování #flashcard 
Určuje/reprezentuje paralelní plány $(\Pi = [\pi_1, \pi_2, ..., \pi_k])$, aneb posloupnost množin akcí, které lze provádět paralelně, nebo sekvenčně v libovolném pořadí. Lze převést na sekvenční plán při zajištění nezávislosti mezi paralelně proveditelnými akcemi. Snižuje větvení prostoru, obsahuje nedosažitelné stavy, potřeba hlídat mutexy.
![[planovaci_graf.png]]
Sloupce: Stavy, akce, stavy, akce. Spojita cara je pozitivni efekt, carkovana cara je negativni efekt.
<!--ID: 1691174966081-->



Popis algoritmu GRAPHPLAN v kontextu automatického plánování #flashcard 
střídá 2 fáze: Expanze, Extrakce
- expanze - přidává vrstvy do plánovacího grafu, dokud nezíská v poslední vrstvě cílový stav tak, že žádná dvojice jeho atomů není mutex
- pokus o extrakci paralelního plánu z plánovacího grafu (používá tabulku nogoodů). Polynomiální časová a prostorová složitost
V podstatě hledá nejdřív plán délky 1, pak délky 2, ... konec když najde plán co vede do Sg
<!--ID: 1691174966084-->



# Plánování jako SAT


Popište kompilaci plánování jako problém výrokové splnitelnosti #flashcard 
* **atomy** - jsou proměnné at(robot1, location1) (nabyvaji hodnot 0, 1)
* **stavy** - ohodnocení některých proměnných (mutexy se musí udělat zvlášť bud je na tomhle miste, nebo na jinem)
* **cil, start** - Vynutíme pomocí klauzulí at(r1, l1) and at(r2, l2)
* **čas** - každý atom a každou akci kopíruju pro každý časový krok $at(r1, l1)_t$
* **akce** - promenne co probihaji v case $move(r1, l1, l2)_t$ (nabyva 0, 1)
* preconditions jsou zakodovany jako podminky
Algoritmus pro reseni automatickeho planovani timto zpusobem se jmenuje SATPLAN
<!--ID: 1691174966087-->



# Plánování jako CSP

Popište kompilaci plánování jako problém splňování omezení (CSP) #flashcard 
Možnost 1: Převést na SAT a pak na CSP
Možnost 2:
* Proměnné (Robots = {r1, r2}) mají vícehodnotovou doménu (locations={l1, l2}).
* Casova expanze stejne jako v SAT (Kopiruju vsechno pro kazdy casovy krok a indexuju)
<!--ID: 1691174966089-->


# Hierarchické plánování


Co je hierarchické plánování (Hierarchical Task Network) #flashcard 
snaží se zmírnit potíže s příliš dlouhými plány pomocí jednodušších úkolů.
* operátory jsou pro komplexnější akce a obsahují návod, jak operátor vykonat = metody
* návod = rozklad na jednodušší úkoly + podmínky
* Abstraktní procedura HTN postupně dekomponuje úkoly v síti
	* přidává podmínky (precedence)
	* lepší nasměrování k cíli než u klasického plánování - návrh metod a dekompozic dává prostor pro integraci expertních znalostí určité domény
	* použitelné na úlohy reálné velikosti (ne jen hračky)
<!--ID: 1691174966091-->


# plánování v prostoru plánů


Popiš automatické plánování v prostoru plánů #flashcard 
Postupně opravujeme částečný plán (známe start a end) - přidáváme operace pro validní plán. V průběhu vznikají kazy které odstraňujeme:
* Kaz1 - otevřený cíl - známe cíl, nevíme jak splnit precondition. Řešení - najít akci co předpoklad splní, nebo instanciovat proměnné, nebo nastavit kauzální podmínky
* Kaz2 - Hrozba - možnost, že si přidáním akce (hrozby) rozbijeme splněný předpoklad. Řešení - hrozba musí následovat akci, nebo akce musí předcházet generátoru hrozby, nebo zakázat přidání hrozby
<!--ID: 1691174966093-->


# Plánování pohybu a problém lokalizace v robotice


Jaký je problém lokalizace v robotice, na který musíme brát při plánování pohybu ohled? #flashcard 
Senzory měří nepřesně. Používáme pravděpodobnostní modely jako Kalman Filter, Monte-Carlo, Particle Filter, Bayes-update atd... Aktualizujeme pravděpodobnost o lokaci Bayesovou větou.
<!--ID: 1691174966095-->



Konfigurační prostor pro plánování v robotice #flashcard 
- poloha, orientace, natočení kloubů
- hledání cesty spojující počáteční a cílovou konfigurai (v konfigurační spojitém prostoru)
- reprezentace pomocí pracovních souřadnic
	- pozice prvků robota (kleští, zápěstí)
	- plně popisuje pozici
	- vhodná na detekci kolizí
- reprezentace pomocí konfigurací
	- natočení kloubů ramena a zápěstí
<!--ID: 1691174966096-->



Jak se jmenuje a jak se aplikuje dopředné a zpětné plánovní v robotice? #flashcard 
dopředná kinematika:
- známe otočení kloubů, tj. konfiguraci, chceme určit polohu efektoru (lineární transformace)
inverzní kinematika:
- známe pozici efektoru reprezentovanou pracovními souřadnicemi, chceme určit konfiguraci (složitá transformace)
<!--ID: 1691174966097-->



V robotice se pohybujeme spojitým prostorem. jak se tento problém řeší v kontextu automatického plánování? #flashcard 
Rozklad na buňky - diskretizace spojitého prostoru. hledám cestu v prostoru buněk. Citlivost pohybu se řeší lepším rozlišením v příslušném místě.
Prostor se konstruuje ruznymi zpusoby, jeden z nich muze byt Voroneho diagram, nebo pravdepodobnostni mapa, kdy spojujeme konfigurace mezi kterymi vede snadna cesta.
<!--ID: 1691174966098-->
