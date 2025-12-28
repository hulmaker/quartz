- Visual test je kontrola kvality instalace a konfigurace systému.
- Vyhodnocuje se zvlášť pro každý entrance, který je součástí nějaké entrance group.
- Garantujeme odchylku od reality max. 5%
- Spolehlivost VT je závislá na počtu průchodů.

Na základě statistické analýzy (task 86bx7b5r9)  máme referenční tabulku, která nám dává horní odhad odchylky v závislosti na počtu průchodů pro confidence interval 95%

Zde je zjednodušená kategorizace pro vyhodnocení člověkem. (Plánujeme strojové vyhodnocování co na základě ref. Tabulky automatizuje VT - tam je granularita mnohem jemnější)  
 

# P(ACC > 95% | FF) > 95%

|     |          |        |                               |
| --- | -------- | ------ | ----------------------------- |
| FF  | Err.est. | VT ACC | Worst case ACC with 95% conf. |
| 35  | .048     | 100    | 95                            |
| 50  | .04      | 99     | 95                            |
| 60  | .037     | 98.7   | 95                            |
| 70  | .033     | 98.3   | 95                            |
| 80  | .03      | 98     | 95                            |
| 100 | .027     | 97.7   | 95                            |
| 120 | .023     | 97.3   | 95                            |
| 150 | .02      | 97     | 95                            |
| 200 | .017     | 96.7   | 95                            |

Kde FF je počet průchodů, Err. Est. je horní odhad odchylky VT v 95% confidence intervalu, VT ACC accuraccy co musí vyjít, aby v nejhorším případě byla skutečná ACC alespoň 95%

Jinými slovy: Když na 100 průchodech odhadneme ACC 97.7, tak máme 95% jistotu, že sensor bude počítat s max. chybou 5%

Když se stane, že pro požadovaný počet průchodů nemáme dost velkou acc, tak se buď nahrává dál, nebo se musí změnit config a vyhodnotit znovu. Pokud má ACC s přibývajícími annotacemi růst, pak nahráváme. Pokud tu tendenci nemá a je málo průchodů, tak spíš konfigurujeme.

Jak udělat logiku, co rozhodne jestli se mění config, nebo jestli se nahrává dál?