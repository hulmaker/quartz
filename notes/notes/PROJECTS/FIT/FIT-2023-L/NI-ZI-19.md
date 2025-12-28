TARGET DECK: NI-ZI-2023::NI-PON
FILE TAGS: NI-ZI-2023 NI-ZI-19 NI-PON

prev::[[NI-ZI-18]]
next::[[NI-ZI-20]]

# Hladká optimalizace (bez vazeb)
spádové metody, volba směru a délky kroku


Popiš jak vypadá standartní optimalizační problém #flashcard 
minimalizuj $f(x)$,
za podmínek $g(x)=0, h(x) \leq 0$ atd...
kde $f: D \to \mathbb{R}, g: D \to \mathbb{R}^p, h: D \to \mathbb{R}^m$, kde $D \subset \mathbb{R}^n$
<!--ID: 1691966313983-->

Popiš klasifikace optimalizačních úloh #flashcard 
minimalizuj $f(x)$, za podmínek $g(x)=0, h(x) \leq 0$
1) **nelineární programování** (nonlinear programming - NLP): předpokládáme spojitou diferencovatelnost (někdy i dvojitou)
2) **lineární programovnání** (linear programming - LP): $f, g$ a h jsou afinní funkce
3) **kvadratické programování** (quadratic programming LP): $f$ je kvadratická (tj.$f(x) = a^T\cdot x +\frac{1}{2}x^T\cdot B\cdot x$), kde $g, h$ jsou afinní funkce)
4) **konvexní optimalizace** (convex optimization): $f$ je konvexní na $M$ - množina připustných řešení
5) **nehladká optimalizace** (non-smooth optimization): některá z funkcí není diferencovatelnáa)(smíšené) celočíselné programování a jeho varianty
<!--ID: 1691966313988-->



Kdy je funkce $f$ totálně diferencovatelná v bodě $a \in D$? #flashcard 
pokud existuje zobrazení $\lambda(x): D \to \mathbb{R}^m$ tž,
$$\lim _{h \rightarrow 0} \frac{\|f(a+h)-f(a)-\lambda(h)\|}{\|h\|}=0$$
<!--ID: 1691966313989-->



Co za vlastnost (souvisí s derivací) by měla mít funkce, kterou optimalizujeme? #flashcard 
Měla by být dvakrát spojitě diferencovatelná. Abychom mohli použít ty oblíbené iterační metody. Dál často používáme Taylorův rozvoj druhého řádu.
<!--ID: 1691966313991-->



Optimalizační metoda, kdy iterujeme přes posloupnost aproximací konvergující k nějakému minimu. Jaké základní metody pro počítání následující aproximace máme? #flashcard 
**line-search** - Následující aproximaci hledáme v nějakém daném směru $p_k$, směr se dá volit např. jako směr největšího spádu, newtonova metoda atd.
**region-trust** - Na okolí bodu $x_k$ vytvoříme nějakou aproximaci funkce $f$, označené $m_k$, a hledáme minimum této aproximace $m_k$ na okolí bodu $x_k$ 
<!--ID: 1691966313993-->



Optimalizační metoda, kdy iterujeme přes posloupnost aproximací konvergující k nějakému minimu. Je možné najít globální minimum? Zdůvodni a řekni jestli nám lokální minima vadí. #flashcard 
Je to teoreticky možné, ale téměř neupočitatelné. Z toho důvodu se spokojíme s lokálním minimem. Lokální minimum je dostačující, jelikož pro funkce s mnoho parametry je často velmi blízko tomu globálnímu. (například neuronky)
<!--ID: 1691966313995-->



