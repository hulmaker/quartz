TARGET DECK: NI-SPOL-2023::NI-VSM
FILE TAGS: NI-SPOL-2023 NI-SPOL-10 NI-VSM

prev::[[NI-SPOL-09]]
next::[[NI-SPOL-11]]

# Systémy hromadné obsluhy a jejich limitní vlastnosti. Souvislost s Markovskými řetězci se spojitým časem.


Kendallova notace pro systémy hromadné obsluhy #flashcard 
> $A\mid S\mid c\mid K\mid N\mid D$
* A - rozdělení časů příchodů $F_A$ ($M, M(\lambda), D, D(d), G$)
* S - rozdělení časů obsluhy $F_S$
* c - počet obslužných míst
* K - kapacita systému (default $+\inf$)
* N - velikost populace (default $+\inf$)
* D - typ obsluhy (default: FIFO)
<!--ID: 1691966314119-->



Jaké jsou možné procesy příchodů zákazníků v systémech hromadné obsluhy? #flashcard 
* *$M, M(\lambda)$ - exponenciální rozdělení (markovská)
* *$D, D(d)$  - degenerované rozdělení, soustředěné v hodnotě d
* $G$ - obecné rozdělění, neznámé, nebo známé neexplonenciální
<!--ID: 1691966314120-->



Jaké různé typy obsluhy (řazení požadavků) máme? Bavíme se o systému hromadné obsluhy. #flashcard 
LIFO - last in first out = fronta
FIFO - first in first out = zásobník
řazení podle priority, náhodné atd.
<!--ID: 1691966314121-->



Littleho věta (systémy hromadné obsluhy) #flashcard 
Bud $\left\{X_t \mid t \geq 0\right\}$ striktně stacionární proces hromadné obsluhy. jsou li-všchny střední hodnoty konečné, pak: 
$$EN=\lambda \cdot ET$$
kde
EN: střední počet zákazníků v systému
ET: střední doba strávené zákazníkem v systému
lambda: intenzita příchodů
<!--ID: 1691966314122-->



Systém hromadné obsluhy typu $M|M|1$:
Proces zrodu a zániku s parametry: $\lambda_n = \lambda, n \in \mathbb{N}_0, \mu_m = \mu, m \in \mathbb{N}$


