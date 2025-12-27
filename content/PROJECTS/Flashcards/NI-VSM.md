TARGET DECK: Obsidian::statistics

[[NI-SPOL-06]], [[NI-SPOL-07]], [[NI-SPOL-08]], [[NI-SPOL-09]], [[NI-SPOL-10]]


Základní pojmy testování hypotéz - vysvětli $H_A, H_0$ #flashcard 
Hypotéza - tvrzení o rozdělení dat
Nulová hypotéza $H_0$ – tvrzení, o kterém chceme rozhodovat
Alternativní hypotéza $H_A$ – opačné tvrzení, které stavíme proti 
* Na základě testu zamítneme, nebo nezamítneme $H_0$. 
* Když nulovou hypotézu zamítneme, můžeme tvrdit, že s velkou pravděpodobností platí $H_A$.
* Když nulovou hypotézu nezamítneme, tak nevíme nic - nelze tvrdit že platí. 
* Testy volíme tak, aby alternativní hypotéza byla ta, kterou chceme dokázat.
<!--ID: 1729010154068-->



Vysvětlete následující pojmy v kontextu testování hypotéz: p-hodnota, kritický obor a testová statistika #flashcard 
p-hodnota: Nejmenší hodnota hladiny významnosti $\alpha$, u které zamítám $H_0$.
Kritický obor $W_\alpha$: svědčí ve prospěch alternativy (zamítáme $H_0$), jeho pravděpodobnost je $\alpha$. Vybíráme ho tak, aby byl co nejmenší (chyba 2. druhu).
![[EXTRAS/Media/test_hypotez.png]]
<!--ID: 1729010154069-->



## T-testy

Jaké znáš typy t-testů při testování hypotéz a co dělají? Stačí intuitivní popis. #flashcard 
t-testy jsou parametrické, používáme studentovo rozdělení, slouží k porovnávání rozdělení. V tabulce níže to je pro stř. hodnotu, ale testuje se i rozptyl.
$$
\begin{array}{|c|c|}
\hline H_0 & H_A  \\
\hline \mu_1=\mu_2 & \mu_1 \neq \mu_2  \\
\mu_1 \leq \mu_2 & \mu_1>\mu_2  \geq t_{\alpha, n-1} \\
\mu_1 \geq \mu_2 & \mu_1<\mu_2  \\
\hline
\end{array}
$$
**Jednovýběrový**:  Set testů o parametrech normálního rozdělení. (o střední hodnotě při známém a neznámem rozptylu, a o samotném rozptylu)
**Párový**: Dvourozměrné rozdělení - dvojice $(X_i, Y_i)$. testujeme shodu stř. hodnot. Odečtením hodnot lze převést na jednovýběrový.
**Dvouvýběrový**: Máme dva nezávislé náhodné výběry (už to nejsou dvojice), testuju shodu stř. hodnot.
<!--ID: 1729010154070-->



## testy dobré shody

K čemu je test dobré shody v kontextu testování hypotéz? Shrnutí testů co máme (stačí intuice) #flashcard 
* Máme napočítaná data - četnosti pozorování jednotlivých hodnot (multinomické rozdělení)
* testujeme hypotézu, že pravděpodobnosti jednotlivých hodnot jsou 
Testy:
$H_0$ pravděpodobnosti hodnot jsou $p_1, ..., p_k$
$\chi^2$ test při **známých parametrech**:
$$
\begin{array}{|c|c|c|c|}
\hline H_0 & H_A & \text { testová statistika } \chi^2 & \text { kritický obor } \\
\hline \boldsymbol{p}^{\prime}=\boldsymbol{p} & \boldsymbol{p}^{\prime} \neq \boldsymbol{p} & \chi^2=\sum_{i=1}^k \frac{\left(N_i-n p_i\right)^2}{n p_i} & \chi^2 \geq \chi_{\alpha, k-1}^2 \\
\hline
\end{array}
$$
$\chi^2$ test při **neznámých parametrech**: hodnoty závisí na neznámém vektoru parametrů (jeho hodnotu odhadujeme při testování)
$$
\begin{array}{|c|c|c|c|}
\hline H_0 & H_A & \text { testová statistika } \chi^2 & \text { kritický obor } \\
\hline \boldsymbol{p}^{\prime}=\boldsymbol{p} & \boldsymbol{p}^{\prime} \neq \boldsymbol{p} & \chi^2=\sum_{i=1}^k \frac{\left(N_i-n p_i\right)^2}{n p_i} & \chi^2 \geq \chi_{\alpha, k-m-1}^2 \\
\hline
\end{array}
$$
<!--ID: 1729010154071-->



