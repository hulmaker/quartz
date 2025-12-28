TARGET DECK: NI-SPOL-2023::NI-VSM
FILE TAGS: NI-SPOL-2023 NI-SPOL-06 NI-VSM

prev::[[NI-SPOL-05]]
next::[[NI-SPOL-07]]
# Testování statistických hypotéz

Základní pojmy testování hypotéz #flashcard 
Hypotéza - tvrzení o rozdělení dat
Testování hypotéz - ověřování jejich platnosti na základě pozorovaných hodnot
Nulová hypotéza $H_0$ – tvrzení, o kterém chceme rozhodovat
Alternativní hypotéza $H_A$ – opačné tvrzení, které stavíme proti 
* Na základě testu zamítneme, nebo nezamítneme $H_0$. 
* Když nulovou hypotézu zamítneme, můžeme tvrdit, že s velkou pravděpodobností platí $H_A$.
* Když nulovou hypotézu nezamítneme, tak nevíme nic - nelze tvrdit že platí. 
* Testy volíme tak, aby alternativní hypotéza byla ta, kterou chceme dokázat.
<!--ID: 1691432888795-->



Jaké typy chyb můžou nastat při testování hypotéz? #flashcard 
* Chyba prvního druhu – zamítneme H0, ačkoliv ve skutečnosti platí
* Chyba druhého druhu – nezamítneme H0, ačkoliv ve skutečnosti neplatí (a platí HA)
<!--ID: 1691432888796-->



p-hodnota, krit. obor a testová statistika v kontextu testování hypotéz #flashcard 
Krit. obor $W_\alpha$ svědčí ve prospěch alternativy (zamítáme H0), jeho pravděpodobnost je $\alpha$. Musí být vybraný tak, aby byl co nejmenší (chyba 2. druhu).
p-hodnota Nejmenší hodnota hladiny významnosti $\alpha$, u které zamítám $H_0$.
![[PROJECTS/FIT/FIT-2023-L/media/test_hypotez.png]]
<!--ID: 1691432888798-->



## T-testy

Jaké jsou typy t-testů při testování hypotéz? #flashcard 
t-testy jsou parametrické, používáme studentovo rozdělení.
Jednovýběrový -  testy o parametrech normálního rozdělení.
Párový - Dvourozměrné rozdělení. hypotéza $H_0: \mu_1 = \mu_2$ proti $H_A: \mu_1 \neq \mu_2$. Odečtením hodnot lze převést na jednovýběrový.
Dvouvýběrový - Máme dva nezávislé náhodné výběry, testuju shodu středních hodnot.
<!--ID: 1691432888799-->


Jaké testy o parametrech normálního rozdělení znáš? Popiš je #flashcard 
![[Pasted image 20230817170009.png]]
<!--ID: 1692285345489-->



Párový a dvouvýběrový t-test. Popiš je #flashcard 
Párový t-test: Pozorujme náhodný výběr $\left(X_1, Y_1\right)^T, \ldots,\left(X_n, Y_n\right)^T$ z nějakého dvojrozměrného rozdělení s neznámým vektorem středních hodnot
$$
\begin{array}{|c|c|c|c|}
\hline H_0 & H_A & \text { testová statistika } T & \text { kritický obor } \\
\hline \mu_1=\mu_2 & \mu_1 \neq \mu_2 & & |T| \geq t_{\alpha / 2, n-1} \\
\mu_1 \leq \mu_2 & \mu_1>\mu_2 & T=\frac{\bar{Z}_n}{s_Z} \sqrt{n} & T \geq t_{\alpha, n-1} \\
\mu_1 \geq \mu_2 & \mu_1<\mu_2 & & T \leq-t_{\alpha, n-1} \\
\hline
\end{array}
$$
Kde sz je odmocnina z vyberoveho rozptylu veliciny Z.
8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--
Dvouvýběrový t-test stejné rozptyly: $X_1, \ldots, X_n$ a $Y_1, \ldots, Y_n$
Máme dva náhodné výběry
$$
\begin{array}{|c|c|c|c|}
\hline H_0 & H_A & \text { testová statistika } T & \text { kritický obor } \\
\hline \mu_1=\mu_2 & \mu_1 \neq \mu_2 & & |T| \geq t_{\alpha / 2, n+m-2} \\
\mu_1 \leq \mu_2 & \mu_1>\mu_2 & T=\frac{\bar{X}_n-\bar{Y}_m}{s_{12}} \sqrt{\frac{n \cdot m}{n+m}} & T \geq t_{\alpha, n+m-2} \\
\mu_1 \geq \mu_2 & \mu_1<\mu_2 & & T \leq-t_{\alpha, n+m-2} \\
\hline
\end{array}
$$
kde 
$$s_{12}=\sqrt{\frac{(n-1) s_X^2+(m-1) s_Y^2}{n+m-2}}$$
Různé rozptyly: 
$$
\begin{array}{|c|c|c|c|}
\hline H_0 & H_A & \text { testová statistika } T & \text { kritický obor } \\
\hline \mu_1=\mu_2 & \mu_1 \neq \mu_2 & & |T| \geq t_{\alpha / 2, n_d} \\
\mu_1 \leq \mu_2 & \mu_1>\mu_2 & T=\frac{\bar{X}_n-\bar{Y}_m}{s_d} & T \geq t_{\alpha, n_d} \\
\mu_1 \geq \mu_2 & \mu_1<\mu_2 & & T \leq-t_{\alpha, n_d} \\
\hline
\end{array}
$$
kde
$$
s_d=\sqrt{\frac{s_X^2}{n}+\frac{s_Y^2}{m}} \quad \text { a } \quad n_d=\frac{s_d^4}{\frac{1}{n-1}\left(\frac{s_X^2}{n}\right)^2+\frac{1}{m-1}\left(\frac{s_Y^2}{m}\right)^2}
$$
<!--ID: 1692285345494-->