Jaké jsou možné podmínky pro volbu délky kroku v line-search optimalizaci? #flashcard 
**Armijova podmínka** - next step musí být pod klesající přímkou (můžu si dovolit velký krok, jen musí být dost dobrý) $\phi\left(\alpha_k\right) \leq \phi(0)+\alpha_k c \phi^{\prime}(0)$
**Goldsteinova podmínka** - Jako Armijova podmínka, jen mám přímku i pro lower boud. - můžu tak minout minimum co bude pod hranicí, ale nedělám miniaturní kroky. $\phi(0)+\alpha_k(1-c) \phi^{\prime}(0) \leq \phi\left(\alpha_k\right) \leq \phi(0)+\alpha_k c \phi^{\prime}(0)$
**Wolfeho slabá podmínka** - přímka shora a derivace v next step je větší, než v bodě kde teď jsem (svah není moc strmý), 
**Wolfeho silná podmínka** - přímka shora, sklon je v absolutní hodnotě = krom spádu kouká i na růst
<!--ID: 1691966313997-->



Popiš metodu line-search pro optimalizační úlohu #flashcard 
Následující aproximaci hledáme v nějakém daném směru $p_k$.
$x_{k+1} = x_k + \alpha_kp_k$, kde $p_k$ je směr a $\alpha$ je délka kroku.
<!--ID: 1691966313998-->



Jak se dá volit směr v optimalizační úloze při metodě line-search? #flashcard 
line search $x_{k+1} = x_k + \alpha_kp_k$, kde $p_k$ je směr a $\alpha$ je délka kroku.
Častá volba směru: směr spádu: $p_k = -B_k^{-1}\nabla f(x_k)$
$Bk = I$ - metoda největšího spádu
$B_k = \nabla^2 f(x_k)$ - Newtonova metoda
$B_k \approx \nabla^2 f(x_k)$ - kvazi-Newtonova metoda
<!--ID: 1691966313999-->



Co je metoda největšího spádu při optimalizaci? #flashcard 
typ line-search metody, kdy směr následujícího kroku volíme jako směr, ve kterém funkce nejvíce klesá. To odpovídá směru -gradient v bodě kde právě jsem
<!--ID: 1691966314001-->



Jaká je motivace za exact line search a inexact line search pro optimalizaci? Proč se co používá? #flashcard 
Najít minimum na line může být dost složitý (exact), proto se hledá nějaká délka kroku, co zajistí dostatečný pokles funkční hodnoty (inexact)
<!--ID: 1691966314002-->



Armijova podmínka (optimalizace) #flashcard 
Používá se v kontextu hledání vhodné délky kroku připotimalizaci
definujme pomocnou funkci $\phi(\alpha)$, co mi vrátí hodnotu $f$ pro další krok z bodu $x_k$  ve směru $p_k$, s délkou kroku $\alpha$
$\phi(\alpha) = f(x_k + \alpha p_k), \alpha \geq 0$
Armijova podmínka potom vypadá takto:
$\phi(\alpha_k) \leq \phi(0) + \alpha_kc\phi'(0)$
kde $0 < c < 1$
Tedy funkční hodnota má ležet pod zvolenou přímkou, nalezený krok by však neměl být příliš malý.
<!--ID: 1691966314004-->



Goldsteinova podmínka (optimalizace) #flashcard 
Používá se v kontextu hledání vhodné délky kroku připotimalizaci
definujme pomocnou funkci $\phi(\alpha)$, co mi vrátí hodnotu $f$ pro další krok z bodu $x_k$  ve směru $p_k$, s délkou kroku $\alpha$
$\phi(\alpha) = f(x_k + \alpha p_k), \alpha \geq 0$
Goldsteinova podmínka potom vypadá takto:
$\phi(0) + \alpha_k (1-c)\phi'(0) \leq \phi(\alpha_k) \leq \phi(0) + \alpha_kc\phi'(0)$
kde $0 < c < \frac{1}{2}$
Tedy funkční hodnota má ležet mezi zvolenými přímkami: omezuje se nevhodná možnost, že nalezenýkrok bude příliš malý
Nevýhoda: můžeme minout optimálního hodnotu pro $\alpha_k$
<!--ID: 1691966314005-->



