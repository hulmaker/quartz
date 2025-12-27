TARGET DECK: NI-SPOL-2023::NI-MPI
FILE TAGS: NI-SPOL-2023 NI-SPOL-05 NI-MPI

prev::[[NI-SPOL-04]]
next::[[NI-SPOL-06]]

# Numerická matematika
reprezentace čísel v počítači, chyby vznikající při výpočtech s pohyblivou řádovou čárkou, podmíněnost a stabilita numerických algoritmů.


Strojové číslo Standard IEEE-754 (1985) #flashcard 
Strojové číslo lze reprezentovat znaménkem $s$ a celými kladnými čísly $e$ (exponent) a $m$ (mantisa). Označme $(m_2)_2 = m$.
Ve vědeckém zápisu číslo odpovídá $x= \pm m \cdot 2^e$
$$
\begin{array}{|l|c|c|c|}
\hline \text { přesnost } & \text { délka } m & d=\text { délka } e & \text { parametr } b \\
\hline \text { poloviční (binary16, half precision) } & 10 & 5 & 15 \\
\hline \text { jednoduchá (binary32, single precision) } & 23 & 8 & 127 \\
\hline \text { dvojitá (binary64, double precision) } & 52 & 11 & 1023 \\
\hline \text { čtyřnásobná (binary128, quadruple prec.) } & 112 & 15 & 16383 \\
\hline
\end{array}
$$
- $\operatorname{pokud} e=2^d-1$ a $m \neq 0, \operatorname{tak} x=\mathrm{NaN}$ (Not a Number)
- pokud $e=2^d-1$ a $m=0$, tak $x=(-1)^s \cdot \operatorname{Inf}$
- pokud $0<e<2^d-1$, pak $x=(-1)^s \cdot\left(1 . m_2\right)_2 \cdot 2^{e-b}$ (tzv. normalizovaná čísla)
- pokud $e=0$ a $m \neq 0$, pak $x=(-1)^s \cdot\left(0 . m_2\right)_2 \cdot 2^{1-b}$ (tzv. subnormální (denormalizovaná) čísla)
- $\operatorname{pokud} e=0$ a $m=0$, pak $x=(-1)^s \cdot 0$
<!--ID: 1692871987409-->



Absolutní a relativní chyba reprezentace čísla pomocí strojového čísla #flashcard 
Nechť číslo $\alpha \in F$ je přibližnou hodnotou čísla $a \in \mathbb{R}$:
Absolutní chyba: $|\alpha - a|$
relativni chyba: $\frac{|\alpha - a|}{|a|}$
<!--ID: 1692871987416-->



Co je to krácení v kontextu strojových čísel? Lze se mu vyhnout? #flashcard 
Krácení je ztráta platných cifer, kde které dochází typicky při odčítání. Má nejhorší vliv na chybu ze všech možných jiných ztrát.
Nechť $x$ a $y$ jsou normalizovaná strojová čísla a platí $x > y > 0$. Pokud $2^{−p} \leq 1 − \frac{y}{x} \leq 2^{−q}$ pro nějaká kladná celá $p$ a $q$, tak platí, že nejvíce $p$ a nejméně $q$ platných binárních bitů je ztraceno při provedení odečítání $x − y$.
Krácení se lze vyhnout několika technikami: (teoreticky se jím můžeme zbavit jiné chyby :D )
* přeformulováním problému tak, aby nedocházelo k odečítání
* použitím rozvojů funkcí do řad (např. do Taylorovy řady)
* použitím jiných rovností …
* (použitím přesné aritmetiky)
<!--ID: 1692871987419-->



Jak přesně bude vypadat 32 bitů reprezentujících následující čísla (uvažujeme jednoduchou přesnost, pouze normalizovaná čísla a zaokrouhlování k nejbližšímu, nerozhodné směrem od nuly – první bit je znaménko, pak exponent a pak mantisa:
a) -1/5
b) 2/3
c) součet těchto reprezentovaných čísel
#flashcard 
$$
\begin{aligned}
-\frac{1}{5} & =-1.100110011001100110011001 \ldots \cdot 2^{-3} \\
\mathrm{fl}\left(-\frac{1}{5}\right) & =-1.10011001100110011001101 \cdot 2^{-3} \\
\frac{2}{3} & =1.010101010101010101010101 \ldots \cdot 2^{-1} \\
\mathrm{fl}\left(\frac{2}{3}\right) & =1.01010101010101010101011 \cdot 2^{-1}
\end{aligned}
$$
$$
\begin{aligned}
\mathrm{fl}\left(\frac{2}{3}\right) & =1.0101010101010101010101100 \cdot 2^{-1} \\
\mathrm{fl}\left(-\frac{1}{5}\right) & =-0.0110011001100110011001101 \cdot 2^{-1}
\end{aligned}
$$


Dopředná a zpětná chyba  u numerických algoritmů. Výstup označme $V^*(d)$, kde $d$ jsou vstupní data. Výsledek oznčme $V(d)$
Dopředná/přímá chyba: $\Delta v=V^*(d)-V(d)$
zpětná chyba: nejmenší číslo $\Delta d$ takové, že $V^*(d+\Delta d)=V(d)$ je zpětná chyba.
![](https://cdn.mathpix.com/snip/images/2nxBgFaeemwd7Mf9h-fwa57mxc9MeRmd6vs26fJ_09w.original.fullsize.png)


Podmíněnost numerického algoritmu. Relativní číslo podmíněnosti #flashcard 
Podmíněnost úlohy vyjadřuje závislost změny výstupu na změně vstupních dat - jejich malé perturbaci $\delta d$
Relativní číslo podmíněnosti úlohy je:
$$C_r=\lim _{\epsilon \rightarrow 0^{+}} \sup _{\substack{d+\delta d \in D \\\|\delta d\| \leq \epsilon}} \frac{\frac{\left\|V^*(d+\delta d)-V^*(d)\right\|}{\left\|V^*(d)\right\|}}{\frac{\|\delta d\|}{\|d\|}}$$
kde $D$ je zkoumaný definiční obor $V$ potažmo $V^∗$
Je-li $C_r \approx 1$, řekneme, že úloha je dobře podmíněná (well-conditioned).
Je-li velké, řekneme, že je špatně podmíněná (ill-conditioned).
<!--ID: 1692871987422-->
