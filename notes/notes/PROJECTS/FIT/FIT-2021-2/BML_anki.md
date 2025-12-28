TARGET DECK: FIT-2021-2
FILE TAGS: BML FIT-2021-2

## Lec 01 - 17.02.2021 - základy a specifika Bayesovské teorie

Silný zákon velkých čísel SZVC: $X_1, ..., X_n$ jsou i.i.d. náhodné veličiny a $EX_i = \mu$ #flashcard 
$$\bar{X}_{n} \stackrel{a.s.}{\rightarrow} \mu \quad \text{ pro } \quad n \rightarrow \infty$$ kde $\bar{X}_{n}(\omega)$ konverguje jako číselná posloupnost s pravděpodobností 1 (almost surely k $\mu$) $$\mathrm{P}\left(\left\{\omega \in \Omega: \bar{X}_{n}(\omega) \rightarrow \mu \text { při } n \rightarrow \infty\right\}\right)=1$$
<!--ID: 1613561383763-->


popiš význam apriori distribuce a aposteriori distribuce + jejich užití #flashcard 
**apriori** - (před) -> předpokládaná distribuce náhodné proměnné bez závislosti na naměřených datech
**aposteriori** - (potom) -> distribuce parametru náhodné proměnné v závislosti na naměřených datech.
Obě kvantifikují míru neurčitosti v naší znalosti o odhadovaném parametru.
<!--ID: 1613561383769-->


popiš rozdíl mezi frekventistickým (statistickým) přístupem a Bayesovským přístupem #flashcard 
**Statistika** - měří data a z nich určuje rozdělení pomocí histogramu atd. 
**Bayes** - díky a priori znalosti určí rozdělení a tu potom na základě měření mírně upravuje.
<!--ID: 1613561383774-->


dej příklady diskrétního pravděpodobnostního rozdělení #flashcard 
**Bernoulliho** - jeden hod (ne)vyváženou mincí
**Kategorické** - zobecněné Bernoulliho pro k tříd
**Binomické** - Počet hlav v n hodech (ne)vyváženou mincí.
**Multinomické** - Zobecněné Binomické pro k tříd.
**Geometrické** - Počet hodů nevyváženou mincí než padne první hlava.
**Poissonovo** - počet požadavků, co přijdou na server za 15s
<!--ID: 1613561383779-->


dej příklady spojitého pravděpodobnostního rozdělení #flashcard 
**Rovnoměrné** - uniformní
**Exponenciální** - modelování času -> životnost lampy než se porouchá
**Normální (Gaussovo, standartní)** - výška člověka
**studentovo t-rozdělení** - odhad mean std. rozdělení s málo vzorky a neznáme směrodatnou odchylku $\sigma$
**beta** - Využívá se na modelování chování omezených na intervaly konečné délky
<!--ID: 1613561383784-->


definuj marginalizaci #flashcard 
Výpočet $P(A)$ ze sdružené pravděpodobnosti $P(A, B)$
<!--ID: 1613561383789-->


Bayesova věta #flashcard 
$$\pi(\theta \mid x)=\frac{f(x \mid \theta) \pi(\theta)}{f(x)}, \quad f(x) > 0$$
$\pi(\theta \mid x)$ - aposteriori podmíněná hustota
$\pi(\theta)$ - apriori hustota
$f(x \mid \theta)$ - model (likelyhood) dat
$$P(A \mid B)=\frac{P(B \mid A) P(A)}{P(B)}$$
<!--ID: 1613561383795-->


popiš postup, jak s apriori znalostí získám aposteriori pravděpodobnost. #flashcard 
mám apriori znalost, z ní si určím model. Pomocí modelu a naměřených dat si vypočítám aposteriori pravděpodobnost pomocí Bayesovy věty. -> potom můžu vzít aposteriori pravděpodobnost a pro nová data je použít jako apriori.
<!--ID: 1613561383800-->

Definuj diskrétní i spojitou střední hodnotu #flashcard 
$$\mathrm{E} X=\sum_{k} x_{k} \mathrm{P}\left(X=x_{k}\right)$$
$$\mathrm{E} X=\int_{-\infty}^{\infty} x f(x) d x$$
Průměr vážený pravděpodobností.
<!--ID: 1613732439550-->


Definuj rozptyl #flashcard 
$$\operatorname{var} X=\mathrm{E}\left[(X-\mathrm{E} X)^{2}\right]$$
<!--ID: 1613732439565-->


