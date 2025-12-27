
# Teams
## Cíle
* Oddělení statických a dynamických informací. (plánky, kontakty vs. instalace, objednávky)
* Mít místo, na kterém je uložena "pravda"
* Možnost zachytit vývoj zákazníka a spolupráce v čase

### Objednávky
Objednávky jsou číslované - propojení ClickUp a Teams, verzování, vývoj v čase
**Název**: {YYMMDD_OID} {Property}  - {N}S - {Description}
* YYMMDD_OID, je číslo objednávky, OID je unikátní identifikátor ownera - odpovídá db Cloudu
* číslo objednávky stačí k jednoznačné identifikaci
* Property je budova, nebo skupina budov
* N je počet sensorů. Příklad: 4S, 29S
* Description je libovolný popisek vystihující podstatu objednávky

## Services - struktura
[Odkaz na template]([Services | Template | Microsoft Teams](https://teams.microsoft.com/l/channel/19%3Ad11835e9438f427bbd06a678f4a46be1%40thread.tacv2/Template?groupId=8f41e919-2883-419e-b8f6-e84857ae8b2f&tenantId=6488f506-7cd7-4da5-9d4d-02769c526b82))
**Owner (OID)** - každý owner má svůj channel, OID je unikátní identifikátor ownera z Cloudu
* \_EVIDENCE KLIENTA - statická část, existuje i když nebyla žádná objednávka
	* Plánky - složka pro uložení dokumentace a plánků u jednotlivých budov
	* Evidence klienta.xlsx
	* Kontakty.xlsx
* {YYMMDD_OID} {Property}  - {N}S - {Description}
	* Zakreslení sensorů v .ppt
	* Evidence sensorů, výšky, entrance groups
	* Zakreslení směrů
	* Zaměření
	* Instalace
	* ....
* 240511_44 Baťa Chodov  - 2S - Rozšíření
* 240618_44 Baťa  - 4S - heatmapy
## Customers

# ClickUp
Slouží jako pracovní nástroj. Měl by odrážet realitu, odpovídat záznamům v cloudu a v teamsech. [Delivery 2024](https://app.clickup.com/18311012/v/l/6-901502782854-1)

## Cíle
* Přehled o delivery na různých úrovních abstrakce - zákazník, objednávka, sensor, detail
	* [Orders](https://app.clickup.com/18311012/v/l/6-901502782854-1) - Rozpracované objednávky a jejich stav
	* [Owners](https://app.clickup.com/18311012/v/gr/6-901502782854-23) - Souhrn přes zákazníky
	* Task - reprezentuje konkrétní objednávku, lze sledovat její stav
	* Subtask - detailní úrověň, reprezentuje jednotlivé kroky
* Transparentnost pro všechny ve firmě
* Jasná pravidla, pojmenování, minimalizace chaosu
* snadné zaškolení
* Využití potenciálu ClickUp k organizaci
	* Mít možnost vytvářet **pohledy pro jednotlivá oddělení**, fáze, zákazníky, atd atd
## Order (Task)
Objednávky jsou číslované - propojení s teams, verzování, vývoj v čase
[Příklad objednávky v ClickUp](https://app.clickup.com/t/86byw5b9y)

Každá objednávka bude mít následující vlastnosti: 

**Název**: {YYMMDD_OID} {Property}  - {N}S - {Description}
* YYMMDD_OID, je číslo objednávky, OID je unikátní identifikátor ownera - odpovídá db Cloudu
* Property je budova, nebo skupina budov
* N je počet sensorů. Příklad: 4S, 29S
* Description je libovolný popisek vystihující podstatu objednávky
**Assignee**: Owner procesu, dohlídne na průběh a přidělí odpovědnosti (Katka?)
**Priority**: Může se hýbat v závislosti na tom jak potřebujeme
**Owner**: Tag s názvem vlastníka a OID. Formát: {Owner} (OID)
**Comment**: High-level kontext na úrovni objednávky: např. velký blokátor co by měl zajímat všechny e.g. nejsou čočky, musíme objednat, katastrofická chyba, vracíme se zpět atd...
#### Description
Každá objednávka bude mít popis, aby bylo při rozkliknutí na první pohled jasné o co se jedná.
* **Zadání**: Co děláme, proč to děláme, co chce zákazník, co je cílem a jaké jsou požadavky, podmínky atd...
* **Poznámky**: info co stojí za to mít na úvodní stránce. Např. že obsluha je problematická a je potřeba dávat pozor na toto a toto
* **Sensory**: seznam sensorů co je potřeba v rámci tasku odbavit. Každý musí být funkční před uzavřením objednávky

## Status
* Statusy popisují stav objednávky. Odpovídají delivery procesu tak jak byl zakreslen v [[iCDelivery.png|diagramu]].
* Status mají i subtasky - ty jsou nejdřív OPEN, pak se posouvají do příslušného stavu podle toho čeho se týkají. Vysvětlení v nadpisu **Subtask**
* Status tasku je vždy podle statusu posledního subtasku. Bude-li 9 sensorů odevzdáno a jeden bude na instalaci, status bude INSTALLATION.
	* Takové případy jsou ještě popsané v nadpisu **Dělení/Fázování**

| Status        | Responsible person | Popis                                        |
| ------------- | ------------------ | -------------------------------------------- |
| OPEN          | Katka              | Jednání se zákazníkem, objednávka je koncept |
| DESIGN        | Marek              | Design řešení, zaměření, dokumentace         |
| INSTALLATION  | Vojta              | Kabeláž, instalace, sklad                    |
| CONFIG        | Erik               | Config online sensorů podle dokumentace      |
| VISUAL TEST   | Martin             | nahrávání, annotace, vyhodnocení výsledků    |
| INVESTIGATION | Filip, Martin      | VT neprošla, opravy, debugging               |
| REVIEW        | Katka              | Odevzdávání, nastavení EGs, přístupů         |
| CLOSED        |                    | fakturujeme, archivujeme                     |

## Subtask
Každý subtask bude mít následující vlastnosti:
* **Name** {Pojmenování objednávky} - {popis subtasku}
	* Když budeme držet tuto konvenci, lze folterovat subtasky a groupovat je v listech a mít pohledy s větší detailností a seznamem subtasků přes všechny tasky.
	* Příklad: {YYMMDD_OID} {Property}  - {N}S - VISUAL TEST
	* Příklad: {YYMMDD_OID} {Property}  - {N}S - Kabeláž
* **Assignee**: odpovědná osoba, zajistí že bude task v review
* **Description**: jasný popis, musí být zřejmé co se musí stát aby se úkol splnil
* **Status**: Open, "in progress", review, closed
	* jelikož se statusy dědí z tasku, tak uvažujme, že in progress je ten task, který není open, ani closed
	* Když se subtask bude týkat VT, "in progress" bude VISUAL TEST, pokud se bude týkat configu, "in progress" bude CONFIG

#### Pravidla
Pokud něco chybí, je odpovědnost vykonavatele vyžádat a odpovědnost zadavatele poskytnout.

**Situace -> pravidlo**
* Zadavatel přidělí vykonavatele -> task je aktivní, status OPEN
* task je aktivní -> vykonavatel zjistí o co jde a může si vyžádat dodatečné informace
* vykonavatel požaduje informace -> task je blokovaný, zadavatel má povinnost je zajistit
* Vykonavatel má vše co potřebuje -> posouvá stav do stavu odpovídajícího "in progress"
* Úkol je splněn -> vykonavatel posune na REVIEW
* task je v REVIEW -> zadavatel/owner provede kontrolu a posune na CLOSED pokud je v pořádku. Jinak se task vrací vykonavateli.

## Dělení / Fázování
Někdy je nutné objednávky rozdělit na fáze a odevzdat např. vchody dříve. Pak máme 2 možnosti.

### 1. Dělení Objednávek
Vhodné pro složitější případy. (např. Objednávka má víc jak 10 sensorů)
1. Rozdělíme sensory na skupiny a pro každou skupinu vytvoříme virtuální objednávku s odpovídajícím popisem. 
	* V teamsech se nic nemění, virtuální objednávky jsou jen "pracovní" pro nás.
	* Virtuální objednávky na sobě musí být nezávislé, nemají zmínku o sensorech, kterých se netýkají
1. Virtuálním objednávkám nastavíme závislosti, jméno, description atd.
2. Reálná objednávka má takový status, jako ta nejposlednější virtuální.
3. Virtuální objednávky jedou nezávisle na sobě a musí obsahovat všechny informace pro dokončení

**Příklad dělení**: platí: N = N1 + N2
* Reálná objednávka [ClickUp](https://app.clickup.com/t/86byw5b9y): {YYMMDD_OID} {Property}  - {N}S 
* virtuální objednávka 1 [ClickUp](https://app.clickup.com/t/86byw7hng): {YYMMDD_OID}.1 {Property}  - {N1}S
* virtuální objednávka 2 [ClickUp](https://app.clickup.com/t/86byw7q09): {YYMMDD_OID}.2 {Property}  - {N2}S

### 2. Dělení Subtasků
Vhodné pro jednodušší případy. Postup:
1. V popisu objednávky v Sensors rozepíšeme jak se sensory dělí na skupiny
2. Subtasky vytváříme tolikrát, kolik máme skupin.
3. Pojmenováváme subtasky podle schématu popsaném v dělení objednávek