Jaká je matice intenzit příchodů v systému hromadné obsluhy typu $M|M|1$:
Proces zrodu a zániku s parametry: $\lambda_n = \lambda, n \in \mathbb{N}_0, \mu_m = \mu, m \in \mathbb{N}$
![](https://cdn.mathpix.com/snip/images/skRiVUSoYrTFmv0TPo-dc6UsKnBddE-e_c44hENt23s.original.fullsize.png)


Co musí platit, aby se systém hromadné obsluhy typu $M|M|1$ nezahltil? #flashcard 
$\varrho \leq 1$, kde $\varrho = \frac{\lambda}{c\mu}$ , kde $\lambda$ je intenzita příchodů, $c$ je počet obslužných míst a $\mu$ intenzita obsluhy
<!--ID: 1691966314123-->



Dokažte, že pro $M|M|1$ platí $EN=\frac{\varrho}{1-\varrho}$ #flashcard 
pokud $\varrho < 1$, pak existuje stacionarni rozdeleni $\pi$, je jednoznačné a $p(t)=\pi$, pak
$$\mathrm{E} N=\sum_{n=0}^{+\infty} n \cdot \boldsymbol{\pi}_n=\sum_{n=0}^{+\infty} n(1-\varrho) \varrho^n=\varrho \sum_{n=1}^{+\infty} n(1-\varrho) \varrho^{n-1}=\frac{\varrho}{1-\varrho}$$
že $\pi_n = (1-\varrho)\varrho^n$ máme z řešení rekurentní rovnice plynoucí z $\pi Q = 0$
<!--ID: 1691966314124-->



Co víme středním počtu zákazníků ve frontě $EN_f$ v systému $M|M|1$? Jak souvisí s $EN, EN_S$ #flashcard 
$EN$ - střední počet zákazníků v systému ve stacionárním stavu
$EN_s$ - střední počet zákazníků na serveru
Platí $EN=EN_s+EN_f$
Dále víme že platí: $EN=\frac{\varrho}{1-\varrho}$
No a : $\mathrm{E} N_s=1-\pi_0=\varrho$ implikuje
$$\operatorname{E} N_f=\mathrm{E} N-\mathrm{E} N_s=\frac{\varrho}{1-\varrho}-\varrho=\frac{\varrho^2}{1-\varrho}$$
<!--ID: 1691966314125-->



Jaká je doba čekání ve frontě v systému hromadné obsluhy $M|M|1$? #flashcard 
Zákazník nečeká pouze pokud je server prázdný: $\mathrm{P}(W=0)=\mathrm{P}\left(X_t=0\right)=\pi_0=1-\varrho=1-\frac{\lambda}{\mu}$
Pokud je v systému víc zákazníků, pak W je součet n exponenciálně rozdělených nezávliských veličin s parametrem $\mu$
$$
\begin{aligned}
\mathrm{P}(W>t, W>0) &= \sum_{n=1}^{+\infty} \boldsymbol{\pi}_n \mathrm{P}\left(W>t \mid X_t=n\right)=\sum_{n=1}^{+\infty} \boldsymbol{\pi}_n \int_t^{+\infty} \frac{\mu^n}{(n-1) !} e^{-\mu x} x^{n-1} \mathrm{~d} x \\
&= \int_t^{+\infty} \sum_{n=1}^{+\infty}\left(1-\frac{\lambda}{\mu}\right)\left(\frac{\lambda}{\mu}\right)^n \frac{\mu^n}{(n-1) !} e^{-\mu x} x^{n-1} \mathrm{~d} x\\
&= \frac{\lambda}{\mu} \int_t^{+\infty}(\mu-\lambda) e^{\lambda x} e^{-\mu x} \mathrm{~d} x=\mathrm{P}(W>0) \int_t^{+\infty}(\mu-\lambda) e^{-(\mu-\lambda) x} \mathrm{~d} x
\end{aligned}
$$
Z tý děsivý věci výše vychází $\mathrm{P}(W>t \mid W>0)=e^{-(\mu-\lambda) t}$, což je funkce přežití exponenciálního rozdělení.
<!--ID: 1691966314126-->



Jaká je střední doba $ET_k$ strávená zákazníkem v systému hromadné obsluhy $M|M|1$ #flashcard 
$ET=\frac{EN}{\lambda} = \frac{1}{\mu-\lambda}$ , kde $EN$: stř. poč. zák. v systému, $\lambda$: intenzita příchodů.
$ET= E_\pi W+E_\pi S_j = \frac{\lambda}{\mu} \frac{1}{\mu-\lambda}+\frac{1}{\mu}=\frac{1}{\mu-\lambda}$, kde $W_k$ je doba čekání ve frontě a $S_k$ je doba obsluhy
<!--ID: 1691966314127-->



Jaké jsou intenzity v procesu hromadné obsluhy $M|M|c$ #flashcard 
$$\mathbf{Q}_{n, n+1}=\lambda, \mathbf{Q}_{n, n-1}=\min \{c, n\} \cdot \mu= \begin{cases}n \cdot \mu & n \leq c \\ c \cdot \mu & n>c\end{cases}$$
<!--ID: 1691966314128-->


Co musí platit v systému hromadné obsluhy $M|M|c$, aby existovalo stac. rozdělení? #flashcard 
$\varrho \leq 1$, kde $\varrho = \frac{\lambda}{c\mu}$ , kde $\lambda$ je intenzita příchodů, $c$ je počet obslužných míst a $\mu$ intenzita obsluhy
<!--ID: 1691966314129-->



K čemu se dá použít systém hromadné obsluhy typu $M|G|\infty$ #flashcard 
Příchody josu Poissonovské, ale máme neomezeně serverů a libovolné rozdělení doby zpracování. 
Použije se k výpočtu potřebného počtu serverů, aby byla záruka že obsloužíme např. 99.5% zákazníků. Chceme, aby $P(N \leq n) \geq 0.995$
<!--ID: 1691966314130-->


Jaký je vzorec pro stacionární rozdělení $\pi = (\pi_0, \pi_1, ..., \pi_n)$ pro systém hromadné obsluhy $M\mid M\mid 1$?
Pokud λ < μ, existuje stacionární rozdělení procesu ve tvaru:
$$
\boldsymbol{\pi}_n=\left(1-\frac{\lambda}{\mu}\right)\left(\frac{\lambda}{\mu}\right)^n
$$
Kde $\lambda$ je intenzita příchodů a $\mu$ je intenzita obsluhy.