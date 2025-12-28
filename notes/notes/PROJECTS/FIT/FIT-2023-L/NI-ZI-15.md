TARGET DECK: NI-ZI-2023::NI-BML
FILE TAGS: NI-ZI-2023 NI-ZI-15 NI-BML

prev::[[NI-ZI-14]]
next::[[NI-ZI-16]]

# Stavové modely
 - rovnice pro vývoj stavu a rovnice měření, rozdíly mezi nimi. Bayesovský sekvenční odhad stavových modelů a jejich vliv na apriorní distribuci (znalost). Možnosti odhadu stavů v případě nelinearity (pouze vyjmenovat).


Definice stavového modelu rovnice pro vývoj stavu a rovnice měření (NI-BML) #flashcard 
Stavový model systému nebo procesu má tři veličiny:
- **stav**: $x_t$ nemůžeme jej pozorovat, ale můžeme jej odhadovat
- **vstup**: $u_t$ nazývaný **řídící veličina**, známe ho
- **výstup**: $y_t$, pozorovatelná veličina determinovaná $x_t$ a $u_t$
Stavový model může být v čase buď **diskrétní** (náš případ), nebo **spojitý**. Je-li systém lineární, potom jej můžeme zapsat:
Nelineární stavové modely jsou opět ve tvaru
$$
\begin{aligned}
x_t &= A_t x_{t-1} + B_t u_t + w_t &= f_t(x_{t-1}, u_t), \\
y_t &= H_t x_t + \varepsilon_t  &= g_t(x_t),
\end{aligned}
$$
$w_t$ a $v_t$ jsou **šum stavu** a **šum měření** a $A_t, B_t$ a $H_t$ jsou matice patřičných rozměrů. Pokud je systém časově invariantní, jsou matice konstantní, $A_t=A, B_t=B, H_t=H$. Za druhým rovnítkem je funkcionální zápic co toho hodne schová.
<!--ID: 1691601081099-->



Jak vypadá markovský model n-tého řádu? #flashcard 
Markovský proces (markovský model 1. řádu), je model, v němž aktuální stav závisí pouze na stavu předchozím.
$$
\begin{alignat}{2}
&p(x_t|x_{t-1}) &&\qquad\text{(pravděpodobnost přechodu)}, \\
&p(x_0) &&\qquad\text{(počáteční stav)}.
\end{alignat}
$$
Aktuální stav modelu $n$-tého řádu závisí na n předchozích stavech: $p(x_t|x_{t-1},...,x_{t-n})$. To ovšem vede k náročnějším výpočtům.
<!--ID: 1691601081103-->



Stručně popiš co je Markovský model (Hidden Markov Model - HMM) #flashcard 
Takový Markovský, který není přímo pozorovatelný, ale lze na něj nahlížet prostřednictvím jiné pozorovatelné veličiny.
<!--ID: 1691601081107-->



Vyberte správné tvrzení o stavové veličině 1) Jde o veličinu, jejíž hodnotu známe a priori 2) Jde o veličinu, jejíž hodnotu známe a posteriori, 3) Jde o veličinu, kterou nelze přímo měřit #flashcard 
Jde o veličinu, kterou nelze přímo měřit
<!--ID: 1691601081110-->



Lineární stavové modely 1) se sestávají z rovnice pro predikci budoucích měření a rovnice měření. 2) Ani jedna z ostatních odpovědí není správně 3) se sestávají z rovnice pro vývoj stavu a rovnice měření. #flashcard 
se sestávají z rovnice pro vývoj stavu a rovnice měření.
<!--ID: 1691601081112-->


# Kalmanuv filtr


Sestav a popiš stavový model Kalmanova filtru pro 
$$
\begin{aligned}
h_{t}&=h_{0}+v_{0} \Delta_{t}-\frac{1}{2} g \Delta_{t}^{2}+w_{h, t} \\
v_{t}&=v_{0}-g \Delta_{t}+w_{v, t} \\
\end{aligned}
$$
Z něho odvoď obecný stavový model pro KF. #flashcard 
Stavový model:
$$
\begin{aligned} 
X_{t} &=\left[\begin{array}{cc}1 & \Delta_{t} \\ 0 & 1\end{array}\right] X_{t-1}+\left[\begin{array}{c}-\frac{1}{2} \Delta_{t}^{2} \\ -\Delta_{t}\end{array}\right] g+\left[\begin{array}{l}w_{h, t} \\ w_{v, t}\end{array}\right] \\ 
y_{h, t} &=\left[\begin{array}{cc}1 & 0\end{array}\right] X_{t}+\varepsilon_{t} 
\end{aligned}
$$
Obecný stavový model pro KF.
$$
\begin{aligned}
X_{t}&=A_{t} X_{t-1}+B_{t} u_{t}+w_{t} \\
y_{t}&=H_{t} X_{t}+\varepsilon_{t}
\end{aligned}
$$
kde $X_t$ je **stav**, $y_t$ jsou naměřené hodnoty, $u_t$ je **řídící veličina**, $w_t$ a $\varepsilon_t$ jsou **šum stavu** a **šum měření** a $A_t, B_t$ a $H_t$ jsou matice patřičných rozměrů.
<!--ID: 1691601081113-->



Kalmanův filtr 1) reprezentuje měření jako nelineární funkce stavů.  2) filtruje měření od šumu, tj. interpoluje data. 3) odhaduje hodnoty stavů z dostupných měření. #flashcard 
odhaduje hodnoty stavů z dostupných měření.
<!--ID: 1691601081115-->



