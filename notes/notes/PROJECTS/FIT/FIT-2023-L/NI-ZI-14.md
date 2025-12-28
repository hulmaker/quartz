TARGET DECK: NI-ZI-2023::NI-BML
FILE TAGS: NI-ZI-2023 NI-ZI-14 NI-BML

prev::[[NI-ZI-13]]
next::[[NI-ZI-15]]
# Principy bayesovského modelování


## model, apriori a aposteriori distribuce

Popište co je to model v kontextu bayesovského modelování #flashcard 
TLDR: Pravděpodobnostní distribuce popisující nějaká data.
Pro popis dat (měření, pozorování) resp. jejich vlastností slouží _matematický model_. S prvními modely jsme se potkali už velmi záhy na základní škole, například v podobě vzorečku pro rychlost v=s/t (fyzikální model). Stejně tak můžeme modelovat například hmotnost objektu na základě jeho opakovaného měření. V případě fyzikálního modelu víme, že jeho platnost není úplně stoprocentní, zvl. při vysokých rychlostech dochází k relativistickým jevům. Stejně tak hmotnost objektu nemusíme pokaždé naměřit stejně (přesně). Proto používáme statistiku (zvl. bayesovskou nebo frekventistickou) a v ní modely v podobě pravděpodobnostních distribucí.
<!--ID: 1691320173228-->



popiš význam apriori distribuce a aposteriori distribuce + jejich užití (NI-BML) #flashcard 
**apriori** - (před) -> předpokládaná distribuce náhodné proměnné bez závislosti na naměřených datech
**aposteriori** - (potom) -> distribuce parametru náhodné proměnné v závislosti na naměřených datech.
Apriorní znalost (distribuce) přejde zahrnutím nových informací v aposteriorní. Obě kvantifikují míru neurčitosti v naší znalosti o odhadovaném parametru.
<!--ID: 1691320173234-->



Bayesova věta #flashcard 
Buďte $x$ a $\theta$ náhodné veličiny a s hustotami $f(x \mid \theta)$ a $\pi(\theta)$. Platí
$$\pi(\theta \mid x)=\frac{f(x \mid \theta) \pi(\theta)}{f(x)}, \quad f(x) > 0$$kde:
- $\pi(\theta|x)$ je **aposteriorní** podmíněná hustota veličiny $\theta$
- $\pi(\theta)$ je **apriorní** hustota
- $f(x|\theta)$ je model nebo též věrohodnost (likelihood) dat,
- $f(x)$ je marginální hustota $X$, též normovací faktor nebo anglicky `evidence`
<!--ID: 1691320173239-->

popiš postup, jak s apriori znalostí získám aposteriori pravděpodobnost. (NI-BML) #flashcard 
mám apriori znalost, z ní si určím model. Pomocí modelu a naměřených dat si vypočítám aposteriori pravděpodobnost pomocí Bayesovy věty. -> potom můžu vzít aposteriori pravděpodobnost a pro nová data je použít jako apriori.
<!--ID: 1691320173244-->



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
<!--ID: 1691320173247-->



## Exponenciální třída distribucí, konjugovaná apriorna a jejich význam v bayesovském odhadu. 


**Definice exponenciální třída distribucí** (NI-BML) #flashcard 
Uvažujme náhodnou veličinu $y$ podmíněnou veličinou $x$ a parametrem $\theta$. Exponenciální třída distribucí obsahuje distribuce s hustotou pravděpodobnosti ve tvaru
$$
f(y|x, \theta) = h(y, x) g(\theta) \exp \left[ \eta^{\intercal} T(y,x) \right],
$$
kde $\eta \equiv \eta(\theta)$ je přirozený parametr, $T(y,x)$ je suficientní statistika fixního rozměru, $h(y,x)$ je známá funkce a $g(\theta)$ je normalizační funkce. Platí-li $\eta(\theta)=\theta$ je třída kanonická.
<!--ID: 1691320173249-->


Definuj konjugovanou apriori distribuci a řekni k čemu je. #flashcard 
$y|x, \theta$ má rozdělení z exponenciální třídy distribucí. Říkáme, že apriorní distribuce $\theta$ s hyperparametry $\xi$ $\nu$ je k němu konjugovaná, pokud její hustota pravděpodobnosti má tvar 
$$\pi(\theta) = q(\xi, \nu) g(\theta)^{\nu} \exp \left[ \eta^{\intercal} \xi \right]$$
kde $\xi$ má stejný rozměr jako sufficientní statistika $T(y,x), \nu\in\mathbb{R}^{+}$ a $q(\xi,\nu)$ je známá funkce. Funkce $g(\theta)$ je stejná jako normalizační funkce v hustotě pro $y|x, \theta$ (v exponenciální třídě distribucí) a $\eta$ je přirozený parametr $\theta$.
Pokud je aposteriori distribuce $p(\theta \mid x)$ ve stejné rodině distribucí jako apriori $p(\theta)$, pak jsou kojugované a je to k tomu, že chci, aby pro sekvenční odhad parametrů vypadla po updatu stejná distribuce jako byla předtím a mohl jsem snadno cyklit. Potom je jednokrokový bayes update jen přičítání k parametrům. $\xi_{t} = \xi_{t-1} + T(y_{t},x_{t}), \nu_{t} = \nu_{t-1} + 1$
<!--ID: 1692184510634-->




Příklady konjugovaných distribucí (IN-BML) #flashcard 
| Model | Příklad použití | Konjugované apriorno |
|:---|:---:|:---|
|Normální se známým rozptylem | Všude možně :-) | Normální |
|Normální s neznámým rozptylem | Všude možně :-) | Normální inverzní-gama |
|Bernoulliho | Úspěch-neúspěch (mince, spolehlivost) | Beta |
|Binomický |  Úspěch-neúspěch (mince, spolehlivost) | Beta |
|Poissonův | Řídké jevy (telefony, částice ve fyzice, doprava) | Gama |
|Multinomický | Klasifikace do více tříd (kostka, spolehlivost) | Dirichletovo |
Více na [wikipedii](https://en.wikipedia.org/wiki/Conjugate_prior).
<!--ID: 1691320173254-->
