TARGET DECK: NI-ZI-2023::NI-SCR
FILE TAGS: NI-ZI-2023 NI-ZI-21 NI-SCR

prev::[[NI-ZI-20]]
next::[[NI-ZI-22]]

# Autoregresní modely (AR) a modely klouzavých průměrů (MA)
základní vlastnosti modelů/procesů, jejich stacionarita. Zápis AR a MA, včetně zápisu pomocí operátoru zpoždění. Identifikace řádů AR a MA z autokorelačních funkcí a pomocí informačních kritérií.


Co dělá autokorelační funkce? (ACF) #flashcard 
Funkce, která vrací korelaci hodnot časové řay v různých časových okamžicích.
$R(s, t)=\frac{\mathbb{E}\left[\left(X_{t}-\mu_{t}\right)\left(X_{s}-\mu_{s}\right)\right]}{\sigma_{t} \sigma_{s}}, \quad R(s, t) \in[-1,1]$
<!--ID: 1692477065965-->


Co dělá parciální autokorelační funkce? (PACF) #flashcard 
Funkce, která vrací korelaci hodnot časové řady v různých časových okamžicích s tím, že předtím odstraníme lineární vliv mezilehlých hodnot.
<!--ID: 1692477065972-->


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
<!--ID: 1692477065976-->


Definuj autoregresní model řádu p. Jaké má momenty? #flashcard 
$X_{t}=c+\phi_{1} X_{t-1}+\ldots+\phi_{p} X_{t-p}+\varepsilon_{t}$
lidově: Následující hodnota se odvíjí od hodnot minulých (šum je nezávislý, p - délka historie)
Momenty závisí na stacionaritě. Pokud je stacionární, tak jdou dopočítat. Pokud stacionární není, tak se mění v čase a lze tvrdit, že jsou limitně nekonečno.
<!--ID: 1692886189396-->



Zápis moving average modelu včetně operátoru zpoždění. #flashcard 
MA(p) lze zapsat jako:
$X_{t}=\mu+\varepsilon_{t}+\theta_{1} \varepsilon_{t-1}+\theta_{2} \varepsilon_{t-2}+\ldots+\theta_{q} \varepsilon_{t-q}, \quad \varepsilon_{t} \sim$ iid $\mathcal{N}\left(0, \sigma^{2}\right)$
Pomocí operátoru zpoždění:
$$X_t=\left(1+\sum_{i=1}^q \theta_i B^i\right) \varepsilon_t$$
<!--ID: 1692886189399-->


Zápis autoregresního modelu včetně operátoru zpoždění. #flashcard 
Autoregresní model řádu p se dá napsat jako: $X_{t}=c+\phi_{1} X_{t-1}+\ldots+\phi_{p} X_{t-p}+\varepsilon_{t}$
Pomocí operátoru zpoždění vyjádříme $\varepsilon_t$:
$$
\varepsilon_t=X_t-\phi_1 B^1 X_t-\ldots-\phi_p B^p X_t=\left(1-\sum_{i=1}^p \phi_i B^i\right) X_t
$$
<!--ID: 1692886189402-->



Charakteristická rovnice AR(p) procesu. Souvislost se stacionaritou. #flashcard 
Vektor regresních koeficientů: $[c, \phi_1, ..., \phi_p]^T$
Charakteristická rovnice: $1 - \phi_1 z - \phi_2 z^2 - \ldots - \phi_p z^p  = 0$
Pokud kořeny charakteristické rovnice leží vně jednotkové kružnice, tak proces JE slabě stacionární. tj. pro každé (komplexní) $z_i\in\mathbb{C}$ platí $|z_i| > 1$. 
<!--ID: 1692886189405-->



Jak se chová ACF a PACF, když je pošleš na AR proces řádu p? #flashcard 
ACF klesá, PACF klesá pouze do lagu p. (Hodnoty ve funkci můžou být střídavě kladné, záporné atd.)
![[AR_ACF_PACF.png]]
<!--ID: 1692477065982-->



Jak se dá detekovat řád AR procesu? #flashcard 
Pomocí PACF. Funkce bude mít tolik peaků, kolik je řád. Na obrázku AR(1)
![[AR_ACF_PACF.png]]
<!--ID: 1692477065984-->



Co je moving average model řádu p? MA(p) Jaké má momenty? #flashcard 
$X_{t}=\mu+\varepsilon_{t}+\theta_{1} \varepsilon_{t-1}+\theta_{2} \varepsilon_{t-2}+\ldots+\theta_{q} \varepsilon_{t-q}, \quad \varepsilon_{t} \sim$ iid $\mathcal{N}\left(0, \sigma^{2}\right)$
lidově: Následující hodnota se odvíjí od minulého šumu (známé hodnoty jsou nezávislé, p - délka historie)
$\mathbb{E}\left[X_t\right]=c, \quad \operatorname{var} X_t=\sigma^2 \cdot \sum_{i=0}^q \theta_i^2$
<!--ID: 1692477065987-->