V jakém kroku Kalmanova filtru uplatníme Bayesovu větu? #flashcard 
v updatu
<!--ID: 1691601081117-->



Pro použití Kalmanova filtru potřebujeme znát (mimo jiné) 1) hodnotu měření  2) hodnotu realizace šumové veličiny na stavech. 3) hodnotu stavu x #flashcard 
hodnotu měření 
<!--ID: 1691601081118-->



Kalmanův filtr: každý predikční krok 1) sníží hodnotu kovariance odhadu stavů.  2) nezmění hodnotu kovariance odhadu stavů. 3) zvýší hodnotu kovariance odhadu stavů. #flashcard 
zvýší hodnotu kovariance odhadu stavů.
<!--ID: 1691601081119-->



Kalmanův filtr předpokládá, že je stavový model 1) lineární, 2) lineární nebo slabě nelineární, 3) slabě či silně nelineární.
#flashcard 
stavový model je lineární.


Odvození kalmnaova filteru: Distribuce šumových proměnných, distribuce $x_t, y_t$ a apriorní distribuce $x_t$ #flashcard 
$$
\begin{aligned}
x_t &= A x_{t-1} + B u_t + w_t, \\
y_t &= H x_t + \varepsilon_t,
\end{aligned}
$$
šumové proměnné: $w_t \sim \mathcal{N}(0, Q), \varepsilon_t \sim \mathcal{N}(0, R)$
Normalita není nutná pro KF, ale my ji potřebujeme, z toho vidíme že:
$$
\begin{alignat}{2}
x_t &\sim \mathcal{N}(Ax_{t-1} + Bu_t, Q) &&\qquad\text{s hustotou}\quad p(x_t|x_{t-1}, u_t) \\
y_t &\sim \mathcal{N}(Hx_{t}, R) &&\qquad\text{s hustotou}\quad f(y_t|x_t).
\end{alignat}
$$
apriorní distribuce $x_t$: Model $y_t$ je normální, konjugované apriorno bude tedy rovněž normální se střední hodnotou označenou $x_{t-1}^{+}$ a kovarianční maticí $P_{t-1}^{+}$, $$
\pi(x_t|y_{0:t-1}, u_{0:t-1}) = \mathcal{N}(x_{t-1}^{+}, P_{t-1}^{+}).
$$
<!--ID: 1691601081121-->


Odvození predikce Kalmanova filteru pomocí bayesovského sekvenčního odhadu #flashcard 
řešíme časový vývoj stavu $x_{t-1} \to x_t$. Použijeme odhad reprezentovaný posledním aposteriornem, nyní apriornem pro další časový krok a ten "proženeme" modelem vývoje:
$$
\pi(x_{t}|y_{0:t-1}, u_{0:t})
= \int p(x_{t}|x_{t-1}, u_{t})\, \pi(x_{t-1}|y_{0:t-1}, u_{0:t-1})\, \mathrm{d}x_{t-1}.
$$
Násobíme dva Gausse a marginalizujeme -> dostaneme Gausse $\mathcal{N}(x_{t}^{-}, P_{t}^{-})$ s hyperparametry
$$
\begin{aligned}
    x_{t}^{-} &= A x_{t-1}^{+} + B u_{t}, \\
    P_{t}^{-} &= A P_{t-1}^{+} A^{\intercal} + Q.
\end{aligned}
$$
Odhad stavu $x_t^{-}$ je dosazení do rovnice v maticích. Kovariance odhadu $P_t^{-}$ je míra nejistoty odhadu.
<!--ID: 1691601081122-->



Odvození update pro Klamanův filtr pomocí bayesovského sekvenčního odhadu #flashcard 
Update "opraví" predikovaný odhad novými pozorováními $y_t$. K tomu slouží Bayesova věta:
$$
\pi(x_{t}|y_{0:t}, u_{0:t}) \propto f(y_{t}|x_{t}) \pi(x_{t}|y_{0:t-1}, u_{0:t})
$$
Když si přepíšeme model do tvaru distribuce z exponenciální třídy, tak je bayesovský update jen součet hyperparametru a suficientní statistiky: $\xi_{t}  = \xi_{t-1} +  T(y_{t})$
Pak odvodíme Aposteriorní parametry normálního rozdělení
$$
\begin{aligned}
    P_{t}^{+} &= (I - K_{t} H) P_{t}^{-} \\
    x_{t}^{+} &= x_{t}^{-} + P_{t}^{+} H^{\intercal} R^{-1}(y_{t} - Hx_{t}^{-})
\end{aligned}
$$
kde $K_{t} = P_{t}^{-} H^{\intercal}(R + H P_{t}^{-}H^{\intercal})$ je Kalmanovo zesílení
<!--ID: 1691601081123-->



# Možnosti odhadu stavů v případě nelinearity (pouze vyjmenovat)


Jaké znáte nelineární stavové modely? Lze používat lineární stavové modely v případě nelineární funkce? #flashcard 
Nelineární stavové modely jsou opět ve tvaru
$$
\begin{aligned}
x_t &= f_t(x_{t-1}, u_t), \\
y_t &= g_t(x_t),
\end{aligned}
$$
ovšem jedna nebo obě funkce již nejsou lineární. Zde je více možností řešení:
Slabá nelinearita: 
* lokálně linearizovat derivacemi prvního/druhého řádu
* extended kalman filter (neoptimální, může divergobat)
Větší nelinearita: unscented KF
Bruteforce: Monte Carlo, particle filter
<!--ID: 1691601081124-->
