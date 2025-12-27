TARGET DECK: NI-ZI-2023::NI-SCR
FILE TAGS: NI-ZI-2023 NI-ZI-20 NI-SCR

prev::[[NI-ZI-19]]
next::[[NI-ZI-21]]

# Časové řady
aditivní a multiplikativní dekompozice, momenty (střední hodnota, rozptyl, autokovariance).


Jaké jsou cíle analýzy časových řad? #flashcard 
1. Popis pozorovaného jevu - rozsahy, perioda, vývoj, outliers, extremy, zavislosti
2. predikce vývoje/interpolace minulého vývoje
3. řízení - řízení vývoje procesu (epidemie, cena atd)
<!--ID: 1691617378778-->



Co je trend v kontextu časových řad? #flashcard 
dlouhodobý vývoj střední hodnoty
<!--ID: 1691617378788-->



Co je sezonnost v kontextu časových řad? #flashcard 
sezónnost - periodicky se opakující, poměrně pravidelný a předpověditelný (očekávatelný) vývoj časové řady. Typické jsou například vývoje teploty v průběhu roku, počet zákazníků v pneuservisech, počet zaměstnanců v zemědělství, počet zákazníků v horských centrech apod. Sezónnost můžeme celkem dobře analyzovat v příslušném [grafu sezónnosti](https://en.wikipedia.org/wiki/Seasonal_subseries_plot), či lépe v řadě box plotů, oba vyžadují znalost periody. Tu můžeme zjistit pomocí _autokorelační funkce_ (ACF). Pro analýzu sezónnosti je ale vždy potřeba nejprve odstranit _trend_.
<!--ID: 1691617378796-->



Co jsou cyklické změny v kontextu časových řad? #flashcard 
Cyklické změny - fluktuace bez pravidelné periody. Občas se projeví, ale nedá se predikovat kdy. Pokud se projeví, tak se ale dá predikovat její průběh
<!--ID: 1691617378802-->



Jaké vlastnosti u časových řad pozorujeme? #flashcard 
1. trend - dlouhodobý vývoj střední hodnoty
2. sezónnost - pravidelný, periodický predikovatelný pattern. Perioda se dá zjistit pomocí autokorelační funkce
3. Cyklické změny - fluktuace bez pravidelné periody. Občas se projeví, ale nedá se predikovat kdy. Pokud se projeví, tak se ale dá predikovat její průběh
4. další nepravidelné fluktuace
<!--ID: 1691617378808-->



Momenty časových řad: stř. hodnota, ropzptyl, autokovariance ... #flashcard 
střední hodnota: $\mu_t = \mathbb{E}[X_t]$
variance: $\sigma_t^2 = \operatorname{var} X_t$
autokovariance: $\gamma(t_1, t_2) = \operatorname{cov}(X_{t_1}, X_{t_2}) = \mathbb{E}[(X_{t_1} - \mu_{t_1})(X_{t_2} - \mu_{t_2})]$.
<!--ID: 1691617378813-->



Aditivní a multiplikativní dekompozice časových řad. #flashcard 
Časovou řadu lze často rozložit na jednotlivé uvedené složky, přičemž cyklické změny a nepravidelné fluktuace se sloučí do jedné.
**aditivní**: $Y_t = T_t + S_t + E_t$,
**multiplikativní**: $Y_t = T_t \cdot S_t \cdot E_t$,
kde $Y_t$ je pozorovaná veličina v čase $t$, $T_t$ je hodnota trendu, $S_t$ je sezónní složka a $E_T$ nevysvětlená složka. V aditivních modelech obecně platí, že amplituda sezónních složek je přibližně stejná, zatímco v multiplikativních se s rostoucím trendem zvyšuje i sezónní amplituda (a naopak). 
<!--ID: 1691617378817-->



# Druhy stacionarity a rozdíl mezi nimi


Stacionarita časových řad - definice, druhy: #flashcard 
Stacionarita říká, jaký má vliv posun o libovolný čas na sdruženou distribuci.
Časová řada je:
* ***striktně (silně) stacionární**, pokud sdružená distribuce $X_{t_1},\ldots, X_{t_n}$ je stejná, jako sdružená distribuce $X_{t_1+\tau},\ldots, X_{t_n+\tau}$ pro všechna $t_1, \ldots, t_n, \tau$.
* ***slabě stacionární**, pokud je invariantní vůči posunům v čase pouze v rámci momentů rozdělení do druhého řádu: $\mathbb{E}[X_t] = \mu,  \operatorname{cov}(X_t, X_{t+\tau}) = \gamma(\tau)$
Budeme-li tedy uvažovat $n=1$, potom striktní stacionarita znamená, že distribuce $X_{t}$ je stejná pro všechna $t$ a rovněž momenty $\mu = \mu_t$ a $\sigma^2 = \sigma_t^2$ jsou v čase konstantní.
<!--ID: 1691617378821-->



# Základní vlastnosti náhodné procházky a bílého šumu


Definujte časovou řadu a určete její vlastnosti - bílý šum #flashcard 
[Bílý šum](https://en.wikipedia.org/wiki/White_noise) je náhodný proces $\{X_t\}$, kde
$$
\begin{aligned}
\mathbb{E}[X_t] &= 0, \\
\operatorname{var}(X_t) &= \sigma^2 < \infty,\\
\operatorname{cov}(X_t, X_{t+\tau}) = \gamma(\tau) &= 0.
\end{aligned}
$$
Speciálním případem je potom normální (gaussovský) bílý šum, kde $X_t \sim \mathcal{N}(0, \sigma^2)$.
Je striktně stacionární, nemá sezónost ani cyklické změny
<!--ID: 1691617378826-->



Definujte časovou řadu a určete její vlastnosti - náhodná procházka #flashcard 
Uvažujme diskrétní bílý šum $Z_t \sim \mathcal{L}(0, \sigma^2)$. Proces $\{X_t\}$ nazýváme [náhodnou procházkou](https://en.wikipedia.org/wiki/Random_walk), pokud
$$
\begin{aligned}
X_0 &= 0,\\
X_t &= X_{t-1} + Z_t,
\end{aligned}
$$
a tedy $X_t = \sum_{i=1}^t Z_t$, $\mathbb{E}[X_t] = 0$ a $\operatorname{var}(X_t) = t\sigma^2$.
Není stacionární, nemá sezónost ani cyklické změny
Náhodná procházka je oblíbeným modelem pro modelování cen akcií, ve fyzice pro popis Brownova pohybu, v computer science pro odhad velikosti webu atd.
<!--ID: 1691617378830-->
