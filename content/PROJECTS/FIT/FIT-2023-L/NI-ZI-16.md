TARGET DECK: NI-ZI-2023::NI-BML
FILE TAGS: NI-ZI-2023 NI-ZI-16 NI-BML

prev::[[NI-ZI-15]]
next::[[NI-ZI-17]]

# Rejection sampling (RS) a importance sampling (IS): důvody používání RS a IS, jejich základní principy a rozdíly, efektivita práce se vzorky. Stanovení vah v IS a možnosti jejich normování.


Co je Monte Carlo ingegrace? #flashcard 
Jelikoz plati: $\int_{a}^{b} f(x) d x = (b-a)\langle f\rangle$
1) Zjistime pomoci Monte Carlo zjistit odhad stredni hodnoty (zakon velkych cisel)
	1) pomoci rovnomerneho rozdeleni generuju body
	2) sectu jejich funkcni hodnoty a vydelim poctem
2) tenhle odhad vynasobime $(b-a)$. Muzeme si spocitat i rozptyl odhadu integralu atd.
$$
\begin{gathered}
<f(x)>=\frac{1}{b-a} \int_a^b f(x) d x \\
(b-a)<f(x)>=\int_a^b f(x) d x \\
(b-a) \frac{1}{N} \sum_{i=1}^N f\left(x_i\right) \approx \int_a^b f(x) d x
\end{gathered}
$$
<!--ID: 1691966314044-->


# Rejection Sampling

Proč bychom v bayesovské teorii chtěli používat rejection sampling? #flashcard
často se setkáváme s komplikovanými aposteriori distribucemi vyjadřujícími odhad hledané veličiny (parameteru). Lze se s nimi vypořádat pomocí *konjugovaných apriorních distribucí*. 
Pokud jej ovšem nechceme nebo nemůžeme použít, potřebujeme stále nějak zjistit vlastnosti aposteriori distribuce (např. stř. hodnota). Pokud nechceme dělat analytické metodami a aproximace, můžeme využít Monte Carlo vzorkování, z aposteriorna nagenerovat hromadu vzorků a spočítat z nich jeho přibližné vlastnosti. 
Jednou z nejjednodušších metod je  **rejection sampling**, který využívá proposal distribuci, což je nějaká vhodná distribuce, z níž umíme snadno vzorkovat.
<!--ID: 1721313056880-->



Na jaké větě je založen rejection sampling v bayesovské teorii? #flashcard 
Označme $f(x)$ hustotu, z níž chceme vzorkovat. Algoritmus je postaven na tom, že
$$
f(x) = \int_0^{f(x)} du = \int_0^1 \underbrace{\mathbb{1}_{0<u<f(x)}}_{f(x,u)}du.
$$
**Základní teorém vzorkování (Fundamental theorem of simulation)**: 
> Vzorkování $x\sim f(x)$ je ekvivalentní k vzorkování $(x, u) \sim \mathcal{U}\{(x, u): 0 < u < f(x)\}$.
Tento teorém nejde využít přímo, ale je možné jít oklikou: Navzorkovat $(x, u)$ z větší množíny a vybrat takové dvojice, pro něž je podmínka $0 < u < f(x)$ splněna.
<!--ID: 1691966314045-->