Wolfeho slabá podmínka (optimalizace) #flashcard 
Používá se v kontextu hledání vhodné délky kroku při optimalizaci
definujme pomocnou funkci $\phi(\alpha)$, co mi vrátí hodnotu $f$ pro další krok z bodu $x_k$  ve směru $p_k$, s délkou kroku $\alpha$
$\phi(\alpha) = f(x_k + \alpha p_k), \alpha \geq 0$
Wolfeho slabá podmínka potom vypadá takto:
$\phi(\alpha_k) \leq \phi(0) + \alpha_kc_1\phi'(0)$
$\phi'(\alpha_k) \geq c_2\phi'(0)$
kde $0 < c_1 < c_2 < 1$
Tedy funkční hodnota má ležet pod zvolenou přímkou a derivace je v dalším kroku větší.
<!--ID: 1691966314006-->



Wolfeho silná podmínka (optimalizace) #flashcard 
Používá se v kontextu hledání vhodné délky kroku připotimalizaci
definujme pomocnou funkci $\phi(\alpha)$, co mi vrátí hodnotu $f$ pro další krok z bodu $x_k$  ve směru $p_k$, s délkou kroku $\alpha$
$\phi(\alpha) = f(x_k + \alpha p_k), \alpha \geq 0$
Wolfeho silná podmínka potom vypadá takto:
$\phi(\alpha_k) \leq \phi(0) + \alpha_kc_1\phi'(0)$
$|\phi'(\alpha_k)| \leq c_2|\phi'(0)|$
kde $0 < c_1 < c_2 < 1$
Tedy funkční hodnota má ležet pod zvolenou přímkou a přidáním absolutní hodnoty zajistíme, aby derivace neměla příliš velké hodnoty. (svah i růst není tak strmý)
<!--ID: 1691966314008-->



Jaká je obecná myšlenka Newton method? - optimalizace #flashcard 
Předpokládá komplikovanou ztrátovou funkci. Aproximuje jí Taylorem 2. řádu a hledá minimum. Jelikož to je polynom, tak tu rovnici zvládneme vyřešit relativně snadno.
parciální derivace, gradient = 0, normální rovnice atd.
<!--ID: 1691966314009-->



Taylorův polynom 2. stupně pro funkci $f(x_k + p)$ #flashcard 
$f\left(x_{k}+p\right) \approx f\left(x_{k}\right)+\nabla f\left(x_{k}\right)^{T} p+\frac{1}{2} p^{T} \nabla^{2} f\left(x_{k}\right) p=m_{k}\left(x_{k}+p\right)$
<!--ID: 1691966314010-->



Odvoď směr $p_k$ v Newtonově metodě (optimalizace) #flashcard 
Taylorův polynom 2. stupně funkce $f\left(x_{k}+p\right)$
$m_{k}\left(x_{k}+p\right) = f\left(x_{k}\right)+\nabla f\left(x_{k}\right)^{T} p+\frac{1}{2} p^{T} \nabla^{2} f\left(x_{k}\right) p$
hledáme $p_{k}=\underset{p}{\operatorname{argmin}} m_{k}\left(x_{k}+p\right)$
parciální derivace, gradient
$\nabla m_{k}\left(x_{k}+p\right)=0 \quad \Longleftrightarrow \quad \nabla f\left(x_{k}\right)+\nabla^{2} f\left(x_{k}\right) p=0$
směr dostaneme takto
$p_k = -(\nabla^2(fx_k))^{-1}\nabla f(x_k)$
Předpokládáme, že $\nabla^2(fx_k)$ je regulární
<!--ID: 1691966314012-->



Co se stane, když v Newtonově metodě není $\nabla^2(fx_k)$ pozitivně definitní? (optimalizace) #flashcard 
není zaručeno, že je $p_k$ spádový směr.
<!--ID: 1691966314013-->



Co se dá udělat, když v Newtonově metodě není $\nabla^2(fx_k)$ pozitivně definitní? (optimalizace) #flashcard 
Její inverze tedy nemusí existovat, potom je několik možných řešení.
A to nastavit $B_k = \nabla^2(fx_k) + E_k$ tak, aby byla pozitivn2 definitní
* změnou záporných vlastních čísel (bez porušení symetrie přičteš něco, co odstraní záporná vlastní čísla)
* přičtení kladné diag. matice (regularizace - posune všechna vlastní čísla (ridge regresion))
* modifikace nějakého rozkladu $\nabla^2(fx_k)$
* Kvazinewtonovské metody to částečně řeší
<!--ID: 1691966314014-->



