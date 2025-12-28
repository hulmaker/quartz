Hint - otevři obsah v sidepane, Diagram lze zobrazit zde: https://app.eraser.io/workspace/uLxpn70lvUMH6AOSZsbk?origin=share

Vysvětlení struktury tohoto dokumentu.
===

# H1 - space
Reprezentuje **<mark style="background: #FF5582A6;">proces</mark>** ve firmě, víme pak, kolik času a peněz se tu spálí

Nový space přidává jen ten, co drží tenhle model v hlavě. Space musí být konzistentní s dosavadní strukturou. Každý proces musí mít definovaného jednoho hlavního představitele.

## H2 - List
Jednotlivé dělení v rámci procesu - vytváří se zde tasky. Task je velký a pro jeho splnění je potřeba vynaložit hodiny, které měříme. Životní cyklus tasku jsou dny-týdny. Tasky vytváří project owner, subtasky si definuje kdo chce. Každý task má povinný label odpovídajícího **customera**, nebo **obědnávky**.

**<mark style="background: #FF5582A6;">Customer je label/hashtag</mark>**, je to to nejduležitější koncept v celé struktuře. Celý ekosystém se točí kolem zákazníka, kvůli nim to děláme. Každý task má POVINNÝ label customer. Některé tasky se vztahují k obědnývkám, to je specifikováno níže. **<mark style="background: #FF5582A6;">Defaultní zákazník je iC samotné!!</mark>** - interní zákazník (počítají se náklady, výnosnost atd)

Lze do workspace nastavit required custom field customer, vhodný by byl dropdown, nebo label. Label umožní multichoice. Lze nastavit jako required. (Nevim jestli lze zakazat tvorba novych labelu - ochrana proti missclicku tato položka je velmi velmi důležitá)

Každému listu lze nastavit description, Je důležité, aby každý jeden člověk věděl jak to přesně funguje. Měl by mít přístup k tomuto dokumentu a popiskům ve clickupu. Měl by vědět, kdo je zodpovědná osoba.


ClickUp Structure
===

# Sales
>  1. Sales vyjednají zakázku, která pak přechází na [[#Delivery (projects, operations)]] 

Responsible person: Katka?, Team: Katka, Adam, Zuzka, Martin Baumgartl

Sales bude těžko měřit čas u tasku, účetní je bude muset rozpočítat a přiřadit podle nějakého odhadu. 

## {{Customer 1, 2, ...}}
Jednotliví zákazníci by zde měli mít svoji složku a v ní rozjednané dealy, tam může probíhat komunikace mezi Sales a R&D ohledně požadavků?
Sem bychom mohli dát pevný seznam customers? (v jiných spaces asi nebude kompletní seznam) Domluvit se s Katkou 

# Delivery (projects, operations)
> 2. [[#Sales]] dají požadavek. Delivery si vyžádá výrobu od [[#Production]], po instalaci nahraje software, který produkuje a dokumentuje [[#R&D]]. Delivery končí předávacím protokolem. Tam pak začíná [[#Support]].

Responsible person: Čulda, Team: Bílek-instalace, výroba, Erik-software)

## {{Order 1, 2, ...}}
Plánování umístění
Instalace senzorů, komplikace související s instalacemi
Softwarova konfigurace, monitoring, cloud, vizualni zkousky, ...

# Production
> 3. Dostanou požadavek od [[#Delivery (projects, operations)]] a buď senzory vyrobí, nebo vydají ze skladu. (POZOR: Production nevyvíjí hardware, to se děje v R&D!)

Responsible person: Mára, Team: Mára, Vojta
## {{Order 1, 2, ...}}

# Support 
> 4. Po podepsání předávacího protokolu přichází support. Komunikují se zákazníky, řeší problémy, updatují senzory atd.

Responsible person: #todo ??, Team: (Filip, Katka, Martin, Bílek)

## {{Customer 1, 2, ...}}
Žumpa, reklamace, update, atd...

# R&D
> R&D vyvíjí software i hardware. V případě software je výstupem zdrojový kód a dokumentace. V případě hardware je výstupem jen dokumentace - blueprint

Responsible person: Filip (Gru), Team: minions

## Sprint Folder
Pojedeme [agile software development](https://en.wikipedia.org/wiki/Agile_software_development) (např [SCRUM](https://en.wikipedia.org/wiki/Scrum_(software_development))) - je nutné, aby každý rozuměl workflow, můžou se kdykoliv doptat. Někdo, kdo může být "SCRUM master"

Zde bude sprint folder, která bude obsluhovaná product ownerem ([[PROJECTS/iC/wiki/Personal/Filip Naiser]]?, [[Jan Culik]]?)

Ve sprintech se nevytvářejí tasky, jen se tam linkují. Jsou vždy na dané období, slouží jako přehled toho, co se aktuálně děje.

## {{Product}}
## Sensor - HW
Mára, vojta
## Cloud
Pavel, Jarda, Michal
## Monitoring
Filip B.
## Footfall
minions
Tracking, detector, heatmapy, testing, a nevim co vsechno
## Citylight
ghost town

# Marketing

# HR
Responsible person: #todo ??

## Recruitment
Personal/technical interviews - co člověk, to task, poznámky z meetingu psát do tasku

Omezený přístup? Asi by to neměl vidět každý, jsou tam citlivé osobní informace

## Management
task description, task supervision, task evaluation

# Annotations
> Technicky patří z části pod R&D a Delivery. Má ale vedoucího a je přehlednější anotační proces agregovat v samostatném space. Chodí sem požadavky z R&D na anotace pro tréning, požadavky z Delivery na vizuální zkoušky a ze Supportu také na vizuální zkoušky.

Responsible person: Viki, Team: anotators, goodsailors

## Visual Test
Vizuální zkoušky - nevytvářejí se žádná nová data pro trénování, ale validuje se stávající přesnost.

## General
Zde se fakturuje čas annotátorů pro tvorbu nových dat. Zamyslet se, zda-li nerozdělovat mezi našimi a goodsailors

# IT
Responsible person: Filip B.  ?, Team: minions
Nastavování nástrojů, instalace, nastavení teamsů, clickupu, licence, oprava tiskáren...

# Finance
Responsible person: Adam?, Team: Adam, Zuzka, externí účetní
Zuzka - dotaz, zda li se to hodí zakládat na clickupu


Problémy s Clickupem
===
* Měření času tam moc nefunguje (problém s více záložkami najednou)
* člověk musí být nutně online - blbne to i s časem [tvrdi ale ze umi offline](https://help.clickup.com/hc/en-us/articles/6308895791127-Offline-Mode)
* Byly by speciální tasky jen na měření času?

Možná řešení - integrace toggle, jiné nástroje - popis v [[2023-11-08]]
