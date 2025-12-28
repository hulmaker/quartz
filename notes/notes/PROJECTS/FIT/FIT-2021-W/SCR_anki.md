TARGET DECK: FIT-2021-W
FILE TAGS: SCR FIT-2021-W

# 01 - Úvod, exponenciální vyhlazování

Cíle analýzy časových řad #flashcard 
1. Popis pozorovaného jevu - rozsahy, perioda, vývoj, outliers, extremy, zavislosti
2. predikce vývoje/interpolace minulého vývoje
3. řízení - řízení vývoje procesu (epidemie, cena atd)
<!--ID: 1632861184450-->


Co je trend? #flashcard 
1. trend - dlouhodobý vývoj střední hodnoty
<!--ID: 1638857393542-->



Co je sezonnost #flashcard 
2. sezónnost - periodicky se opakující, poměrně pravidelný a předpověditelný (očekávatelný) vývoj časové řady. Typické jsou například vývoje teploty v průběhu roku, počet zákazníků v pneuservisech, počet zaměstnanců v zemědělství, počet zákazníků v horských centrech apod. Sezónnost můžeme celkem dobře analyzovat v příslušném [grafu sezónnosti](https://en.wikipedia.org/wiki/Seasonal_subseries_plot), či lépe v řadě box plotů, oba vyžadují znalost periody. Tu můžeme zjistit pomocí _autokorelační funkce_ (ACF). Pro analýzu sezónnosti je ale vždy potřeba nejprve odstranit _trend_.
<!--ID: 1638857393548-->



Co jsou cyklicke zmeny #flashcard 
3. Cyklické změny - fluktuace bez pravidelné periody. Občas se projeví, ale nedá se predikovat kdy. Pokud se projeví, tak se ale dá predikovat její průběh
<!--ID: 1638857393553-->



Jaké vlastnosti u časových řad pozorujeme? #flashcard 
1. trend - dlouhodobý vývoj střední hodnoty
2. sezónnost - pravidelný, periodický predikovatelný pattern. Perioda se dá zjistit pomocí autokorelační funkce
3. Cyklické změny - fluktuace bez pravidelné periody. Občas se projeví, ale nedá se predikovat kdy. Pokud se projeví, tak se ale dá predikovat její průběh
4. další nepravidelné fluktuace
<!--ID: 1632861184455-->



Definuj stacionaritu, je bilý šum stacionární? #flashcard 
* Řada je **striktně** stacionární, pokud sdružená distribuce $X_{t1}, ..., X_{tn}$ je stejná jako $X_{t1+r}, ..., X_{tn+r}$ pro všechna $t_1, ..., t_n$ -> distribuce je invariantní vůči časovému posunu.
* Řada je **slabě** stacionární, pokud je invariantní vůči posunům v čase pouze v rámci momentů rozdělení do druhého řádu, tj. konstantní mean a cov
<!--ID: 1643302120910-->



Bilý šum je stacionární, prvky jsou na sobě nezávislé a mají stejnou distribuci nezávisle na posunu.
<!--ID: 1632861184461-->


Jaký je princip simple exponential smoothing (SES)? #flashcard 
Vývoj řady v čase $t+1$ je vážená kombinace jeho předchůdců, kdy váhy exponenciálně slábnou tak jak jsou vzdálené v minulosti.
$\hat{y}_{t+1 \mid t} = \sum_{j=0}^{T} \alpha(1-\alpha)^{j} y_{T-j} = \alpha y_{t}+(1-\alpha) \hat{y}_{t \mid t-1}$
hodnota alfy se dá odhadovat pomocí LS.
<!--ID: 1632861184465-->



Popiš komponentní formu simple exponential smoothing (SES) #flashcard 
Je to jen jiný zápis vážených průměrů pomocí rekurentní formy rovnice.
**Forecast eq.**: $\hat{y}_{t+h \mid t}=l_{t}$
**Smoothing eq.**: $l_{t}=\alpha y_{t}+(1-\alpha) l_{t-1}$
<!--ID: 1632861184470-->


Jaký je princip double exponential smoothing (DES)? #flashcard 
Rozšíření SES, kdy se bere ohled i na trend. Existuje tlumená varianta, kde se díky parametru tlumí v každém kroku trend. Nejde tudíž do nekonečna.
Rovnice jsou tedy 3: **Forecast**, **Smoothing**, **Trend**
* Existuje model, co tlumí trend nějakými váhami - Holtova metoda s tlumeným trendem (když není trend invariantní)
<!--ID: 1632861184475-->



Jaký je princip triple exponential smoothing (Holt-Winters)? #flashcard 
Rozšíření DES a SES, kdy se bere v potaz i sezónost. Metoda existuje v aditivní i v multiplikativní formě.
* Rovnice jsou tedy 4: **Forecast**, **Smoothing**, **Trend**, **Seasonal**
<!--ID: 1632861184479-->


# 02 - ACF, PACF, autoregresní modely

Co dělá autokorelační funkce? (ACF) #flashcard 
Funkce, která vrací korelaci hodnot časové řay v různých časových okamžicích.
$R(s, t)=\frac{\mathbb{E}\left[\left(X_{t}-\mu_{t}\right)\left(X_{s}-\mu_{s}\right)\right]}{\sigma_{t} \sigma_{s}}, \quad R(s, t) \in[-1,1]$
<!--ID: 1633690648847-->



Co dělá parciální autokorelační funkce? (PACF) #flashcard 
Funkce, která vrací korelaci hodnot časové řady v různých časových okamžicích s tím, že předtím odstraníme lineární vliv mezilehlých hodnot.
<!--ID: 1633690648851-->



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
<!--ID: 1633690648855-->


# sm.add_constant(arr) adds a column of ones to an array arr.
```


Definuj autoregresní model řádu p #flashcard 
$X_{t}=c+\phi_{1} X_{t-1}+\ldots+\phi_{p} X_{t-p}+\varepsilon_{t}$
lidově: Následující hodnota se odvíjí od hodnot minulých (šum je nezávislý, p - délka historie)
<!--ID: 1633690648858-->



Jak se chová ACF a PACF, když je pošleš na AR proces řádu p? #flashcard 
ACF klesá, PACF klesá pouze do lagu p. (Hodnoty ve funkci můžou být střídavě kladné, záporné atd.)
![[AR_ACF_PACF.png]]
<!--ID: 1633690648862-->



Jak se dá detekovat řád AR procesu? #flashcard 
Pomocí PACF. Funkce bude mít tolik peaků, kolik je řád. Na obrázku AR(1)
![[AR_ACF_PACF.png]]
<!--ID: 1633690648866-->



# 03 - MA, ARMA

Co je moving average model řádu p? MA(p) #flashcard 
$X_{t}=\mu+\varepsilon_{t}+\theta_{1} \varepsilon_{t-1}+\theta_{2} \varepsilon_{t-2}+\ldots+\theta_{q} \varepsilon_{t-q}, \quad \varepsilon_{t} \sim$ iid $\mathcal{N}\left(0, \sigma^{2}\right)$
lidově: Následující hodnota se odvíjí od minulého šumu (známé hodnoty jsou nezávislé, p - délka historie)
<!--ID: 1633690648870-->



Jak detekuješ MA proces? #flashcard 
ACF klesá a pak jde strmě k nule, PACF klesá postupně. (Hodnoty ve funkci můžou být střídavě kladné, záporné atd.)
![[MA_ACF_PACF.png]]
<!--ID: 1633690648874-->



Co je invertibilita MA procesů? #flashcard 
Vlastnost některých MA modelů. MA model je invertibilní, pokud ho lze přepsat na AR($\infty$)
Zamysli se, jak bude vypadat ACF a PACF pro MA a pro AR($\infty$)
<!--ID: 1633690648878-->



Co je ARMA(p, q) model a jak se od něj liší ARIMA(p, d, q)? #flashcard 
**ARMA(p, q)** je smíšený model AR(p) a MA(q) - rovnice je prakticky jen součet těch dvou modelů. Předpoklad pro funkci ARMA je slabá stacionarita.
**ARIMA(p, d, q)** oproti ARMA nemá jako předpoklad slabou stacionaritu. Dělá to tak, že používá metodu diferencí. t.j. $X_t^` = X_t - X_{t-1}$
Pozor. řady nelze vždy "zestacionárnit".
<!--ID: 1633690648882-->

Jak se řada nechá zestacionárnit pomocí diferencování? #flashcard 
Diferencováním se můžeme zbavovat trendu. Typicky nám stačí diferencovat 2x.
* Mám náhodnou procházku (s driftem), tu diferencuju -> bílý šum.
* Mám bílý šum, ten diferencuju -> MA(1) == přehnal jsem to. Ideální je končit na WN.
![[stac-diff.png]]
<!--ID: 1638857393557-->



# 04 - ARIMA, testy


Jak vypadá operátor zpoždění B a operátor difference $\Delta$? #flashcard 
$$BX_t = X_{t-1}$$
$$\Delta X_t = X_t - X_{t-1} = (1-B)X_t$$
-   umožňují snadný zápis charakteristických polynomů při vyšetřování stacionarity AR a invertibility MA procesu.
-   jde s nimi dělat různá algebraická kouzla díky komutativitě $B(\beta X_t)=\beta B X_t$ distributivitě atd.
<!--ID: 1638857393561-->



Co ověřuje Z-test koeficientů? #flashcard 
$H_0$ testuje, zda jsou keoficienty nulové. (v nějakém intervalu spolehlivosti)
<!--ID: 1634677490393-->



Co ověřuje Ljung-Box Q test? #flashcard 
$H_0$ říká, že jsou data nekorelovaná a nezávislá. (A časové řady se tím myslí autokorelace) U predikce se tím myslí nekorelovanost standardizovaných reziduí (chyb predikce)
<!--ID: 1634677490398-->



Co ověřuje test heteroskedasticity? #flashcard 
$H_0$ říká, že standardizovaná rezidua (chyby predikce) jsou heteroskedastická. Heteroskedasticita je opak homoskedasticity. Řada je homoskedastická, pokud má konstantní rozptyl. Řada je heteroskedastická, pokud se rozptyl mění.
<!--ID: 1634677490402-->



Definuj heteroskedasticitu u časových řad. #flashcard 
Heteroskedasticita je opak homoskedasticity. Řada je homoskedastická, pokud má konstantní rozptyl. Řada je heteroskedastická, pokud se rozptyl mění.
<!--ID: 1634677490406-->



Co ověřuje Jarque-Bera test? #flashcard 
$H_0$ ověřuje, že data mají stejnou výběrovou šikmost a špičatost jako normální rozdělení.
<!--ID: 1634677490410-->
