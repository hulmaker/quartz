TARGET DECK: Obsidian::statistics

[[NI-ZI-14]], [[NI-ZI-15]], [[NI-ZI-16]]


# Principy bayesovského modelování


## model, apriori a aposteriori distribuce

Popište co je to model v kontextu bayesovského modelování #flashcard 
TLDR: Pravděpodobnostní distribuce popisující nějaká data.
Pro popis dat (měření, pozorování) resp. jejich vlastností slouží _matematický model_. S prvními modely jsme se potkali už velmi záhy na základní škole, například v podobě vzorečku pro rychlost v=s/t (fyzikální model). Stejně tak můžeme modelovat například hmotnost objektu na základě jeho opakovaného měření. V případě fyzikálního modelu víme, že jeho platnost není úplně stoprocentní, zvl. při vysokých rychlostech dochází k relativistickým jevům. Stejně tak hmotnost objektu nemusíme pokaždé naměřit stejně (přesně). Proto používáme statistiku (zvl. bayesovskou nebo frekventistickou) a v ní modely v podobě pravděpodobnostních distribucí.
<!--ID: 1729010154017-->



Popiš význam apriori distribuce a aposteriori distribuce + jejich užití (NI-BML) #flashcard 
**apriori** - (před) -> předpokládaná distribuce náhodné proměnné bez závislosti na naměřených datech
**aposteriori** - (potom) -> distribuce parametru náhodné proměnné v závislosti na naměřených datech.
Apriorní znalost (distribuce) přejde zahrnutím nových informací v aposteriorní. Obě kvantifikují míru neurčitosti v naší znalosti o odhadovaném parametru.
<!--ID: 1729010154018-->




Bayesova věta #flashcard 
Buďte $x$ a $\theta$ náhodné veličiny a s hustotami $f(x \mid \theta)$ a $\pi(\theta)$. Platí
$$\pi(\theta \mid x)=\frac{f(x \mid \theta) \pi(\theta)}{f(x)}, \quad f(x) > 0$$kde:
- $\pi(\theta|x)$ je **aposteriorní** podmíněná hustota veličiny $\theta$
- $\pi(\theta)$ je **apriorní** hustota
- $f(x|\theta)$ je model nebo též věrohodnost (likelihood) dat,
- $f(x)$ je marginální hustota $X$, též normovací faktor nebo anglicky `evidence`
<!--ID: 1729010154019-->



popiš postup, jak s apriori znalostí získám aposteriori pravděpodobnost. (NI-BML) #flashcard 
mám apriori znalost, z ní si určím model. Pomocí modelu a naměřených dat si vypočítám aposteriori pravděpodobnost pomocí Bayesovy věty. -> potom můžu vzít aposteriori pravděpodobnost a pro nová data je použít jako apriori.
<!--ID: 1729010154020-->



Jak vypadá aposteriorní hustota pro jednokrokový update podle Bayes theorem? #flashcard 
Nechť $f(y_t|x_t, \theta)$ je hustota pravděpodobnosti $y_t|x_t,\theta$. Dále nechť $\pi(\theta|y_{0:t-1}, x_{0:t-1})$ je apriorní hustota pro $\theta$. Aposteriorní hustota pro jednokrokový update má tvar
$$
\begin{aligned}
\pi(\theta|y_{0:t}, x_{0,t}) 
&= 
\frac
{f(y_t|x_t, \theta)\, \pi(\theta|x_{0:t-1}, y_{0:t-1})}
{\int f(y_t|x_t, \theta)\, \pi(\theta|x_{0:t-1}, y_{0:t-1})d\theta} \\[3mm]
&=
\frac
{f(y_t|x_t, \theta)\, \pi(\theta|x_{0:t-1}, y_{0:t-1})}
{f(y_t|x_t)} \\[3mm]
&\propto
f(y_t|x_t, \theta)\, \pi(\theta|x_{0:t-1}, y_{0:t-1}).
\end{aligned}
$$
Posledni radek vyjadřuje bayesovský update v jednoduchém zápisu - bez normalizující hustoty ve jmenovateli.
<!--ID: 1729010154021-->



## Exponenciální třída distribucí, konjugovaná apriorna a jejich význam v bayesovském odhadu. 