Hlavní myšlenka Kvazinewtonových metod? (optimalizace) #flashcard 
Kvazinewtonovské metody nějakým způsobem aproximují matici $\nabla^2(fx_k)$ a snaží se tak vylepšit celkově algoritmus, například tím, že matice $B_{k+1}$ se napočítává aktualizací matice $B_k$.
Je to další aproximace, ale velmi výrazně snižuje koplexitu algoritmu. Dá se ukázat, že má podobné vlastnosti jako Newtonova metoda a že konverguje.
<!--ID: 1691966314015-->


Do jake kategorie line search algoritmů patří BFGS metoda. Co optimalizuje a v jakém případě ji chceme použít? (optimalizace) #flashcard 
Je to jedna z Kvazinewtonovských metod pro spojitou optimalizaci funkce. Součástí toho je aproximace $B_k = \nabla^2 f\left(x_k\right)$. BFGS se snaží vylepšit newtonovskou metodu optimalizace tím, že matici $B_{k+1}$ napočítá aktualizací matice $B_k$.
Upřesnění: Víc se nám hodí inverze $B_k$, proto odhadujeme rovnou tu inverzi.
<!--ID: 1691966314016-->



Jak se aproximuje chovani funkce $f$ v bode $x_k + p$ v BFGS metode? (optimalizace) #flashcard 
$m_{k}\left(p\right)=f\left(x_{k}\right)+\nabla f\left(x_{k}\right)^{T} p+\frac{1}{2} p^{T} B_{k} p$
<!--ID: 1691966314017-->



Jaké jsou podmínky pro aproximaci matice $B_{k+1}$ na základě znalosti $B_k$ v BFGS metodě? (optimalizace) #flashcard 
$m_{k+1}$ musí mít stejný gradient jako $f$ v bodech $x_k$ a $x_{k+1}$
<!--ID: 1691966314018-->



Odvoď rovnici pro aproximaci matice $B_{k+1}$ ze znalosti $B_k$ v metodě BFGS.  Co musí $B_{k+1}$ splňovat? (optimalizace) #flashcard 
$m_{k}(p)=f\left(x_{k}\right)+\nabla f\left(x_{k}\right)^{T} p+\frac{1}{2} p^{T} B_{k} p$
jelikož $m_{k+1}$ musí mít stejný gradient jako $f$ v bodech $x_k$ a $x_{k+1}$, tak můžeme položit 
$\nabla m_{k+1}\left(-\alpha_{k} p_{k}\right)=\nabla f\left(x_{k+1}\right)-\alpha_{k} B_{k+1} p_{k}=\nabla f\left(x_{k}\right)$
a tedy
$B_{k+1}\alpha_{k} p_{k} = \nabla f\left(x_{k+1}\right) - \nabla f\left(x_{k}\right)$ a to zjednodušíme na
$B_{k+1}s_k = y_k$
aby rovnice měla řešení, musí pro pozitivně definitní $B_{k+1}$  platit $s_k^T * y_k > 0$, což zaručí wolfeho podmínky pro volbu kroku.
<!--ID: 1691966314020-->



V BFGS musíme invertovat matici $B_{k+1}$. To je jednak numericky nestabilní a druhak náročné. Jak získáme inverzi rovnou? (optimalizace) #flashcard 
toto byla rovnice $B_{k+1}s_k = y_k$
jako inverzi si označím neznámou matici $H_{k+1}$
$H_{k+1}y_k = s_k$
pak tam jsou nejake kroky a dostáváme.
$H_{k+1}=\left(I-\frac{s_{k} \cdot y_{k}^{T}}{y_{k}^{T} \cdot s_{k}}\right) H_{k}\left(I-\frac{y_{k} \cdot s_{k}^{T}}{y_{k}^{T} \cdot s_{k}}\right)+\frac{s_{k} \cdot s_{k}^{T}}{y_{k}^{T} \cdot s_{k}}$
<!--ID: 1691966314021-->