Definuj medián #flashcard 
$q_{0.5}$ - druhý kvantil == medián
<!--ID: 1613732439577-->


Definuj modus #flashcard
$argmax(f_x)$ kde $f_x$ je hustota
<!--ID: 1613732439586-->

## Lec 02 - 24.02.2021 - Lineární modely, sekvenční odhad, predikce

Definuj pravděpodobnostní prostor. #flashcard 
je to trojice $(\Omega, \mathcal{F}, \mathrm{P})$
$\Omega$ - množina možných výsledků experimentů
$\mathcal{F}$ - tvoří náhodné jevy = podmnožiny $\Omega$
$\mathrm{P}$ - pravděpodobnosti co přiřazujeme náhodným jevům
<!--ID: 1614212494300-->


Definuj náhodný proces. #flashcard 
$(\Omega, \mathcal{F}, \mathrm{P})$ pravděpodobnostní prostor a $T \subseteq \mathbb{R}$ indexová množina.
Systém náhodných veličin $X=\left\{X_{t} \mid t \in T\right\}, \quad X_{t}: \Omega \rightarrow \mathbb{R}$  nazýváme náhodný proces
<!--ID: 1614212494305-->


Popiš přstupy Bayesovského modelování náhodných procesů. #flashcard 
**Rostoucí datové okno** - když přijdou nová data, přepočítat celý model od začátku
**Plovoucí datové okno** - zajímá nás jen posledních $n$ dat. Periodicky přepočítávám, ale jen na omezeném množství dat.
**Plně sekvenční odhad** - ke stávající informaci přidáváme pouze nová data.
<!--ID: 1614212494310-->


Definuj podmíněnou pravděpodobnost pomocí sdružené pravděpodobnosti. #flashcard 
podmíněná = sdružená / pst. podmínky
$$P(A \mid B) = \frac{P(A, B)}{P(B)}$$
<!--ID: 1614212494313-->



$f\left(y_{t} \mid x_{t}, \theta\right)$ je hustota pravdepodobnosti (model), $\pi\left(\theta \mid x_{0: t-1}, y_{0: t-1}\right)$ je apriori hustota pro $\theta$. Dej mi aposteriori hustotu pro jednokrokový update $\pi\left(\theta \mid y_{0: t}, x_{0, t}\right)$ #flashcard 
$$\begin{aligned}
\pi\left(\theta \mid y_{0: t}, x_{0, t}\right) &=\frac{f\left(y_{t} \mid x_{t}, \theta\right) \pi\left(\theta \mid x_{0: t-1}, y_{0: t-1}\right)}{\int f\left(y_{t} \mid x_{t}, \theta\right) \pi\left(\theta \mid x_{0: t-1}, y_{0: t-1}\right) d \theta} \\
&=\frac{f\left(y_{t} \mid x_{t}, \theta\right) \pi\left(\theta \mid x_{0: t-1}, y_{0: t-1}\right)}{f\left(y_{t} \mid x_{t}\right)}
\end{aligned}$$
ten součin musíme normalizovat = vydělit plochou samo sebe (to je ten integrál). Vlastně nás zajímá jen čitatel, jelikož na $\theta$ nemá normalizace vliv. Proto zapisujeme pomocí proporcionality. (kvůli zjednodušení zápisu) 
<!--ID: 1614212494317-->



$f\left(y_{t} \mid x_{t}, \theta\right)$ je hustota pravdepodobnosti (model), $\pi\left(\theta \mid x_0, y_0\right)$ je apriori hustota, odvoď vícekrokový update pro  $\pi\left(\theta \mid x_{0: t}, y_{0: t}\right)$ #flashcard 
![[odvozeni_updatu.png]]
a to se da zapsat jako:
$$\pi\left(\theta \mid y_{0: t}, x_{0: t}\right) \propto \pi\left(\theta \mid y_{0}, x_{0}\right) \prod_{\tau=1}^{t} f\left(y_{\tau} \mid x_{\tau}, \theta\right)$$
<!--ID: 1614212494321-->


Pomocí jakých hodnot můžeme reprezentovat bodový odhad $\theta$ díky aposteriori hustotě? #flashcard 
- Střední hodnotu $\mathbb{E}[\theta]$ - (složitý výpočet)
- modus - MAP = maximum aposteriori odhad
- medián - prostřední hodnota
<!--ID: 1614212494325-->