Jak byste postavili statistický test v případě, že máte náhodný výběr z o velikosti n z diskrétního rozdělení a znáte pro něj četnosti. Pak chcete otestovat, že ten výběr má rozdělení s pravděpodobnostmi $p_1, ..., p_k$ #flashcard 
Na to jsou testy dobré shody:
<!--ID: 1729010154072-->


Vyjmenujte statistické testy pro testování vlastností různých rozdělení. Jaké vlastnosti testují?
- **Jednovýběrový t-test**: testuje shodu parametrů náh. výběru s normálním rozdělením.
- **Párový t-test**: testuje shodu parametrů náh. výběrů z vícerozměrného rozdělení. Odečtením lze převést na jednovýběrový.
- **Dvouvýběrový t-test**: Porovnává vlastnosti dvou nezávislých náh. výběrů.
- **Test dobré shody** $\chi^2$: Test, zda četnosti prvků v náh. výběru odpovídají multinomickému rozdělení.
- **Testy nezávislosti**: Testujeme jestli jsou náh. výběry nezávislé.
- **Blokové testy nezávislosti NIST**: Máme řadu, testujeme zda-li jsou na sobě hodnoty závislé.


Popište hierarchii kódů (stačí intuitivně) - základy teorie kódování a informace (NI-MPI) #flashcard 
**Instantní**: (prefixový) žádné kódové slovo není prefixem jiného kódového slova
**Jednoznačně dekódovatelný**: Kód $C$ je jednoznačně (též unikátně) dekódovatelný, pokud je $C^*$ nesingulární.  Kde $C^*$ je rozšíření kódu $C$. (Je-li např. $C(x_1) = 0$ a $C(x_2) = 001$, tak $C^∗(x_1x_2) = 0001$)
**Nesingulární**: $C$ prosté zobrazení. Tj. $x \neq x^{\prime} \Rightarrow C(x) \neq C\left(x^{\prime}\right)$
![[teorie_informace-hierarchie_kodu.png]]
<!--ID: 1729010154073-->



# Entropie


Entropie diskrétní náhodné veličiny - definice, co znamená, vlastnosti, operace #flashcard 
Míra neurčitosti, Nulová entropie znamená jistý jev, S klesající pravděpodobností jevu roste hodnota jeho entropie, entropie je nezáporná.
$$H(X)=-\mathrm{E} \log (p(X))=-\sum_{x \in X} p(x) \cdot \log (p(x))$$
Pravidlo: $H(X, Y)=H(X)+H(Y \mid X)$
* Neboli $H(Y \mid X)=H(X, Y)-H(X)$, tedy $H(Y \mid X)$určuje, jaká informace je navíc v Y oproti X
* $H(X)$ určuje informaci pouze v $X$
* $H(X, Y)$ určuje sjednocení informace v $X$ a $Y$
* $H(Y \mid X)$ určije informaci v $Y$ co není v $X$
* $I(X, Y)$ určuje průnik informací v $X$ a $Y$
* pro nezávislé $X, Y$ platí: $H(X, Y)=H(X)+H(Y)$
<!--ID: 1729010154074-->



Definujte markovský řetězec s diskrétním časem a markovskou podmínku #flashcard 
Náhodný proces $\left\{X_n \mid n \in \mathbb{N}_0\right\}$ s nejvýše spočetnou množinou stavů $S$ nazýváme markovský řetězec s diskrétním časem, pokud splňuje markovskou podmínku:
**Markovská podmínka**:
$$
(\forall n \in \mathbb{N}, \text { a } \forall s, s_0, \ldots, s_{n-1} \in S):
$$
$$
\mathrm{P}\left(X_n=s \mid X_{n-1}=s_{n-1}, \ldots, X_1=s_1, X_0=s_0\right)=\mathrm{P}\left(X_n=s \mid X_{n-1}=s_{n-1}\right)
$$
<!--ID: 1729010154075-->
