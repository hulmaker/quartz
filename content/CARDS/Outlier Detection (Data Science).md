---
tags:
  - on/ai
  - on/statistics
  - note/develop
  - note/tidy
  - on/DS
---

[[NI-PDD]], [[NI-ZI-05]]

## Metody detekce odlehlých hodnot
**Kouknu a vidim**:
* Pohledem např. na graf vidím vzdálené hodnoty
**Statistika**:
* výpočty nad daty jako rozptyl, kolik standartních odchylek je bod vzdálen od středu atd.
**Pomocí shlukové analýzy**:
* Hierarchické shlukování: Ti co se spojí poslední jsou daleko
* K-means: nějaké skupiny obsahují výrazně méně vzorků, nebo jsou daleko od ostatních, nebo mají velký vnitřní rozptyl
* kNN průměrná vzdálenost sousedů je o dost větší...



## Jak se s nimi vypořádat?
* do nothing
* enforce upper and lower bounds
* let binning handle the problem
* Use cluster analysis
* Examine data statistics