Jak detekuješ MA proces? #flashcard 
ACF klesá a pak jde strmě k nule, PACF klesá postupně. (Hodnoty ve funkci můžou být střídavě kladné, záporné atd.)
![[MA_ACF_PACF.png]]
<!--ID: 1692477065989-->



Co je invertibilita MA procesů? #flashcard 
Vlastnost některých MA modelů. MA model je invertibilní, pokud ho lze přepsat na AR($\infty$)
Zamysli se, jak bude vypadat ACF a PACF pro MA a pro AR($\infty$)
<!--ID: 1692477065991-->



Co je ARMA(p, q) model a jak se od něj liší ARIMA(p, d, q)? #flashcard 
**ARMA(p, q)** je smíšený model AR(p) a MA(q) - rovnice je prakticky jen součet těch dvou modelů. Předpoklad pro funkci ARMA je slabá stacionarita.
**ARIMA(p, d, q)** oproti ARMA nemá jako předpoklad slabou stacionaritu. Dělá to tak, že používá metodu diferencí. t.j. $X_t^` = X_t - X_{t-1}$
Pozor. řady nelze vždy "zestacionárnit".
<!--ID: 1692477065993-->



Jak se řada nechá zestacionárnit pomocí diferencování? #flashcard 
Diferencováním se můžeme zbavovat trendu. Typicky nám stačí diferencovat 2x.
* Mám náhodnou procházku (s driftem), tu diferencuju -> bílý šum.
	* Mám bílý šum, ten diferencuju -> MA(1) == přehnal jsem to. Ideální je končit na WN.
![[stac-diff.png]]
<!--ID: 1692477065995-->




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
<!--ID: 1692477065997-->


Co ověřuje Z-test koeficientů (SCR)? #flashcard 
Test ověřuje nenulovost jednotlivých koeficientů modelu, např. pro ARMA(1,0) máme hypotézu o AR koeficientu $\phi_1$ v 1. zpoždění v podobě
$$
\begin{aligned}
H_0&: \phi_1 \equiv \text{AR.L1} = 0, \\
H_1&: \phi_1 \equiv \text{AR.L1} \ne 0.
\end{aligned}
$$
Test počítá $Z$ statistiku, $p$-hodnotu a $(1-\alpha)\%$ interval spolehlivosti pro příslušné koeficienty. Zajímají nás především nejvyšší koeficienty modelu, např. pro ARMA(2, 3) by to byly $\phi_2$ a $\theta_3$.
<!--ID: 1692886189409-->



Co ověřuje Ljung-Box Q test? #flashcard 
Je to test nad časovými řadami.
$H_0$ říká, že jsou data nekorelovaná a nezávislá. (A časové řady se tím myslí autokorelace) U predikce se tím myslí nekorelovanost standardizovaných reziduí (chyb predikce)
<!--ID: 1692886189412-->



Co ověřuje test heteroskedasticity? #flashcard 
Je to test nad časovými řadami.
$H_0$ říká, že standardizovaná rezidua (chyby predikce) jsou heteroskedastická. Heteroskedasticita je opak homoskedasticity. Řada je homoskedastická, pokud má konstantní rozptyl. Řada je heteroskedastická, pokud se rozptyl mění.
<!--ID: 1692886189415-->




Definuj heteroskedasticitu u časových řad. #flashcard 
Heteroskedasticita je opak homoskedasticity. Řada je homoskedastická, pokud má konstantní rozptyl. Řada je heteroskedastická, pokud se rozptyl mění.
<!--ID: 1692886189418-->



Co ověřuje Jarque-Bera test? #flashcard 
Je to test nad čas. řadami.
$H_0$ ověřuje, že data mají stejnou výběrovou šikmost a špičatost jako normální rozdělení.
<!--ID: 1692886189421-->



**AIC - [Akaikeho informační kritérium](https://en.wikipedia.org/wiki/Akaike_information_criterion)** #flashcard 
Používá se na automatické hledání řádů. Hodnotu AIC minimalizujeme.
Označme počet odhadovaných parametrů $k$ a maximální hodnotu věrohodnosti při daném modelu $\mathcal{L}$. Potom kritérium je číslo
$$
\mathrm{AIC} = 2k - 2\ln \mathcal{L}.
$$
Kritérium je asymptoticky ekvivalentní ke křížové validaci.
<!--ID: 1692886189424-->



**BIC - [Bayesovské informační kritérium](https://en.wikipedia.org/wiki/Bayesian_information_criterion)** #flashcard 
Používá se na automatické hledání řádů. Hodnotu BIC minimalizujeme.
Označme navíc počet pozorování $n$. Potom kritériem je číslo
$$
\mathrm{BIC} = k \ln(n) - 2\ln \mathcal{L}.
$$
<!--ID: 1692886189428-->