Definuj sufficientní statisktiku $T(x, y)$. #flashcard 
Mám náhodnou veličinu $X$, když chci odhadnout parametr $\theta$, tak nepotřebuju celou $X$. Stačí mi jen její podmnožina a to taková, která obsahuje všechnu informaci o $\theta$, kterou obsahuje $X$. 
Analogie z LN je to, že $X$ je podprostor a $T(x, y)$ je podmnožina $X$, co $X$ generuje.
<!--ID: 1614762006908-->


Exponenciální třída distribucí a příklady rozdělení co do ní patří #flashcard 
Z bayes update se to nezdá, ale zásadním problémem bayesovského modelování je odvození aposteriorní distribuce. Pokud po prvním updatu není aposteriorno některou z "běžných" distribucí, pak s dalším updatem je aposteriorno ještě komplikovanější. V exponenciální třídě distribucí půjdou výpočty ale pohodlně.
$f(y \mid x, \theta)=h(y, x) g(\theta) \exp \left[\eta^{\top} T(y, x)\right]$
kde $\eta \equiv \eta(\theta)$ je přirozený parametr, $T(y,x)$ je suficientní statistika fixního rozměru, $h(y,x)$ je známá funkce a $g(\theta)$ je normalizační funkce.
Příklady: Binomial, Bernoulli, Multinomial, Categorical, Normální, Laplace, Gamma, Exponenciální, Poisson
<!--ID: 1614212494329-->


Definuj konjugovanou apriori distribuci a řekni k čemu je. #flashcard 
$y|x, \theta$ má rozdělení z exponenciální třídy distribucí. Říkáme, že apriorní distribuce $\theta$ s hyperparametry $\xi$ $\nu$ je k němu konjugovaná, pokud její hustota pravděpodobnosti má tvar 
$$\pi(\theta) = q(\xi, \nu) g(\theta)^{\nu} \exp \left[ \eta^{\intercal} \xi \right]$$
kde $\xi$ má stejný rozměr jako sufficientní statistika $T(y,x), \nu\in\mathbb{R}^{+}$ a $q(\xi,\nu)$ je známá funkce. Funkce $g(\theta)$ je stejná jako normalizační funkce v hustotě pro $y|x, \theta$ (v exponenciální třídě distribucí) a $\eta$ je přirozený parametr $\theta$.
Pokud je aposteriori distribuce $p(\theta \mid x)$ ve stejné rodině distribucí jako apriori $p(\theta)$, pak jsou kojugované a je to k tomu, že chci, aby pro sekvenční odhad parametrů vypadla po updatu stejná distribuce jako byla předtím a mohl jsem snadno cyklit. Potom je jednokrokový bayes update jen přičítání k parametrům. $\xi_{t} = \xi_{t-1} + T(y_{t},x_{t}), \nu_{t} = \nu_{t-1} + 1$
<!--ID: 1614763462306-->


Jak vypadá bayesovský update s konjugovaným apriornem? #flashcard 
Použijeme-li konjugovaná apriorna s hyperparametry $\xi_{t-1}$ a $\nu_{t-1}$, je Bayesův update
<!--ID: 1692184510640-->


$$
\pi(\theta|y_{0:t}, x_{0,t}) 
\propto
f(y_t|x_t, \theta)\, \pi(\theta|x_{0:t-1}, y_{0:t-1})
$$
vlastně jen triviální součet
$$
\begin{aligned}
    \xi_{t} &= \xi_{t-1} + T(y_{t},x_{t}), \\
    \nu_{t} &= \nu_{t-1} + 1.
\end{aligned}
$$
**Závěr: Bayesova věta se při použití konjugovaného apriorna ztriviální na přičtení suficientní statistiky k hyperparametru $\xi_{t-1}$ a inkrementaci hyperparametru $\nu_{t-1}$.**


Definuj Beta distribuci a řekni k čemu je dobrá #flashcard 
$$\frac{1}{\mathrm{~B}(\alpha, \beta)} x^{\alpha-1}(1-x)^{\beta-1}$$ where $\mathrm{B}(\alpha, \beta)=\frac{\Gamma(\alpha) \Gamma(\beta)}{\Gamma(\alpha+\beta)}$, and $\Gamma$ is the Gamma function. Využívá se na modelování chování omezených na intervaly konečné délky.
<!--ID: 1614212494333-->