Jak volíme matici $H_0$ v BFGS  metodě? (optimalizace) #flashcard 
Lze volit jednotkovou matici.
<!--ID: 1691966314022-->



Je pravda, že least-squares problem je speciální případ obecné konvexní optimalizace? (optimalizace) #flashcard 
Ano, je to pravda
<!--ID: 1691966314023-->



Je pravda, že konvexní optimalizace je speciální případ lineárního programování? (optimalizace) #flashcard 
Ne, není to pravda. 
Lineární programování je speciální případ obecné konvexní optimalizace.
<!--ID: 1691966314024-->



Je pravda, že se dá každý problém převást na obecný konvexní problém? (optimalizace) #flashcard 
Ne, není to pravda. 
Je složité poznat, že se dá problém převést na konvexní a je často složité ho poté převést. Když to zvládneme, je už relativně rozumně řešitelný.
Ne vše jde převést na obecný konvexní problém, takové problémy se řeší pomocí nonlinear optimization, na kterou neexistují žádné skutečně efektivní řešení. (global optimization může být i exponenciální)
počteníčko: https://web.stanford.edu/~boyd/cvxbook/bv_cvxbook.pdf
<!--ID: 1691966314025-->



Definuj konvexní množinu $\Omega \in \mathbb{R}^n$ a konvexní funkci $f: \Omega 
\to \mathbb{R}$ (optimalizace) #flashcard 
Množina je konvexní, pokud $\alpha x + (1-\alpha)y \in \Omega$
pro $\forall x, y \in \Omega$ a $\forall \alpha \in [0, 1]$ (pro každé dva body lezí všechny body na úsečce mezi nimi v množině. (kružnice, elipsa atd))
funkce je konvexni, pokud $\Omega$ jek onvexni a pokud $f(\alpha x + (1-\alpha )y) \leq \alpha f(x) + (1-\alpha)f(y)$
funkce je ryze konvexni, pokud je tam ostra nerovnost.
<!--ID: 1691966314026-->



Dej mi nějaké vlastnosti konvexních množin  (optimalizace) #flashcard 
* $c \in \mathbb{R}, \{x \in \Omega | f(x) \leq c \}$ je konvexní (sublevel set), kde konvexní $f:\Omega \to \mathbb{R}$
* Průnik (ne)konečně mnoha konv. množin je konvexní
* Afinní zobrazení konvexní množiny je konvexní
* Afinní transformace proměnných zachovává konvexitu funkce
* Je-li f konvexní a g konvexní a monotónní funkce, pak je g složeno s f konvexní
<!--ID: 1691966314027-->



(optimalizace) Doplň nerovnost místo $(tady)$: $f:\Omega \to \mathbb{R}$ je spojitě diferencovatelná a $\Omega$ je konvexní. Pak platí, že $f$ je konvexní právě tehdy, když: $\forall x, y \in \Omega$,  $f(y)\ (tady) f(x) + \nabla f(x)^T \cdot (y-x)$  #flashcard 
$f(y) \geq + \nabla f(x)^T \cdot (y-x)$
<!--ID: 1691966314028-->



(optimalizace) Doplň nerovnost místo $(tady)$: $f:\Omega \to \mathbb{R}$ je spojitě diferencovatelná a $\Omega$ je konvexní. Pak platí, že $f$ je konvexní právě tehdy, když: $\forall x, y \in \Omega, x=y$,  $f(y)\ (tady) f(x) + \nabla f(x)^T \cdot (y-x)$ #flashcard 
$f(y) = f(x) + \nabla f(x)^T \cdot (y-x) \iff f(y) = f(x) + \theta$
<!--ID: 1691966314029-->



Dokaž: $f:\Omega \to \mathbb{R}$ je spojitě diferencovatelná a $\Omega$ je konvexní. Pak platí, že $f$ je konvexní právě tehdy, když: $\forall x, y \in \Omega, f(y) \geq f(x) + \nabla f(x)^T \cdot (y-x)$ #flashcard 
![[konvexni_schema_veta.png]]
![[konvexn_dukaz.png]]
pokud navíc platí $x \neq y$, tak $f(y) > f(x) + \nabla f(x)^T \cdot (y-x)$ ($f$ je ryze konvexní)
<!--ID: 1691966314030-->



