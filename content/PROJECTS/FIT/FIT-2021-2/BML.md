# Bayesovské metody ve strojovém učení

anki flashcards: [[BML_anki]]

## Lec 01 - 17.02.2021 - základy a specifika Bayesovské teorie

kde v JN budou 3 hashtagy, tak tam je parametr co můžeme měnit.

### nechápu
- [ ] cvičení jsem dost vypustil, koukni na záznam

### summary
Lehký úvod do Bayesovského světa, porovnání s frekventistickým přístupem, vysvětlení pojmů jako apriori a aposteriori. Proces určování prevděpodobnosti, následná korekce a výhody/nevýhody bayesovského přístupu. Dále připomenutí pojmů z PST a různých distribucí.

## Lec 02 - 24.02.2021 - Lineární modely, sekvenční odhad, predikce

### nechapu
[**konjugovana apriori distribuce**](https://en.wikipedia.org/wiki/Conjugate_prior)
- chápu to tak, že máme model co něco predikuje a chceme ladit hyperparametry. Pro update chceme sekvenčně updatovat a nechceme, aby se nám měnila distribuce po updatu a zároveň to sedělo na distribuci parametrů. konjugovaná distribuce by měla zajistit, že se pro update bude zachovávat distribuce. -> a když máme konjugované apriorno, tak updatujeme data jenom tak, že přičítáme hyperparametry a neřešíme bayesovu větu.

**Regrese**
- notebook - https://github.com/kamil-dedecius/bml/blob/master/prednasky/Linearni_modely_a_regrese_KD.ipynb
- koukni na video - https://www.youtube.com/watch?v=fI5TM2ePfSY&list=PLWWzz_uGN7YAhgUCAivaJn9YNJ5QBcPUR&index=5

### summary
Definovali jsme si linéární modely a ukázali si bayesovský update v sekvenční analýze. Ukázali jsme si, že když máme exponenciální třídu distribucí a konjugované apriori, tak je bayes update jednoduchý. Zadefinovali jsme si lineární model, kde $\varepsilon$ je kompenzace šumu, který má normální rozdělení. Ukázali jsme si jak odhadnout parametry pro lineární model a jak udělat predikci.


## Lec 03 - 03.03.2021 - Zobecněné lineární modely

### summary
Ukázal zobecněný model lineární regrese, který je definovaný stejně jako LR, jen nemá bias a je použita funkce g na výstup. G může být i identita, nebo třeba sigmoida co je použita v logistické regresi. Ukázali jsme si jak  analiticky odhadnout parametry modelu a jak vyhodnotit jeho přesnost. Což je stejné jako v úloze binární klasifikace.

## Lec 04 - 10.03.2021 - Kalmanův filtr
Ta přednáška je hrozná. Nemám tušení kde se co vzalo, musím si to horko-těžko domýšlet a tvrzení o rovnicích jsou seslána ze vzduchoprázdna. Jsou popsány jednotlivé části, ale chybí obecný přehled. Místo aby nám bylo na začátku jasně sděleno k čemu konkrétně KF je (že se používá pro tracking atd je fajn, ale co to znamená?), tak  musíme nejdřív pochopit motivační příklad, veškerou notaci, definice Markov procesů a celou tu dobu nevíme co s tím. Potom přichází odvození, ale už nepřichází jak to všechno dáme dohromady. Idea za KF je jednoduchá, ale přednáška to prezentuje tak, že si připadám jak úplný idiot co nic nechápe.

## Lec 05 - 17.03.2021 - Monte Carlo

Monte Carlo se pouziva kdyz vsechny odhady selzou a nezbyva nam nic jineho nez brute force. MC metody jsou zalozene na vzorkovani. Nasamplujeme si distribuci a tu potom vyuzijeme.

## Lec 06 - 24.03.2021 - Particle Filter

### summary
Ukázali jsme si další způsob jak odhadovat distribuci pomocí samplování. tentokrát generujeme vzorky a dáváme jim váhy. Výhodou je že nic nezahazujeme a hodí se tedy pro distribuce kde hrozí velký overhead. Dá se využívat sekvenčně. Tato metoda postupně přiřazuje a snižuje váhy různých vzorků a tak po pár krocích filter degeneruje. Proto používáme particle filter, který f unguje stejně jako importance sampling jen tam  je resample krok.

## Lec 07 - 31.03.2021 - Zobecněný lineární model, regularizace 