## Lec 03 - 03.03.2021 - Zobecněné lineární modely

Definuj zobecněný lineární model #flashcard 
Jsou to modely ve tvaru: $\widehat{y}_t = \mathbb{E}[y_t|x_t, \beta] = g^{-1}(\beta^\intercal x_t)$
kde $\mathbb{E}[y_t|x_t, \beta]$ je expected value $y_t$, $\beta^\intercal x_t$ je lineární prediktor a $g$ je linková (spojovací) funkce.
Patří tam logistická regrese, kde g je sigmoida, patří tam i lin. regrese, kde g je identita.
<!--ID: 1614762006917-->


Popiš $y_t$ pro logistický regresní model, řekni z jakého je rozdělení a odvoď rovnici pro $\widehat{y}_t$ #flashcard 
$y_t \sim Bernoulli(p_t), \quad E[y_t]=p_t$
$$g(\mathbb{E}[y_t|p_t]) 
= g(\mathbb{E}[y_t|X_t, \beta])
= g(p_t)
= \textit{logit}(p_t)
= \log \frac{p_t}{1-p_t}
= \beta^\intercal x_t$$
$$\widehat{y}_t = \mathbb{E}[y_t|x_t, \beta] = p_t = g^{-1}(\beta^\intercal x_t)  = \textit{logit}^{-1}(\beta^\intercal x_t) = \sigma(\beta^\intercal x_t)$$
<!--ID: 1614762006925-->


Jak diagnostikuješ kvalitu predikce modelu? (např. log. regrese) #flashcard 
Brierovo skóre == MSE, Confusion matrix, TPR, FPR atd atd atd
<!--ID: 1614762006933-->

Definuj kovarianci #flashcard 
**Kovariance** je statistickou mírou lineární závislosti dvou veličin.
$$\operatorname{cov}(X, Y) = \mathrm{E}\left[\left(X-\mu_{X}\right)\left(Y-\mu_{Y}\right)\right]$$
<!--ID: 1614769217455-->


Definuj korelaci #flashcard 
Je to znormovaná covariance. Korelace je metrika mezi -1 a 1 co vysvětluje, jak změna jedné veličiny změní druhou veličinu.
$$\rho_{X, Y}=\operatorname{corr}(X, Y)=\frac{\operatorname{cov}(X, Y)}{\sigma_{X} \sigma_{Y}}=\frac{\mathrm{E}\left[\left(X-\mu_{X}\right)\left(Y-\mu_{Y}\right)\right]}{\sigma_{X} \sigma_{Y}}$$
<!--ID: 1614769217461-->

## Lec 04 - 10.03.2021 - Kalmanův filtr

Co dělá Kalmanův filter a k čemu se dá použít? #flashcard 
Kalmanův filter se nám hodí v případě, kdy máme hidden markov proces. Chceme aproximovat veličinu, kterou nemůžeme měřit. Máme ale k dispozici jiné veličiny, které nám napovídají. Jsou ale zatížené šumem. Kalman nám pomáhá najít vhodný balanc mezi vstupními proměnnými a vyhlazuje šum. Reaguje dynamicky na změny v nátuře měření. Jako třeba gravitace planety na letící raketu.
<!--ID: 1615846422683-->


Definuj stavový model systému v Bayesovské statistice #flashcard 
Trojice (stav, vstup, výstup)
**stav** - označený typicky $x_t$ - stav nemůžeme pozorovat, ale můžeme ho předpovídat
**vstup** - řídící veličina $u_t$ - tu známe
**vystup** - $y_t$ pozorovatelná veličina podmíněná $x_t, u_t$
Stavový model může být buď diskrétní,enbo spojitý.
state equation: $x_t = f_t(x_{t-1}, u_t)$
measurement equation: $y_t = g_t(x_t)$
<!--ID: 1615846422690-->


Definuj Markovský proces $n$-tého řádu #flashcard 
též Markkov model je model, kde aktuální stav závisí pouze na předchozích $n$ stavech.
$p(x_t \mid x_{t-1}, x_{t-2}, ..., x_{t-n})$ - pravděpodobnost přechodu.
$p(x_0)$ - počáteční stav
<!--ID: 1615846422698-->