Co jsou to konjugované distribuce. Uveď příklady. #flashcard 
Pokud je aposteriori distribuce $p(\theta \mid x)$ ve stejné rodině distribucí jako apriori $p(\theta)$, pak jsou kojugované. Chceme aby pro sekvenční odhad parametrů po updatu vznikla "stejný typ" distribuce. (můžem pak cyklit). Jednokrokový Bayes update je jen přičítání k parametrům.
<!--ID: 1729010154022-->


| Model                         |                  Příklad použití                  | Konjugované apriorno   |
| :---------------------------- | :-----------------------------------------------: | :--------------------- |
| Normální se známým rozptylem  |                  Všude možně :-)                  | Normální               |
| Normální s neznámým rozptylem |                  Všude možně :-)                  | Normální inverzní-gama |
| Bernoulliho                   |       Úspěch-neúspěch (mince, spolehlivost)       | Beta                   |
| Binomický                     |       Úspěch-neúspěch (mince, spolehlivost)       | Beta                   |
| Poissonův                     | Řídké jevy (telefony, částice ve fyzice, doprava) | Gama                   |
| Multinomický                  |  Klasifikace do více tříd (kostka, spolehlivost)  | Dirichletovo           |
Více na [wikipedii](https://en.wikipedia.org/wiki/Conjugate_prior).


# Stavové modely


Definice stavového modelu v kontextu Bayesovského modelování. Rovnice pro vývoj stavu a rovnice měření (NI-BML) #flashcard 
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
$w_t$ a $v_t$ jsou **šum stavu** a **šum měření** a $A_t, B_t$ a $H_t$ jsou matice patřičných rozměrů. Pokud je systém časově invariantní, jsou matice konstantní, $A_t=A, B_t=B, H_t=H$. Za druhým rovnítkem je funkcionální zápis co toho hodne schová.
<!--ID: 1729010154023-->



Jak vypadá Markovský model n-tého řádu? #flashcard 
Markovský proces (markovský model 1. řádu), je model, v němž aktuální stav závisí pouze na stavu předchozím.
$$
\begin{alignat}{2}
&p(x_t|x_{t-1}) &&\qquad\text{(pravděpodobnost přechodu)}, \\
&p(x_0) &&\qquad\text{(počáteční stav)}.
\end{alignat}
$$
Aktuální stav modelu $n$-tého řádu závisí na n předchozích stavech: $p(x_t|x_{t-1},...,x_{t-n})$. To ovšem vede k náročnějším výpočtům.
<!--ID: 1729010154024-->



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
<!--ID: 1729010154025-->




Kalmanův filtr 1) reprezentuje měření jako nelineární funkce stavů.  2) filtruje měření od šumu, tj. interpoluje data. 3) odhaduje hodnoty stavů z dostupných měření. #flashcard 
odhaduje hodnoty stavů z dostupných měření.
<!--ID: 1729010154026-->



Kalmanův filtr: každý predikční krok 1) sníží hodnotu kovariance odhadu stavů.  2) nezmění hodnotu kovariance odhadu stavů. 3) zvýší hodnotu kovariance odhadu stavů. #flashcard 
zvýší hodnotu kovariance odhadu stavů.
<!--ID: 1729010154027-->



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
<!--ID: 1729010154028-->




Jaké znáte nelineární stavové modely? Lze používat lineární stavové modely v případě nelineární funkce? #flashcard 
Nelineární stavové modely jsou opět ve tvaru
$$
\begin{aligned}
x_t &= f_t(x_{t-1}, u_t), \\
y_t &= g_t(x_t),
\end{aligned}
$$
ovšem jedna nebo obě funkce již nejsou lineární. Zde je více možností řešení:
**Slabá nelinearita**: 
* lokálně linearizovat derivacemi prvního/druhého řádu
* extended kalman filter (neoptimální, může divergobat)
**Větší nelinearita**: unscented KF
**Bruteforce**: Monte Carlo, particle filter
<!--ID: 1729010154029-->



Co je Monte Carlo ingegrace? #flashcard 
Jelikoz plati: $\int_{a}^{b} f(x) d x = (b-a)\langle f\rangle$
1) Zjistime pomoci Monte Carlo zjistit odhad stredni hodnoty (zakon velkych cisel)
	1) pomoci rovnomerneho rozdeleni generuju body
	2) sectu jejich funkcni hodnoty a vydelim poctem