Popis algoritmu rejection sampling v bayesovské teorii #flashcard 
Předpokládejme, že $\int_a^b f(x)dx = 1$ a zvolme $m > f(x)$ pro všechna $x\in[a,b]$. Vzorkujeme $(x', u) \sim \mathcal{U}(0<u<m)$ tak, že:
   1. Navzorkujeme $x' \sim \mathcal{U}(a, b)$,
   2. navzorkujeme $u|x=x' \sim \mathcal{U}(0, m)$,
   3. vzorek přijmeme, pokud $0<u<f(x')$.
![[EXTRAS/Media/rejection_sampling.png]]
<!--ID: 1691966314046-->



Vlastnosti algoritmu rejection sampling v bayesovské teorii #flashcard 
* pravděpodobnost přijetí vzorku je $1/M$ - čím blíže je $M$ k vzorkované hustotě, tím vyšší četnost přijatých vzorků.
* Rejection sampling je mnohem efektivnější, než "naivní" Monte Carlo
* špatná efektivita oblastech, kde je hustota koncentrována na malou podmnožinu
* špatná efektivita v oblastech, kde hustota nabývá velmi nízkých hodnot
Abychom nemuseli generovat hodne vzorků, můžeme místo konstantní funkce co limituje výběr zvolit nějakou, co lépe aproximuje f
<!--ID: 1691966314047-->



Co je proposal pro rejection sampling? #flashcard 
jako limit pro vyber $u$ pouzivame funkci $g$, pro kterou plati, ze $g(x) > f(x)$ pro vsechny $x$. Dela se to tak, ze vezmu funkci co aproximuje $f$ a tu nejak naskaluju. Je to dobre k tomu, ze nezavrhneme tolik vzorku a staci nam mene vzorku, mame vetsi acceptance.
<!--ID: 1691966314048-->


# Importance Sampling

Jaká je hlavní výhoda importance sampling oproti rejection sampling? #flashcard 
rejection sampling je neefektivní v oblastech, kdy je plocha hustoty malá. - např. na chvostech normálního rozdělení je přijetí vzorku velmi nepravděpodobné.
**importance sampling** - tento fakt kompenzuje přidělováním **vah** _všem_ vzorkům
<!--ID: 1691966314049-->



Jak získáme váhy pro importance sampling v bayesovské teorii? #flashcard 
Označíme $f(x)$ cílovou (komplikovanou) hustotu a $g(x)$ proposal hustotu
$$
\int f(x) dx = \int g(x) \underbrace{\frac{f(x)}{g(x)}}_{= w(x)} dx = \int g(x) w(x) dx.
$$
kde, $g(x) > 0$ všude, kde je $f(x) > 0$.
**Výpočet vah: vložíme hodnotu $x$ do známých funkcí $f()$ a $g()$.**
To lze zobecnit, např. pro střední hodnotu $\mathbb{E}[x]$ při $f(x)$ platí
$$
\begin{aligned}
\mathbb{E}_f[x] &= \int x\cdot f(x) dx =  \int x\cdot \frac{f(x)}{g(x)}g(x) dx 
= \int x\cdot w(x) g(x) dx = \mathbb{E}_g[x\cdot w(x)],
\end{aligned}
$$
s podmínkou, že $g(x) > 0$ všude, kde je $x f(x) \ne 0$.
Váhy pak normalizujeme aby se sčítaly do jedné.
<!--ID: 1691966314050-->



Algoritmus importance sampling v bayesovské teorii #flashcard 
Celý algoritmus je o určování vah, které pak používáme např. při výpočtu integrálů.
   1. Nagenerujeme $N$ vzorků z proposal hustoty: $x_i \sim g(x)$.
   2. Spočteme hodnotu hustoty $f(x_i)$.
   3. Spočteme hodnotu hustoty $g(x_i)$.
   4. Spočteme váhy $w(x_i) = \frac{f(x_i)}{g(x_i)}$.
   5. Váhy normalizujeme, buď $W(x_i) = w(x_i)/\sum w(x_i)$ nebo $w'(x_i)=w(x_i)/N$.
Např. odhad střední hodnoty $\hat{\mu} = \sum W(x_i) x_i$.
<!--ID: 1691966314051-->



Co je to empirická distribuce? #flashcard 
Empirická distribuce umožňuje aproximovat skutečnou distribuci pomocí vážených či nevážených vzorků. 
Např. histogram je hrubým zobrazením empirické distribuce
Pokud máme vzorky (realizace) $\{x_i\}_{i=1}^N = \{x_1, \ldots, x_N\}$ na množině $E$, můžeme mluvit o empirické distribuci ve tvaru: $$
\eta^N(x) = \frac{1}{N} \sum_{i=1}^N \delta_{x_i}(x).
$$
<!--ID: 1691966314052-->


Algoritmus Sequential Importance Sampling Filteru #flashcard 
1.  Navzorkujeme $x_0^{(i)}$ z vhodné apriorní distribuce $\pi(x_0)$ a přiřadíme jim rovnoměrné váhy $w_0^{(i)} = 1/N$
2.  Pro $t=1,2,\ldots$:
    -   Predikce: navzorkujeme nová $x_t^{(i)}$ z hustoty $f_t(x_t|x_{t-1}^{(i)})$
    -   Update: přepočítáme váhy $w_t^{(i)} = w_{t-1}^{(i)} g(y_t|x_t^{(i)})$ a normalizujeme je $w_t^{(i)} \leftarrow w_t^{(i)}/\sum_j w_t^{(j)}$
    -   Odhad střední hodnoty $\mathbb{E}[x_t|\cdot] = \sum_{i=1}^{N}w_{t}^{(i)} x_t^{(i)}$
<!--ID: 1691966314053-->



Popište stručně sequential importance sampling, kdy a pro co je dobrý? #flashcard 
SIS je alg. sekvenčního odhadování (stavových modelů)
Když je splněna linearita - KF, slabá nelinearita - EKF, silná nelinearita - SIS
	- odhadujeme pomocí vzorků $x_t^{(i)}$ ze stavového prostoru $x_t$ s vahami $w_i$
- váhy chceme updatovat tak, aby pravděpodobnějším hodnotám stavové veličiny rostly a těm méně pravděpodobnějším naopak klesaly.
1) Predikce - udává vývoj stavů z $x_{t−1}​$ na $x_t$​ podle příslušného modelu. Samplujeme z modelu, získáváme novou empirickou distribuci
2) Update - využije Bayesovu větu - vloží do hustoty stavů nová pozorování (měření), přepočítáme váhy a normalizujeme je
<!--ID: 1691966314054-->
