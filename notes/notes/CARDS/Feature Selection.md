---
tags:
  - on/ai
  - note/tidy
  - on/DS
---
[[NI-PDD]]
[[NI-ZI-04]]

- cílem je vybrat ty hodnoty, které nesou největší informační hodnotu, nejlépe oddělují data
- zjednodušení dat vede k snížení dimenzionality => může vést k zrychlení modelu
- snaha o nalezení ideální podmnožiny dat, která data zredukuje, ale zachová (případně i zlepší) celkovou informaci, kterou se snažíme z dat získat
- Snaha odpovědět na otázku: “Jak moc je příznak Xi relevantní pro predikování Y”


## Taxonomie metod pro výběr příznaků
* **Univariate method**: considers one variable (feature) at a time.
* **Multivariate method**: considers subsets of variables (features) together.
* **Filter method**: ranks features or feature subsets independently of the predictor (classifier). (relevance, robust, may not select the most useful features, statistical tests)
* **Wrapper method**: uses a classifier to assess features or feature subsets. (usefulness, prone to overfitting, cross validation)
* **Embedded method**: like wrapper, the search is controlled by the algorithm constructing classifier (je tam nejaka zpetna vazba co meni selekci na zaklade performace) (usefulness, cross validation, less prone to overfitting, heuristic, stochastic, exhaustive search)
* **Mutual Information** - míra vzájemné závislosti mezi dvěmi náhodnými proměnnými.


## Metriky vhodné pro výběr
- **t-test**: slouží k ověření hypotéz o konkrétní střední hodnotě/zda dvě normální rozdělení mají stejný rozptyl/střední hodnotu
- **korelace**: Lineární závislost mezi proměnnými (přímá/nepřímá)
	- Spearman
	- Pearson correlation coefficient $\rho_{X, Y}=\frac{\operatorname{cov}(X, Y)}{\sigma_X \sigma_Y}=\frac{E\left\{\left(X-\mu_X\right)\left(Y-\mu_Y\right)\right\}}{\sigma_X \sigma_Y}$
- **entropie**: očekávané množství informace, které příznak nese $H=-\sum_i P_i \log P_i$
- **Mutual information coefficient** $MI(X, Y) = \int P(X, Y) \log \frac{P(X, Y)}{P(X)P(Y)} dXdY$