2) tenhle odhad vynasobime $(b-a)$. Muzeme si spocitat i rozptyl odhadu integralu atd.
$$
\begin{gathered}
<f(x)>=\frac{1}{b-a} \int_a^b f(x) d x \\
(b-a)<f(x)>=\int_a^b f(x) d x \\
(b-a) \frac{1}{N} \sum_{i=1}^N f\left(x_i\right) \approx \int_a^b f(x) d x
\end{gathered}
$$
<!--ID: 1729010154030-->


# Rejection Sampling

Proč bychom v bayesovské teorii chtěli používat rejection sampling? #flashcard
často se setkáváme s komplikovanými aposteriori distribucemi vyjadřujícími odhad hledané veličiny (parameteru). Lze se s nimi vypořádat pomocí *konjugovaných apriorních distribucí*. 
Pokud jej ovšem nechceme nebo nemůžeme použít, potřebujeme stále nějak zjistit vlastnosti aposteriori distribuce (např. stř. hodnota). Pokud nechceme dělat analytické metodami a aproximace, můžeme využít Monte Carlo vzorkování, z aposteriorna nagenerovat hromadu vzorků a spočítat z nich jeho přibližné vlastnosti. 
Jednou z nejjednodušších metod je  **rejection sampling**, který využívá proposal distribuci, což je nějaká vhodná distribuce, z níž umíme snadno vzorkovat.
<!--ID: 1729010154031-->



Popište princip na kterém je založen rejection sampling v bayesovské teorii? Hint (fundamental theorem of simulation) #flashcard 
Označme $f(x)$ hustotu, z níž chceme vzorkovat. Algoritmus je postaven na tom, že
$$
f(x) = \int_0^{f(x)} du = \int_0^1 \underbrace{\mathbb{1}_{0<u<f(x)}}_{f(x,u)}du.
$$
**Základní teorém vzorkování (Fundamental theorem of simulation)**: 
> Vzorkování $x\sim f(x)$ je ekvivalentní k vzorkování $(x, u) \sim \mathcal{U}\{(x, u): 0 < u < f(x)\}$.
Tento teorém nejde využít přímo, ale je možné jít oklikou: Navzorkovat $(x, u)$ z větší množiny a vybrat takové dvojice, pro něž je podmínka $0 < u < f(x)$ splněna.
<!--ID: 1729010154032-->




