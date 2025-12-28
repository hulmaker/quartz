#todo Map the process completely - diagmam v xmind.

[clickup task](https://app.clickup.com/t/86bw9vq0g)

[Katka diagram](https://icfootfall-my.sharepoint.com/:i:/g/personal/katerina_machova_icsystems_ai/EbQujv5ZDsVBpvX_ER4tSWUBO7yAdthVDblWwmtohLtHAg?e=B2ZjLJ)


The delivery process can be divided into four stages [[#Planning]], [[#Installation]], [[#Calibration]], and [[#Quality assurance]]


We assume, that the proces of manufacturing sensors is done.


# Planning
1. Zákazník nám musí dodat plánek
2. Pověřená osoba (Teď Láďa Bílek) naplánuje umístění senzorů - šlo by využít [[Camera Visibility Mask]] na hrubý odhad ploch kam kamera vidí
3. Zaměřování, iC koště
4. V [services](https://forms.office.com/Pages/DesignPageV2.aspx?prevsubpage=design&groupid=8f41e919-2883-419e-b8f6-e84857ae8b2f) je šablona pro předání zaměření - okopírovat pro každé obchodní centrum zvlášť, pak bude výsledek v jednom excelu. Pro nový formulář klini na collect responses a pošli link tomu kdo pojede zaměřovat
5. Když se formulář exportuje do excelu, excel se pak musí přesunout do odpovídající složky na sharepointu
6. Fotky se pak ukládají sem https://icfootfall.sharepoint.com/:f:/s/Services/EvKi1-SGRYVNl12NpD1fbSUB1FxQyC-_RR3BzYKZdYA2NQ?e=pA5lpa


# Installation
1. Technik dojede na místo a nainstaluje senzor, je pro to potřeba spousta věcí, které se mě teď netýkají. 
2. Pověřená osoba: Vláďa Bílek
3. Výstup by měl být vstup pro nás => Z plánu by mělo jít poznat jak kalibrovat kamery na coudu

#todo - odhadni cas jednotlivych kroku

# Calibration
Předpoklady: Senzory jsou online, mám plán a zakreslení
Vstup jsou sipky na pocitani pruchodu pro VT
1. monitoring - nastavení senzoru #todo
2. cloud - zákazník, senzory #todo
3. pri kazde uprave nebo pridani senzoru je treba k userum priradit nove senzory
4. Nahrávání videa v nějaké časy #todo
5. [[Visual Tests]], [guide v clickupu](https://app.clickup.com/18311012/v/dc/hetv4-9655/hetv4-3875) - todo: Udelat jeden script, umoznit upload na sharepoint
6. vyhodnocení, [[PROJECTS/iC/wiki/QA/Visual Tests/Corrections]] #todo
7. předání Katce, ta předává zákazníkovi


## Strategie Delivery Procesu
1. Porozumění stávajícího procesu
2. Dokumentace stávajícího procesu - nálepky, kategorizace, dokument, diagram
3. Rozšíření a optimalizace
4. Vyhodnocení rizik


## Požadavky
* Lze udělat dashboard, kde bude vidět status? - jaký senzor je v jaké fázi, kolik anotací zbývá - automatizace clickupu?
* Metriky popsane v [[2023-11-02]]
* Porovnání čísel s korekcí a bez korekce, status senzoru v monitoringu

---

Pokud chceme [[Heatmap generation|heatmapy]] nebo [[PROJECTS/iC/wiki/Dev/Tracking - Inter Camera/index|Inter Camera Tracking]], musíme udělat [[image registration]]



Responsible person: [[Erik Hulmak]]