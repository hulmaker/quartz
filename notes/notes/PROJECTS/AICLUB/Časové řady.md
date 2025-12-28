Vážený pane Hulmáku,

jsem nový datový analytik z B4I pod FZU, potkali jsme se minulé pondělí na Vámi vedeném AI klubu. 

Nejdříve bych Vás chtěl poprosit o zaslání prezentace z AI klubu 01, kde jsme bohužel nebyli přítomni jak já tak ani můj nadřizený. 

Dále bych se Vás chtěl zeptat, jestli náhodou nemáte nějaká zkušenosti s predikcí časových řad pomocí buď neuronových sítí nebo tradičních statistických 

metod. Zrovna teď rozjíždíme datový projekt, jehož cílem je predikovat vývoj marží slévárenských produktů v čase (na základě dat z několika let zpátky) a blbě 

se nám hledá nějaký starting point, od kterého bychom se mohli odrazit. Jakoukoliv radu velmi oceníme. 

Děkuji a zdravím,
Otakar Vydra

---

Dobrý den,

Odkaz na slides: [https://docs.google.com/presentation/d/1jpRsZXptvxHOKtCLC9ln_5Cq8SH01mQLiTtEHthgrkw/edit?usp=sharing](https://docs.google.com/presentation/d/1jpRsZXptvxHOKtCLC9ln_5Cq8SH01mQLiTtEHthgrkw/edit?usp=sharing)

S časovými řadami jsem se potýkal okrajově, ale je to rozhodně velmi zajímavá disciplína a budu velmi rád když Vám jakýmkoliv způsobem zvládnu pomoci.

Velmi záleží na datech, určitě je před výběrem modelu udělat solidní analýzu a porozumět vlastnostem řady. Jedná o univariate/multivariate forcasting? 
Pokud o univariate, jaké jsou vlastnosti řady?
* Je lokální rozptyl konzistentní v čase? Pokud ne, lze transformovat?
* Je [stacionární](https://www.statsmodels.org/dev/examples/notebooks/generated/stationarity_detrending_adf_kpss.html)? Pokud ne, postačí [1x differencing?](https://otexts.com/fpp2/stationarity.html#stationarity)
* Kolmost a špičatost [Jarque-Bera](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.jarque_bera.html)
* Lze použít autoregresní modely? (ARIMA, SARIMAX?) Identifikujeme řád pomocí [ACF](https://www.statsmodels.org/dev/generated/statsmodels.tsa.stattools.acf.html), [PACF](https://www.statsmodels.org/dev/generated/statsmodels.tsa.stattools.pacf.html) ([video](https://youtu.be/ZE_WGBe0_VU?si=eCFKRNOmkbuQ02xB))
* Lze pozorovat sezónnost na ACF/PACF?
* Je proces nelineární? Lze lokálně linearizovat differencováním?

U vývoje ceny a tržních předpovědí je nepříjemné, že se řada často velmi podobá náhodné procházce. Algoritmičtí tradeři se často uchylují k jednoduchým lineárním modelům kvůli jejich výkonnosti, flexibilitě a snadnému zapojení různých heuristik. Díky tomu (a rychlosti) poráží nejmodernější transformery.

Doporučuji přečíst tento blogpost (hlavně první polovinu) https://mangodata.io/blog-post/forecasting a kouknout na porovnání transformerů a lineárních modelů ([github](https://github.com/cure-lab/LTSF-Linear), [paper](https://arxiv.org/pdf/2205.13504))

Pro rychlý přehled state-of-the-art metod je skvělý [paperswithcode](https://paperswithcode.com/sota), pro časové řady lze procházet podle kategorií: https://paperswithcode.com/area/time-series

Na novém projektu bych se ale spíše držel základů a volil jednodušší metody co typicky dávají velmi dobré výsledky. Pokud řada splní podmínky pro ARIMA, zkusil bych určitě jako první ([pmdarima](https://pypi.org/project/pmdarima/) - wrapper [statsmodels](https://www.statsmodels.org/stable/index.html), má [autoARIMA](http://alkaline-ml.com/pmdarima/modules/generated/pmdarima.arima.AutoARIMA.html#pmdarima.arima.AutoARIMA) funkcionalitu). 

Jako dobrý baseline se může ukázat i "model" "repeat" - kdy jako následující hodnotu předpovíme tu minulou. (čím je řada blíž náhodné procházce, tím těžší je toto porazit)

Doufám, že i takto stručný text může být nápomocný. Jsem velmi zvědavý jak se projekt povede. Pokud je téma stále relevantní, můžeme si i zavolat.

Mějte se moc hezky,
Erik Hulmák