Popis algoritmu rejection sampling v bayesovské teorii #flashcard 
Předpokládejme, že $\int_a^b f(x)dx = 1$ a zvolme $m > f(x)$ pro všechna $x\in[a,b]$. Vzorkujeme $(x', u) \sim \mathcal{U}(0<u<m)$ tak, že:
   1. Navzorkujeme $x' \sim \mathcal{U}(a, b)$,
   2. navzorkujeme $u|x=x' \sim \mathcal{U}(0, m)$,
   3. vzorek přijmeme, pokud $0<u<f(x')$.
![[Media/rejection_sampling.png]]
<!--ID: 1729010154033-->



Vlastnosti algoritmu rejection sampling v bayesovské teorii #flashcard 
* pravděpodobnost přijetí vzorku je $1/M$ - čím blíže je $M$ k vzorkované hustotě, tím vyšší četnost přijatých vzorků.
* Rejection sampling je mnohem efektivnější, než "naivní" Monte Carlo
* špatná efektivita oblastech, kde je hustota koncentrována na malou podmnožinu
* špatná efektivita v oblastech, kde hustota nabývá velmi nízkých hodnot
Abychom nemuseli generovat hodne vzorků, můžeme místo konstantní funkce co limituje výběr zvolit nějakou, co lépe aproximuje f
<!--ID: 1729010154034-->



Co je proposal pro rejection sampling? #flashcard 
jako limit pro vyber $u$ pouzivame funkci $g$, pro kterou plati, ze $g(x) > f(x)$ pro vsechny $x$. Dela se to tak, ze vezmu funkci co aproximuje $f$ a tu nejak naskaluju. Je to dobre k tomu, ze nezavrhneme tolik vzorku a staci nam mene vzorku, mame vetsi acceptance.
<!--ID: 1729010154035-->



# Importance Sampling

Jaká je hlavní výhoda importance sampling oproti rejection sampling? #flashcard 
rejection sampling je neefektivní v oblastech, kdy je plocha hustoty malá. - např. na chvostech normálního rozdělení je přijetí vzorku velmi nepravděpodobné.
**importance sampling** - tento fakt kompenzuje přidělováním **vah** _všem_ vzorkům
<!--ID: 1729010154036-->




Jak získáme váhy pro importance sampling v bayesovské teorii? #flashcard 
Označíme $f(x)$ cílovou (komplikovanou) hustotu a $g(x)$ proposal hustotu
$$
\int f(x) dx = \int g(x) \underbrace{\frac{f(x)}{g(x)}}_{= w(x)} dx = \int g(x) w(x) dx.
$$
kde, $g(x) > 0$ všude, kde je $f(x) > 0$.
**Výpočet vah: vložíme hodnotu $x$ do známých funkcí $f()$ a $g()$.**
To lze zobecnit, např. pro střední hodnotu $\mathbb{E}[x]$ při $f(x)$ platí
$$
\begin{aligned}
\mathbb{E}_f[x] &= \int x\cdot f(x) dx =  \int x\cdot \frac{f(x)}{g(x)}g(x) dx 
= \int x\cdot w(x) g(x) dx = \mathbb{E}_g[x\cdot w(x)],
\end{aligned}
$$
s podmínkou, že $g(x) > 0$ všude, kde je $x f(x) \ne 0$.
Váhy pak normalizujeme aby se sčítaly do jedné.
<!--ID: 1729010154037-->




Algoritmus importance sampling v bayesovské teorii #flashcard 
Celý algoritmus je o určování vah, které pak používáme např. při výpočtu integrálů.
   1. Nagenerujeme $N$ vzorků z proposal hustoty: $x_i \sim g(x)$.
   2. Spočteme hodnotu hustoty $f(x_i)$.
   3. Spočteme hodnotu hustoty $g(x_i)$.
   4. Spočteme váhy $w(x_i) = \frac{f(x_i)}{g(x_i)}$.
   5. Váhy normalizujeme, buď $W(x_i) = w(x_i)/\sum w(x_i)$ nebo $w'(x_i)=w(x_i)/N$.
Např. odhad střední hodnoty $\hat{\mu} = \sum W(x_i) x_i$.
<!--ID: 1729010154038-->



Co je to empirická distribuce? #flashcard 
Empirická distribuce umožňuje aproximovat skutečnou distribuci pomocí vážených či nevážených vzorků. 
Např. histogram je hrubým zobrazením empirické distribuce
Pokud máme vzorky (realizace) $\{x_i\}_{i=1}^N = \{x_1, \ldots, x_N\}$ na množině $E$, můžeme mluvit o empirické distribuci ve tvaru: $$
\eta^N(x) = \frac{1}{N} \sum_{i=1}^N \delta_{x_i}(x).
$$
<!--ID: 1729010154039-->



Algoritmus Sequential Importance Sampling Filteru #flashcard 
1.  Navzorkujeme $x_0^{(i)}$ z vhodné apriorní distribuce $\pi(x_0)$ a přiřadíme jim rovnoměrné váhy $w_0^{(i)} = 1/N$
2.  Pro $t=1,2,\ldots$:
    -   Predikce: navzorkujeme nová $x_t^{(i)}$ z hustoty $f_t(x_t|x_{t-1}^{(i)})$
    -   Update: přepočítáme váhy $w_t^{(i)} = w_{t-1}^{(i)} g(y_t|x_t^{(i)})$ a normalizujeme je $w_t^{(i)} \leftarrow w_t^{(i)}/\sum_j w_t^{(j)}$
    -   Odhad střední hodnoty $\mathbb{E}[x_t|\cdot] = \sum_{i=1}^{N}w_{t}^{(i)} x_t^{(i)}$
<!--ID: 1729010154040-->



Popište stručně sequential importance sampling, kdy a pro co je dobrý? #flashcard 
SIS je alg. sekvenčního odhadování (stavových modelů)
Když je splněna linearita - KF, slabá nelinearita - EKF, silná nelinearita - SIS
	- odhadujeme pomocí vzorků $x_t^{(i)}$ ze stavového prostoru $x_t$ s vahami $w_i$
- váhy chceme updatovat tak, aby pravděpodobnějším hodnotám stavové veličiny rostly a těm méně pravděpodobnějším naopak klesaly.
1) Predikce - udává vývoj stavů z $x_{t−1}​$ na $x_t$​ podle příslušného modelu. Samplujeme z modelu, získáváme novou empirickou distribuci
2) Update - využije Bayesovu větu - vloží do hustoty stavů nová pozorování (měření), přepočítáme váhy a normalizujeme je
<!--ID: 1729010154041-->