(optimalizace) Co můžeme říci o bodu $x$, když máme konvexní, spojitě diferencovatelné funkci $f$ když víme, že $\forall y \in \Omega, \nabla f\left(x\right)^{T}\left(y-x\right) \geq 0$ #flashcard 
Můžeme říci, že bod $x$ je bodem globálního minima právě tehdy, když platí výraz výše.
<!--ID: 1691966314031-->



(optimalizace) Víme, že $x$ je globální minimum konvexní, spojitě diferencovatelné funkce $f$. Doplň nerovnost za (tady) $\forall y \in \Omega, \nabla f\left(x\right)^{T}\left(y-x\right)\ (tady) 0$ #flashcard 
$\forall y \in \Omega, \nabla f\left(x\right)^{T}\left(y-x\right) \geq 0$
<!--ID: 1691966314032-->



(optimalizace) Co můžeme říci o vlastních číslech matice pokud víme, že je matice pozitivně (semi)definitní? #flashcard 
Vlastní čísla pozitivně semi-definitní jsou nezáporná. -> nejmenší vl. číslo musí být nezáporné
Vlastní čísla pozitivně definitní jsou kladná. -> nejmenší vl. číslo musí být kladné
<!--ID: 1691966314033-->



(optimalizace) $f:\Omega \to \mathbb{R}$ Platí, že Taylorova aproximace druhého řádu funkce $f$ je konvexní. Je konvexní i funkce $f$. Odůvodni pokud ano-ne #flashcard 
Ano, je to dokonce ekvivalence. Jelikož $f$ je tím pádem dvakrát spojitě diferencovatelná a $\forall x \in \Omega, \nabla^2f(x) \succeq 0$
<!--ID: 1691966314034-->



(optimalizace) $f:\Omega \to \mathbb{R}$ je spojitě diferencovatelná a $\Omega$ je uzavřená konvexní množina. Pak platí, že je $f$ konvexní právě tehdy, když $\forall x \in \Omega, \nabla^2f(x) \succeq 0$. Ano/Ne a proč? #flashcard 
Ne, jelikož nevíme, jestli je $f$ dvakrát spojitě diferencovatelná a navíc $\Omega$ musí být otevřená množina.
<!--ID: 1691966314035-->


## Lec 09 - 20.04.2021 - Optimalizace 3

(optimalizace) Máme konvexní funkci co minimalizujeme $f$ metodou nejmenšího spádu. funkce má $L$-Lipschitzovsky spojity gradient. Minimum $x^*$ a krok $\alpha_k = \alpha \leq 1/L$. Omez shora $f(x_k)-f(x^*)$ #flashcard 
$f(x_k)-f(x^*) \leq \frac{||x_0-x^*||^2_2}{2\alpha k}$
$\alpha$ je konstanta, důležité je $k$
Tato věta nám ukazuje konvergenci.
<!--ID: 1691966314036-->



(optimalizace) dej mi gradient pro konvexní kvadratickou funkci $f(x) = a^T \cdot x + \frac{1}{2}x^T \cdot B \cdot x$, kde $x$ je nějaký vektor a $B$ je matice #flashcard 
$\nabla(a^T \cdot x) = a$
$\nabla(\frac{1}{2}x^T \cdot B \cdot x) = \nabla(\frac{1}{2} \sum_{i, j} B^{ij}x_ix_j) = B_{kk}x_k + \frac{1}{2} \sum_{j \neq k} B_{kj}x_j = Bx$
$\nabla f(x) = a + Bx$
<!--ID: 1691966314037-->



