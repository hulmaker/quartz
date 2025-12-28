TARGET DECK: Obsidian::DS

[[NI-ZI-20]], [[NI-ZI-21]], [[NI-ZI-22]]

# Časové řady
aditivní a multiplikativní dekompozice, momenty (střední hodnota, rozptyl, autokovariance).


Co je trend v kontextu časových řad? #flashcard 
dlouhodobý vývoj střední hodnoty
<!--ID: 1729010153947-->



Co je sezonost v kontextu časových řad? Jak ji lze detekovat? #flashcard 
**sezónnost** - periodicky se opakující, poměrně pravidelný a předpověditelný (očekávatelný) vývoj časové řady. Typické jsou například vývoje teploty v průběhu roku, počet zákazníků v pneuservisech, počet zaměstnanců v zemědělství, počet zákazníků v horských centrech apod. Sezónnost můžeme celkem dobře analyzovat v příslušném [grafu sezónnosti](https://en.wikipedia.org/wiki/Seasonal_subseries_plot), či lépe v řadě box plotů, oba vyžadují znalost periody. Tu můžeme zjistit pomocí _autokorelační funkce_ (ACF). Pro analýzu sezónnosti je ale vždy potřeba nejprve odstranit _trend_.
<!--ID: 1729010153948-->



Co jsou cyklické změny v kontextu časových řad? #flashcard 
**Cyklické změny** - fluktuace bez pravidelné periody. Občas se projeví, ale nedá se predikovat kdy. Pokud se projeví, tak se ale dá predikovat její průběh
<!--ID: 1729010153949-->



Jaké vlastnosti u časových řad pozorujeme? #flashcard 
- **trend** - dlouhodobý vývoj střední hodnoty
- **sezónnost** - pravidelný, periodický predikovatelný pattern. Perioda se dá zjistit pomocí autokorelační funkce
- **Cyklické změny** - fluktuace bez pravidelné periody. Občas se projeví, ale nedá se predikovat kdy. Pokud se projeví, tak se ale dá predikovat její průběh
- další nepravidelné fluktuace
<!--ID: 1729010153950-->



Definujte momenty časových řad: stř. hodnota, ropzptyl, autokovariance #flashcard 
střední hodnota: $\mu_t = \mathbb{E}[X_t]$
variance: $\sigma_t^2 = \operatorname{var} X_t$
autokovariance: $\gamma(t_1, t_2) = \operatorname{cov}(X_{t_1}, X_{t_2}) = \mathbb{E}[(X_{t_1} - \mu_{t_1})(X_{t_2} - \mu_{t_2})]$.
<!--ID: 1729010153951-->



Aditivní a multiplikativní dekompozice časových řad. #flashcard 
Časovou řadu lze často rozložit na jednotlivé uvedené složky, přičemž cyklické změny a nepravidelné fluktuace se sloučí do jedné.
**aditivní**: $Y_t = T_t + S_t + E_t$,
**multiplikativní**: $Y_t = T_t \cdot S_t \cdot E_t$,
kde $Y_t$ je pozorovaná veličina v čase $t$, $T_t$ je hodnota trendu, $S_t$ je sezónní složka a $E_T$ nevysvětlená složka. V aditivních modelech obecně platí, že amplituda sezónních složek je přibližně stejná, zatímco v multiplikativních se s rostoucím trendem zvyšuje i sezónní amplituda (a naopak). 
<!--ID: 1729010153952-->




# Druhy stacionarity a rozdíl mezi nimi


**Stacionarita časových řad** - definice, druhy: #flashcard 
Stacionarita říká, jaký má vliv posun o libovolný čas na sdruženou distribuci.
Časová řada je:
* **striktně (silně) stacionární**, pokud sdružená distribuce $X_{t_1},\ldots, X_{t_n}$ je stejná, jako sdružená distribuce $X_{t_1+\tau},\ldots, X_{t_n+\tau}$ pro všechna $t_1, \ldots, t_n, \tau$.
* **slabě stacionární**, pokud je invariantní vůči posunům v čase pouze v rámci momentů rozdělení do druhého řádu: $\mathbb{E}[X_t] = \mu,  \operatorname{cov}(X_t, X_{t+\tau}) = \gamma(\tau)$
Budeme-li tedy uvažovat $n=1$, potom striktní stacionarita znamená, že distribuce $X_{t}$ je stejná pro všechna $t$ a rovněž momenty $\mu = \mu_t$ a $\sigma^2 = \sigma_t^2$ jsou v čase konstantní.
<!--ID: 1729010153953-->



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
<!--ID: 1729010153954-->



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
<!--ID: 1729010153955-->



# Autoregresní modely (AR) a modely klouzavých průměrů (MA)
základní vlastnosti modelů/procesů, jejich stacionarita. Zápis AR a MA, včetně zápisu pomocí operátoru zpoždění. Identifikace řádů AR a MA z autokorelačních funkcí a pomocí informačních kritérií.


Definujte autokorelační funkci. K čemu slouží? (ACF) #flashcard 
Funkce, která vrací korelaci hodnot časové řay v různých časových okamžicích.
$R(s, t)=\frac{\mathbb{E}\left[\left(X_{t}-\mu_{t}\right)\left(X_{s}-\mu_{s}\right)\right]}{\sigma_{t} \sigma_{s}}, \quad R(s, t) \in[-1,1]$
<!--ID: 1729010153956-->



Definujte parciální autokorelační funkci. K čemu slouží? (PACF) #flashcard 
Funkce, která vrací korelaci hodnot časové řady v různých časových okamžicích s tím, že předtím odstraníme lineární vliv mezilehlých hodnot.
<!--ID: 1729010153957-->



Jak se dá interpretovat parcilání korelační koeficient? #flashcard 
Mám veličinu $X$, $Y$, $Z$. Chci změřit parciální korelaci mezi $X$ a $Z$, ale chci odstranit lineární vliv $Y$ na hodnoty $X$ a $Z$.
1. Proložím regresní přímku mezi $X$ a $Y$
2. Proložím regresní přímku mezi $Z$ a $Y$
3. změřím korelaci mezi rezidui 
```python
import statsmodels.api as sm
model1 = sm.OLS(X, sm.add_constant(Y)).fit()
model2 = sm.OLS(Z, sm.add_constant(Y)).fit()
np.corrcoef(model1.resid, model2.resid)
# sm.add_constant(arr) adds a column of ones to an array arr.
```
<!--ID: 1729010153958-->



Definuj autoregresní model řádu p. Jaké má momenty? #flashcard 
$X_{t}=c+\phi_{1} X_{t-1}+\ldots+\phi_{p} X_{t-p}+\varepsilon_{t}$
lidově: Následující hodnota se odvíjí od hodnot minulých (šum je nezávislý, p - délka historie)
Momenty závisí na stacionaritě. Pokud je stacionární, tak jdou dopočítat. Pokud stacionární není, tak se mění v čase a lze tvrdit, že jsou limitně nekonečno.
<!--ID: 1729010153959-->



Zápis moving average modelu včetně operátoru zpoždění. #flashcard 
MA(p) lze zapsat jako:
$X_{t}=\mu+\varepsilon_{t}+\theta_{1} \varepsilon_{t-1}+\theta_{2} \varepsilon_{t-2}+\ldots+\theta_{q} \varepsilon_{t-q}, \quad \varepsilon_{t} \sim$ iid $\mathcal{N}\left(0, \sigma^{2}\right)$
Pomocí operátoru zpoždění:
$$X_t=\left(1+\sum_{i=1}^q \theta_i B^i\right) \varepsilon_t$$
<!--ID: 1729010153960-->



Zápis autoregresního modelu včetně operátoru zpoždění. #flashcard 
Autoregresní model řádu p se dá napsat jako: $X_{t}=c+\phi_{1} X_{t-1}+\ldots+\phi_{p} X_{t-p}+\varepsilon_{t}$
Pomocí operátoru zpoždění vyjádříme $\varepsilon_t$:
$$
\varepsilon_t=X_t-\phi_1 B^1 X_t-\ldots-\phi_p B^p X_t=\left(1-\sum_{i=1}^p \phi_i B^i\right) X_t
$$
<!--ID: 1729010153961-->



Jak se chová ACF a PACF, když je pošleš na AR proces řádu p? #flashcard 
ACF klesá, PACF klesá pouze do lagu p. (Hodnoty ve funkci můžou být střídavě kladné, záporné atd.)
![[AR_ACF_PACF.png]]
<!--ID: 1729010153962-->



Jak se dá detekovat řád AR procesu? #flashcard 
Pomocí PACF. Funkce bude mít tolik peaků, kolik je řád. Na obrázku AR(1)
![[AR_ACF_PACF.png]]
<!--ID: 1729010153963-->



Co je moving average model řádu p? MA(p) Jaké má momenty? #flashcard 
$X_{t}=\mu+\varepsilon_{t}+\theta_{1} \varepsilon_{t-1}+\theta_{2} \varepsilon_{t-2}+\ldots+\theta_{q} \varepsilon_{t-q}, \quad \varepsilon_{t} \sim$ iid $\mathcal{N}\left(0, \sigma^{2}\right)$
lidově: Následující hodnota se odvíjí od minulého šumu (známé hodnoty jsou nezávislé, p - délka historie)
$\mathbb{E}\left[X_t\right]=c, \quad \operatorname{var} X_t=\sigma^2 \cdot \sum_{i=0}^q \theta_i^2$
<!--ID: 1729010153964-->



Jak detekuješ MA proces? #flashcard 
ACF klesá a pak jde strmě k nule, PACF klesá postupně. (Hodnoty ve funkci můžou být střídavě kladné, záporné atd.)
![[MA_ACF_PACF.png]]
<!--ID: 1729010153965-->



Co je invertibilita MA procesů? #flashcard 
Vlastnost některých MA modelů. MA model je invertibilní, pokud ho lze přepsat na AR($\infty$)
Zamysli se, jak bude vypadat ACF a PACF pro MA a pro AR($\infty$)
<!--ID: 1729010153966-->



Co je ARMA(p, q) model a jak se od něj liší ARIMA(p, d, q)? #flashcard 
**ARMA(p, q)** je smíšený model AR(p) a MA(q) - rovnice je prakticky jen součet těch dvou modelů. Předpoklad pro funkci ARMA je slabá stacionarita.
**ARIMA(p, d, q)** oproti ARMA nemá jako předpoklad slabou stacionaritu. Dělá to tak, že používá metodu diferencí. t.j. $X_t^` = X_t - X_{t-1}$
Pozor. řady nelze vždy "zestacionárnit".
<!--ID: 1729010153967-->



Jak se řada nechá zestacionárnit pomocí diferencování? #flashcard 
Diferencováním se můžeme zbavovat trendu. Typicky nám stačí diferencovat 2x.
* Mám náhodnou procházku (s driftem), tu diferencuju -> bílý šum.
	* Mám bílý šum, ten diferencuju -> MA(1) == přehnal jsem to. Ideální je končit na WN.
![[stac-diff.png]]
<!--ID: 1729010153968-->



Jak vypadá operátor zpoždění B a operátor difference $\Delta$? #flashcard 
$$
\begin{aligned}
& BX_t = X_{t-1} \\
& B^{-1}X_t = X_{t+1} \\
& \Delta X_t = X_t - X_{t-1} = (1-B)X_t \\
& \Delta^kX_t = (1-B)^kX_t
\end{aligned}
$$
-   umožňují snadný zápis charakteristických polynomů při vyšetřování stacionarity AR a invertibility MA procesu.
-   jde s nimi dělat různá algebraická kouzla díky komutativitě $B(\beta X_t)=\beta B X_t$ distributivitě atd.
<!--ID: 1729010153969-->



Co ověřuje Z-test koeficientů (SCR)? #flashcard 
Test ověřuje nenulovost jednotlivých koeficientů modelu, např. pro ARMA(1,0) máme hypotézu o AR koeficientu $\phi_1$ v 1. zpoždění v podobě
$$
\begin{aligned}
H_0&: \phi_1 \equiv \text{AR.L1} = 0, \\
H_1&: \phi_1 \equiv \text{AR.L1} \ne 0.
\end{aligned}
$$
Test počítá $Z$ statistiku, $p$-hodnotu a $(1-\alpha)\%$ interval spolehlivosti pro příslušné koeficienty. Zajímají nás především nejvyšší koeficienty modelu, např. pro ARMA(2, 3) by to byly $\phi_2$ a $\theta_3$.
<!--ID: 1729010153970-->



Co ověřuje Ljung-Box Q test? #flashcard 
Je to test nad časovými řadami.
$H_0$ říká, že jsou data nekorelovaná a nezávislá. (A časové řady se tím myslí autokorelace) U predikce se tím myslí nekorelovanost standardizovaných reziduí (chyb predikce)
<!--ID: 1729010153971-->



Co ověřuje test heteroskedasticity? #flashcard 
Je to test nad časovými řadami.
$H_0$ říká, že standardizovaná rezidua (chyby predikce) jsou heteroskedastická. Heteroskedasticita je opak homoskedasticity. Řada je homoskedastická, pokud má konstantní rozptyl. Řada je heteroskedastická, pokud se rozptyl mění.
<!--ID: 1729010153972-->



Definuj heteroskedasticitu u časových řad. #flashcard 
Heteroskedasticita je opak homoskedasticity. Řada je homoskedastická, pokud má konstantní rozptyl. Řada je heteroskedastická, pokud se rozptyl mění.
<!--ID: 1729010153973-->



Co ověřuje Jarque-Bera test? #flashcard 
Je to test nad čas. řadami.
$H_0$ ověřuje, že data mají stejnou výběrovou šikmost a špičatost jako normální rozdělení.
<!--ID: 1729010153974-->



**AIC - [Akaikeho informační kritérium](https://en.wikipedia.org/wiki/Akaike_information_criterion)** #flashcard 
Používá se na automatické hledání řádů. Hodnotu AIC minimalizujeme.
Označme počet odhadovaných parametrů $k$ a maximální hodnotu věrohodnosti při daném modelu $\mathcal{L}$. Potom kritérium je číslo
$$
\mathrm{AIC} = 2k - 2\ln \mathcal{L}.
$$
Kritérium je asymptoticky ekvivalentní ke křížové validaci.
<!--ID: 1729010153975-->



**BIC - [Bayesovské informační kritérium](https://en.wikipedia.org/wiki/Bayesian_information_criterion)** #flashcard 
Používá se na automatické hledání řádů. Hodnotu BIC minimalizujeme.
Označme navíc počet pozorování $n$. Potom kritériem je číslo
$$
\mathrm{BIC} = k \ln(n) - 2\ln \mathcal{L}.
$$
<!--ID: 1729010153976-->