Popiš Markovský model (Hidden Markov Model - HMM) #flashcard 
Takový Markovský, který není přímo pozorovatelný, ale lze na něj nahlížet prostřednictvím jiné pozorovatelné veličiny.
<!--ID: 1615846422703-->


Sestav a popiš stavový model KF pro 
$h_{t}=h_{0}+v_{0} \Delta_{t}-\frac{1}{2} g \Delta_{t}^{2}+w_{h, t}$
$v_{t}=v_{0}-g \Delta_{t}+w_{v, t}$ 
Z něho odvoď obecný stavový model pro KF. #flashcard 
Stavový model
$\begin{aligned} X_{t} &=\left[\begin{array}{cc}1 & \Delta_{t} \\ 0 & 1\end{array}\right] X_{t-1}+\left[\begin{array}{c}-\frac{1}{2} \Delta_{t}^{2} \\ -\Delta_{t}\end{array}\right] g+\left[\begin{array}{l}w_{h, t} \\ w_{v, t}\end{array}\right] \\ y_{h, t} &=\left[\begin{array}{cc}1 & 0\end{array}\right] X_{t}+\varepsilon_{t} \end{aligned}$
Obecný stavový model pro KF.
$X_{t}=A_{t} X_{t-1}+B_{t} u_{t}+w_{t}$
$y_{t}=H_{t} X_{t}+\varepsilon_{t}$
kde $X_t$ je **stav**, $y_t$ jsou naměřené hodnoty, $u_t$ je **řídící veličina**, $w_t$ a $\varepsilon_t$ jsou **šum stavu** a **šum měření** a $A_t, B_t$ a $H_t$ jsou matice patřičných rozměrů.
<!--ID: 1615846422710-->

Vyberte správné tvrzení o stavové veličině 1) Jde o veličinu, jejíž hodnotu známe a priori 2) Jde o veličinu, jejíž hodnotu známe a posteriori, 3) Jde o veličinu, kterou nelze přímo měřit #flashcard 
Jde o veličinu, kterou nelze přímo měřit
<!--ID: 1616277676460-->


Lineární stavové modely 1) se sestávají z rovnice pro predikci budoucích měření a rovnice měření. 2) Ani jedna z ostatních odpovědí není správně 3) se sestávají z rovnice pro vývoj stavu a rovnice měření. #flashcard 
se sestávají z rovnice pro vývoj stavu a rovnice měření.
<!--ID: 1616277676466-->



Kalmanův filtr 1) reprezentuje měření jako nelineární funkce stavů.  2) filtruje měření od šumu, tj. interpoluje data. 3) odhaduje hodnoty stavů z dostupných měření. #flashcard 
odhaduje hodnoty stavů z dostupných měření.
<!--ID: 1616277676471-->


V jakém kroku Kalmanova filtru uplatníme Bayesovu větu? #flashcard 
v updatu
<!--ID: 1616277562760-->


Pro použití Kalmanova filtru potřebujeme znát (mimo jiné) 1) hodnotu měření  2) hodnotu realizace šumové veličiny na stavech. 3) hodnotu stavu x #flashcard 
hodnotu měření 
<!--ID: 1616277676476-->


Kalmanův filtr: každý predikční krok 1) sníží hodnotu kovariance odhadu stavů.  2) nezmění hodnotu kovariance odhadu stavů. 3) zvýší hodnotu kovariance odhadu stavů. #flashcard 
zvýší hodnotu kovariance odhadu stavů.
<!--ID: 1616277676480-->


Kalmanův filtr předpokládá, že je stavový model 1) lineární, 2) lineární nebo slabě nelineární, 3) slabě či silně nelineární.
#flashcard 
stavový model je lineární.

Logistický regresní model 1) má jako vhodné konjugované apriorno pro regresní koeficienty distribuci normální inverzní gama. 2) má jako vhodné konjugované apriorno pro regresní koeficienty normální distribuci. 3) nemá vhodné konjugované apriorno pro regresní koeficienty. #flashcard 
nemá vhodné konjugované apriorno pro regresní koeficienty.
<!--ID: 1616277676486-->

## Lec 05 - 17.03.2021 - Monte Carlo