(optimalizace) Definuj druhotnou Lagrangeovu funkci v kontextu se standartním optimalizačním problémem. #flashcard 
minimalizuj $f(x)$,
za podmínek $g(x)=0, h(x) \leq 0$
kde $f: D \to \mathbb{R}, g: D \to \mathbb{R}^p, h: D \to \mathbb{R}^m$, kde $D \subset \mathbb{R}^n$
přípustná řešení $M = \{x \in D: g(x) = 0 \land h(x) \leq 0\}$
Příslušná Lagrangeova funkce:
$L(x, \lambda, \mu) = f(x) + \lambda^T \cdot g(x) + \mu^T \cdot h(x)$
kde $\lambda$ a $\mu$ jsou vektory Lagrangeových multiplikátorů (**druhotných proměnných**)
Lagrangeova druhotná funkce: $q(\lambda, \mu)=\inf _{x \in D} L(x, \lambda, \mu)$
<!--ID: 1691966314038-->



(optimalizace) Dokaž, že pro Lagrangeovu druhotnou funkci platí $q(\lambda, \mu) \leq p* = min f(x)_{x \in M}$ za předpokladu $\mu \geq 0$ #flashcard 
$L(x, \lambda, \mu)=f(x)+\lambda^{T} \underbrace{g(x)}_{=0}+\underbrace{\mu^{T}}_{\geq 0} \underbrace{h(x)}_{\leq 0} \leq f(x)$
pro bod minima $x* \in M$ dostaneme $q(\lambda, \mu) \leq f(x^*) = p*$
<!--ID: 1691966314039-->



(optimalizace) Máme Lagrangeovu druhotnou funkci $q(\lambda, \mu)=\inf _{x \in D} L(x, \lambda, \mu)$, kde $L(x, \lambda, \mu) = f(x) + \lambda^T \cdot g(x) + \mu^T \cdot h(x)$ a $f: D \to \mathbb{R}$. A platí že $D$ je konkávní. Můžeme říct o $q$, že je konvexní? #flashcard 
Říct to můžeme, ale nebudeme mít pravdu :D
Víme jen, že pokud je $D$ konvexní, tak je $q$ konkávní.
<!--ID: 1691966314040-->



(optimalizace) Je-li prvotní optimalizační problém konvexním problémem a platí-li Slaterova podmínka, pak VŽDY platí $\min f(x)_{x \in M} = \underset{\lambda, \mu \geq 0}{\max } q(\lambda, \mu)$ true/false? #flashcard 
Ano - trů
<!--ID: 1691966314041-->



(optimalizace) Definuj Slaterovu podmínku (pro konvexní vázanou optimalizaci) #flashcard 
Existuje alespoň jeden přípustný bod $\overline{x}$ takový, že všechny nerovnostní neafinní podmínky jsou neaktivní (tedy platí ostrá nerovnost).
Jinými slovy = Některé podmínky jsou neostré $\leq, \geq$ atd. Pokud platí jejich ostrá varianta $<, >$, pak je Slaterova podmínka splněna.
<!--ID: 1691966314042-->



(optimalizace) Uveď postačující podmínky existence lokálního ostrého minima pomocí Karushovy-Kuhnovy-Tuckerovy (KKT) podmínky. (aspoň vágně, vystihni princip) #flashcard 
Je-li $x^*$ řešení problému nelineárního programování a gradienty $\nabla f(x^∗)$, $\nabla g%j(x^∗)$ a $\nabla h%j(x^∗)$ existují a je splněna podmínka $CQ$, (constraint qualification - gradienty jsou LN (jinak je reseni nekonecne mnoho)) potom existují $λ^*$ a $μ^∗$ takové, že
1) $\nabla f\left(x^{*}\right)+\sum \lambda_{i}^{*} \nabla g_{i}\left(x^{*}\right)+\sum \mu_{j}^{*} \nabla h_{j}\left(x^{*}\right)=0$ (optimalita)
2) $\left(\mu^{*}\right)^{T} h_j\left(x^{*}\right)=0$ (zkráceně $\mu^* = 0 \lor h_j(x^*) = 0$ KKT podminka)
3) $\mu^{*} \geq 0$
U této otázky by bylo nejlepší vědět intiuitivně co co znamená, jinak si otevřít materiály a pochopit to.
<!--ID: 1691966314043-->