Máte náhodný výběr z normálního rozdělení a druhý nezávislý náhodný výběr z normálního rozděleni. Chcete testovat rovnost rozptylů. Jak to provedete? #flashcard 
pomocí F-testu rovnosti rozptylů:
$$
\begin{array}{|c|c|c|c|}
\hline H_0 & H_A & \text { testová statistika } T & \text { kritický obor } \\
\hline \sigma_1^2=\sigma_2^2 & \sigma_1^2 \neq \sigma_2^2 & & T \leq F_{1-\alpha / 2, n-1, m-1} \vee T \geq F_{\alpha / 2, n-1, m-1} \\
\sigma_1^2 \leq \sigma_2^2 & \sigma_1^2>\sigma_2^2 & T=\frac{s_X^2}{s_Y^2} & T \geq F_{\alpha, n-1, m-1} \\
\sigma_1^2 \geq \sigma_2^2 & \sigma_1^2<\sigma_2^2 & & T \leq F_{1-\alpha, n-1, m-1} \\
\hline
\end{array}
$$
kde $F_{α,n−1,m−1}$ je kritická hodnota Fisherova–Snedecorova F -rozdělení s $n − 1$ a $m − 1$ stupni volnosti.
<!--ID: 1692285345497-->



## testy dobré shody

K čemu je test dobré shody? Shrnutí testů co máme #flashcard 
* Máme napočítaná data - četnosti pozorování jednotlivých hodnot (multinomické rozdělení)
* testujeme hypotézu, že pravděpodobnosti jednotlivých hodnot jsou 
Testy:
* $\chi^2$ při známých parametrech - $H_0$ pravděpodobnosti hodnot jsou $p_1, ..., p_k$
* $\chi^2$ při neznámých parametrech - hodnoty navíc závisí na neznámém vektoru parametrů (jeho hodnotu odhadujeme při testování)
<!--ID: 1691432888801-->


Jak byste postavili statistický test v případě, že máte náhodný výběr z o velikosti n z diskrétního rozdělení a znáte pro něj četnosti. Pak chcete otestovat, že ten výběr má rozdělení s pravděpodobnostmi $p_1, ..., p_k$ #flashcard 
Na to jsou testy dobré shody:
Uděláte $\chi^2$ test při známých parametrech:
$$
\begin{array}{|c|c|c|c|}
\hline H_0 & H_A & \text { testová statistika } \chi^2 & \text { kritický obor } \\
\hline \boldsymbol{p}^{\prime}=\boldsymbol{p} & \boldsymbol{p}^{\prime} \neq \boldsymbol{p} & \chi^2=\sum_{i=1}^k \frac{\left(N_i-n p_i\right)^2}{n p_i} & \chi^2 \geq \chi_{\alpha, k-1}^2 \\
\hline
\end{array}
$$
Nebo uděláte $\chi^2$ test při neznámých parametrech:
$$
\begin{array}{|c|c|c|c|}
\hline H_0 & H_A & \text { testová statistika } \chi^2 & \text { kritický obor } \\
\hline \boldsymbol{p}^{\prime}=\boldsymbol{p} & \boldsymbol{p}^{\prime} \neq \boldsymbol{p} & \chi^2=\sum_{i=1}^k \frac{\left(N_i-n p_i\right)^2}{n p_i} & \chi^2 \geq \chi_{\alpha, k-m-1}^2 \\
\hline
\end{array}
$$
<!--ID: 1692285345501-->


## testy nezávislosti


Jak funguje test nezávislosti v kontingenčních tabulkách? #flashcard 
Konstruujeme kontingenční tabulku, kdy vkaždé buňce je četnost výskytu páru hodnot co je ve sloupci-řádku. Matice zároveň obsahuje marginální četnosti.
* Testujeme $H_0$, že $p_{ij}=p_{i\bullet}p_{\bullet j}$ (vzorec pro nezávislost veličin)
<!--ID: 1691432888802-->



Jak fungují blokové testy nezávisltosi, NIST? #flashcard 
Testují posloupnosti čísel a zda-li jsou čísla náhodná
Bloky nad/pod mean:
* blok: souvislá sekvence hodnot nad/pod mean
* Vzorec se opírá o četnost bloků nepřekračujících mean: $N_n$.
* $H_0: X_i$ jsou nezávislé
$$T=\frac{2 N_n-n-1}{\sqrt{n-1}}$$
Bloky nahoru/dolů:
* Blok je úsek monotónně se měnících hodnot.
* Opírá se o počet bloků monotonnich hodnot: $N_n$
* Stejně jak v předchozí variantě testujeme nezávislost
$$T=\frac{3 N_n-2 n+1}{\sqrt{1.6 n-2.9}}$$
<!--ID: 1691432888804-->