Ukaz, ze kdyz uvazujes integral jako  soucet obdelniku, tak uzce souvisi s prumerem funkce #flashcard 
$$\int_{a}^{b} f(x) d x \frac{\Delta x \rightarrow 0}{N \rightarrow \infty} \sum_{i=1}^{N} f\left(x_{i}\right) \Delta x=\frac{b-a}{N} \sum_{i=1}^{N} f\left(x_{i}\right)=V \frac{\sum_{i=1}^{N} f\left(x_{i}\right)}{N}=(b-a)\langle f\rangle$$
$\langle f\rangle$ je znacka pro stredni hodnotu
<!--ID: 1617270928061-->


Co je Monte Carlo ingegrace? #flashcard 
Jelikoz plati: $\int_{a}^{b} f(x) d x = (b-a)\langle f\rangle$
1) Zjistime pomoci Monte Carlo zjistit odhad stredni hodnoty (zakon velkych cisel)
	1) pomoci rovnomerneho rozdeleni generuju body
	2) sectu jejich funkcni hodnoty a vydelim poctem
2) tenhle odhad vynasobime $(b-a)$. Muzeme si spocitat i rozptyl odhadu integralu atd.
<!--ID: 1617270928065-->


Zakladni theorem vzorkovani #flashcard 
Vzorkování $x\sim f(x)$ je ekvivalentní k vzorkování  $(x, u) \sim \mathcal{U}\{(x, u): 0 < u < f(x)\}$. Kde $f(x)$ je hustota, $\mathcal{U}$ je rovnomerne rozdeleni.
<!--ID: 1617270928069-->


Popis Naive Rejection sampling #flashcard 
![[PROJECTS/FIT/FIT-2021-2/media/rejection_sampling.png]]
1) navzorkuj x' rovnomernym rozdelenim mezi a, b
2) pro kazde x' vygeneruj $u \mid x'$ z rovnomerneho rozdeleni mezi $0$ a $m$, kde $m < max(f(x))$
3) zavrhni $u \mid x > f(x')$, accept $u \mid x < f(x')$
Histogram vysledku by mel odpovidat profilu funkce. Pak muzu pocitat stredni hodnotu, var atd.
![[rejection_sampling2.png]]
<!--ID: 1617270928073-->


Jaka je nevyhoda rejection sampling? #flashcard 
Musime vygenerovat hodne vzorku abychom dostali dobrou predstavu, Hodne vzorku je mimo. Proto misto konstantni funkce co limituje vyber $u$ volime nejakou, co lepe aproximuje $f$
<!--ID: 1617270928076-->


Co je proposal pro rejection sampling? #flashcard 
jako limit pro vyber $u$ pouzivame funkci $g$, pro kterou plati, ze $g(x) > f(x)$ pro vsechny $x$. Dela se to tak, ze vezmu funkci co aproximuje $f$ a tu nejak naskaluju. Je to dobre k tomu, ze nezavrhneme tolik vzorku a staci nam mene vzorku, mame vetsi acceptance.
<!--ID: 1617270928080-->


## Lec 06 - 24.03.2021 - Particle Filter

Popiš princip importance samplingu a kdy ho chceš použít #flashcard 
Máme nějakou bramboroidní distribuci $f$ a nemáme pro ní generátor. Máme ale jiný generátor, který generuje samply $x$ co mají hustotu $g(x)$. Pomocí těchto samplů můžeme dostávat odhady např. střední hodnoty, nebo můžeme integrovat atd. 
platí $$\int f(x) dx = \int g(x) \underbrace{\frac{f(x)}{g(x)}}_{= w(x)} dx = \int g(x) w(x) dx.$$
1) vygenerujeme samply $x$ ~ distribuce $g$
2) spočítáme váhy $w=f(x)/g(x)$ (optional: normalizujeme $W=\frac{w}{w.sum()}$)
3) průměr $\frac{w*x}{N}$ je odhadem střední hodnoty bramboroidu  $\mathbb{E}f$
<!--ID: 1617270928083-->


Popiš algoritmus importance samplingu #flashcard 
Celý algoritmus je o určování vah, které pak používáme např. při výpočtu integrálů.
1.  Nagenerujeme $N$ vzorků z proposal hustoty: $x_i \sim g(x)$
2.  Spočteme hodnotu hustoty $f(x_i)$
3.  Spočteme hodnotu hustoty $g(x_i)$
4.  Spočteme váhy $w(x_i) = \frac{f(x_i)}{g(x_i)}$
5.  Váhy normalizujeme, buď $W(x_i) = w(x_i)/\sum w(x_i)$ nebo $w'(x_i)=w(x_i)/N$
Dostaneme např. odhad střední hodnoty $\hat{\mu} = \sum W(x_i) x_i$
<!--ID: 1617270928087-->


Algoritmus Sequential Importance Sampling Filteru #flashcard 
1.  Navzorkujeme $x_0^{(i)}$ z vhodné apriorní distribuce $\pi(x_0)$ a přiřadíme jim rovnoměrné váhy $w_0^{(i)} = 1/N$
2.  Pro $t=1,2,\ldots$:
    -   Predikce: navzorkujeme nová $x_t^{(i)}$ z hustoty $f_t(x_t|x_{t-1}^{(i)})$
    -   Update: přepočítáme váhy $w_t^{(i)} = w_{t-1}^{(i)} g(y_t|x_t^{(i)})$ a normalizujeme je $w_t^{(i)} \leftarrow w_t^{(i)}/\sum_j w_t^{(j)}$
    -   Odhad střední hodnoty $\mathbb{E}[x_t|\cdot] = \sum_{i=1}^{N}w_{t}^{(i)} x_t^{(i)}$
<!--ID: 1617270928091-->



Algoritmus bootstrap particle filteru #flashcard 
Uplne stejne jako SIS filter, ale generujeme nova data proporcialne z bodu podle vahy. krok resampling. 
1.  Navzorkujeme $x_0^{(i)}$ z vhodné apriorní distribuce $\pi(x_0)$ a přiřadíme jim rovnoměrné váhy $w_0^{(i)} = 1/N$
2.  Pro $t=1,2,\ldots$:
    - **Resampling**: vybereme $\tilde{x}_{t-1}^{(i)}\sim \sum_{i=1}^N w_{t-1}^{(i)} x_{t-1}^{(i)}$ proporcionálně k jejich vahám $w_{t-1}^{(i)}$
    -   Predikce: navzorkujeme nová $x_t^{(i)}$ z hustoty $f_t(x_t|x_{t-1}^{(i)})$
    -   Update: přepočítáme váhy $w_t^{(i)} = w_{t-1}^{(i)} g(y_t|x_t^{(i)})$ a normalizujeme je $w_t^{(i)} \leftarrow w_t^{(i)}/\sum_j w_t^{(j)}$
    -   Odhad střední hodnoty $\mathbb{E}[x_t|\cdot] = \sum_{i=1}^{N}w_{t}^{(i)} x_t^{(i)}$
<!--ID: 1617270928095-->

## Lec 07 - 31.03.2021 - Zobecněný lineární model, regularizace 

K čemu slouží regularizace v lineární regresi? #flashcard 
Základní ztrátová funkce RSS minimalizuje chybu. Ovšem nebere v potaz velikosti vah. Pokud máme zašuměná, nepřesná nebo jinak podmíněná data, tak platí, že váhy by měly být pokud možno malé. 
Rozšiřujeme tedy ztrátovou funkci na $RSS + \lambda*REG$, kde $REG$ je regularizační funkce penalizující velikost vah a $\lambda$ je parametr co regularizaci přikládá váhu v celkové ztrátě.
<!--ID: 1617359034134-->



Jaké typy regularizace v lineární regresi znáš a jak se modelu říká? #flashcard 
Ridge regression: $\operatorname{RSS}_{\lambda}(\boldsymbol{w})=\|\boldsymbol{Y}-\mathbf{X} \boldsymbol{w}\|^{2}+ \lambda \sum_{i=1}^{p} w_{i}^{2}$
Lasso: $\operatorname{RSS}_{\lambda}(\boldsymbol{w}) = \|\boldsymbol{Y} -\mathbf{X} \boldsymbol{w}\|^{2}+ \lambda \|\boldsymbol{w}\|_1$
Efekt je podobný jako MSE a MAE - Ridge penalizuje velký odchylky a malý mu tolik nevadí a lasso penalizuje všechno, ale může se mu stát, že bude mít někde větší odchylku.
Pak máme hybrida
elastic regularization: $\operatorname{RSS}_{\lambda_1, \lambda_2}(\boldsymbol{w}) = \|\boldsymbol{Y} -\mathbf{X} \boldsymbol{w}\|^{2} + \lambda_1 \sum_{i=1}^{p} w_{i}^{2} + \lambda_2 \|\boldsymbol{w}\|_1$
<!--ID: 1617359034140-->
