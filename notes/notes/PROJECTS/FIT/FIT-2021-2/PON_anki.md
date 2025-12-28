TARGET DECK: FIT-2021-2
FILE TAGS: PON FIT-2021-2

## Lec 01 - 16.02.2021

lineární obal souboru vektorů #flashcard
množina všech lineárních kombinací ze souboru
<!--ID: 1613473085200-->


přepiš sumu na maticové značení $$\sum_{i=1}^{N}\left(Y_{i}-w^{T} x_{i}\right)^{2}$$ #flashcard 
$$\|Y-\mathbf{X} w\|^{2}$$
<!--ID: 1613473085205-->


kdy je vektor ortogonální na podprostor #flashcard 
Když je vektor kolmý na podprostor (sloupce matice co ho definuje)
<!--ID: 1613473085212-->

$$v, u \in \mathbb{R}^{p+1}$$ jsou ortogonální právě když #flashcard 
jejich skalární součin je nula $$v^{T}u = 0 = v_0 u_0 + ... + v_p u_p$$
<!--ID: 1613478006149-->


ortonormální matice #flashcard 
sloupce i řádky jsou ortogonální (vzájemně kolmé) a jsou znormovány na jedničku. Je čtvercová.
<!--ID: 1613478006155-->


$\mathbb{Q}$ je ortogonální. Co je výsledkem $\mathbb{Q}^T \mathbb{Q}$ a proč? #flashcard 
jednotková matice - protože dělám dot produkt ortogonálních vektorů = 0, pouze pro ientitu na diagonále to bude 1
<!--ID: 1613478006161-->


Jak získám inverzní matici k ortogonální matici $\mathbb{Q}$? #flashcard 
transponuju ji, jelikož $\mathbb{Q}^T \mathbb{Q} = \mathbb{E}$ 
<!--ID: 1613478006166-->


dokaž že $||\mathbb{Q}v||^2 = ||v||^2$, kde $\mathbb{Q}$ je ortogonalni #flashcard 
$$||\mathbb{Q}v||^2 = (\mathbb{Q} v)^T \mathbb{Q} v = v^T \mathbb{Q}^T \mathbb{Q} v = v^T \mathbb{E} v = v^T v = ||v||^2$$
<!--ID: 1613478006171-->


proč chceme používat co nejmíň GEM? #flashcard 
GEM je numericky hrozně pomalý, chceme se mu proto vyhnout. Proto je pro inverze nejlepší používat ortogonální matice.
<!--ID: 1613478006176-->

## Lec 02 - 23.02.2021

Odvoď, že X v QR rozkladu má stejný rozměr jako R #flashcard 
Násobení reg. maticí nemění hodnost a Q je regulární (má inverzi)
<!--ID: 1614285966064-->


Dokaž, že v QR rozkladu je j-ty sloupec matice X je lineární kombinací 0..j tych sloupců matice Q. #flashcard 
![[QR_rozklad_LZ_sloupcu_X.png]]
R je trojuhelnikova, takze $X_{:0} = Q_{1:} * R_{11}$.  ($R_{11}$ je nenula, zbytek sloupce $R_{:1}$ jsou nuly), takhle pokracuj a mas to pro j sloupcu, ale j <= p+1
<!--ID: 1614285966070-->


Dokaž pro $QR$ rozklad, že když rozdělíš matici $Q$ na $Q_1$ (p+1 sloupcu) a $Q_2$ (zbytek sloupcu), tak platí, že $X = QR = Q_1R$ #flashcard 
$R$ má od p+2 řádku až do konce jen nuly, takže když jí násobíme, tak stačí jen $Q_1$ a ten horní trojůhelník z R co nejsou nuly. Je to výpočetně i paměťově výhodný.
<!--ID: 1614285966075-->


Dokaž, že když násobím víc ortogonálních matic, tak je výsledek taky ortogonální #flashcard 
$$(Q_1 Q_2)^T Q_2 Q_1 = Q_1^T Q_2^T Q_2 Q_1 = Q_1^T E Q_1 = E$$
<!--ID: 1614285966079-->


Popiš princip algoritmu pro QR rozklad. #flashcard 
![[QR_rozklad_princip.png]]
Využívám toho, že násobení ortogonálních matic je ortogonální matice a že její inverze je její transpozice. Pro každou pozici v R, kde má být nula vyrobím jednu ortogonální matici, kterou když vynásobím X, tak mi vyrobí v R nulu. Ty matice potom spolu pronásobím a transponuju.
Giwensovy rotace - pro každou pozici jedna matice (skoro jednotková)
Hausholdovy reflexe - pro každý sloupec jedna matice
<!--ID: 1614285966083-->

Proč má v QR rozkladu matice Q a R stejnou hodnost? #flashcard 
Protože $A=QR$, no a $Q$ je OG, takže je reg. A násobení regulární maticí nemění hodnost.
Nemění, jelikož každá regulární matice reprezentuje nějakou konečnou posloupnost kroků GEM a GEM nemění hodnost.
<!--ID: 1632748827469-->


Popiš princip QR rozkladu pomocí Giwensovy rotace #flashcard 
Pod diagonálou v R mají být všude nuly. Pro každou nenulovou pozici vytvořím ortogonální matici, kterou když vynásobím s X, tak mi tam vytvoší nulu. Ta ortogonální matice je skoro jednotková, má jen na správném místě na diagonale $[[\alpha, \beta], [-\beta, \alpha]]$ a to mi vytvoří nulu. todo přesné odvození v učebním textu
<!--ID: 1614285966088-->


Popiš princip QR rozkladu pomocí Hausholdovy reflexe #flashcard 
Násobíme X ortogonální maticí ta, aby každá ortogonální matice vytvořila jeden sloupec, co má pod diagonálou nuly.
<!--ID: 1614285966092-->

## Lec 03 - 02.03.2021

Popiš predikci lineární regrese. #flashcard
$$Y=w_{0}+w_{1} x_{1}+\ldots+w_{p} x_{p}+\varepsilon=\boldsymbol{w}^{T} \boldsymbol{x}+\varepsilon$$
kde $E\varepsilon = 0$, což implikuje $EY=\boldsymbol{w}^{T} \boldsymbol{x}$
<!--ID: 1614704131815-->


Popiš RSS v modelu lineární regrese. A řekni co to je #flashcard
$\operatorname{RSS}(\boldsymbol{w})=\sum_{i=1}^{N}\left(Y_{i}-\boldsymbol{w}^{T} \boldsymbol{x}_{i}\right)^{2}=\|\boldsymbol{Y}-\mathbf{X} \boldsymbol{w}\|^{2}$
Je to součet chyb přes všechny body pro kvadratickou ztrátovou funkci. Residuální součet čtverců.
<!--ID: 1614704131823-->


Popiš $\hat{\boldsymbol{w}}_{\mathrm{OLS}}$ v metodě nejmenších čtverců v LR. Dál řekni co musí platit pro matice co používáš. #flashcard 
$$\hat{\boldsymbol{w}}_{\mathrm{OLS}}=\left(\mathbf{X}^{T} \mathbf{X}\right)^{-1} \mathbf{X}^{T} \boldsymbol{Y}$$
$\mathbf{X}^{T} \mathbf{X}$ je regulární, a tudíž můžeme získat její inverzi. Pokud není inverzní, dá se použít pseudoinverzní matice. Sloupce jsou LN. Pokud jsou LZ, nebo skoro LZ, musíme regularizovat pomocí L2 regularizace, což už je hřebenová regrese.
<!--ID: 1614704131827-->


Definuj idempotent matrix #flashcard 
matice pro kterou platí, že $\mathbf{X}^2 = \mathbf{X}$
<!--ID: 1614704131831-->

Dokaž, že $P=$ je idempotentní # flashcard 
todo

Dokaž, že $(I-P)$ je idempotentní, kde $P=$ # flashcard 
$(I-P)^2 = (I-P)(I-P) = I-IP-PI + P^2 = I-2P+P=I-P$
todo

Definuj vlastní čísla #flashcard 
$\lambda \in \mathbb{C}$ je vlastní číslo operátoru $A \in L(V)$, právě když existuje $x \in V, x \neq \theta, tž, Ax=\lambda x$. x je pak vlastní vektor operátoru A příslušející vlastnímu číslu $\lambda$
<!--ID: 1617270927998-->

## Lec 05 - 16.03.2021 - Maticove faktorizace 1

$B, A, P$ jsou matice, dokaz, ze $B$ a $A$ maji stejna vlastni cisla pokud plati: $B=PAP^{-1}$ #flashcard 
![[det_eigenvals.png]]
<!--ID: 1617270928003-->


Kdy jsou si matice $A, B$ podobne? #flashcard 
Pokud existuje regularni $S$ takove, ze $A = S^TBS$
<!--ID: 1617270928007-->


Jakym zpusobem se daji mimo jine ziskat z matice vlastní čísla? #flashcard 
QR algoritmem, který rozkládá matice buď díky Hausholdovým reflexím, nebo Giwensovým rotacím.
<!--ID: 1617270928011-->


Popis zakladni myslenku QR algoritmu #flashcard 
Je to algoritmus pro hledani vlastnich cisel. Idealne v hustych maticich. Jelikoz je to slozite, tak si to iteracnim rozkladanim zjednodusujeme. A to si muzeme dovolit diky tomu, ze podobne matice maji stejna vlastni cisla.
![[PROJECTS/FIT/FIT-2021-2/media/QR_algorithm.png]]
```python
Aiter = A,
for i in range(N):,
    Q, R = np.linalg.qr(Aiter)  # QR rozklad
    Aiter = R.matmul(Q)
assert set(np.linalg.eigvals(Aiter)) == set(np.linalg.eigvals(A))
```
<!--ID: 1617270928015-->


Kdy je matice symetrická? Z jaké množiny čísel jsou vlastní čísla sym. matice? Dokaž to. #flashcard 
když $X^T=X$, což implikuje, že musí být čtvercová.
vl. čísla jsou z $\mathbb{R}$. Což je dobrý, jelikož můžou být z $\mathbb{C}$
![[PON_dukaz.png]]
<!--ID: 1617270928019-->

## Lec 06 - 23.03.2021 - Maticove faktorizace 2

Popis matice v SVD rozkladu. Rekni k cemu je a na co se da toreticky pouzit #flashcard 
$A = U \Sigma V^T$, kde $U$ i $V^T$ jsou ortogonalni, $\Sigma$ je diagonalni matice, co ma na diagonale singular values $\sigma$, pro ktere plati, ze $\sigma^2$ je vl. cislo matice $AA^T, A^TA$.
Zaroven plati, ze $AA^T = U \Sigma^2 U^T$ a $A^TA = V \Sigma^2 V^T$.
pomoci SVD rozkladu se da resit homogeni LSS -> $Xw^T = \theta$ - takhle jsem napr hledal homografii v MPV
Kazda matice se da takhle rozlozit - $U$-rotace, $\Sigma$-stretch, $V^T$-rotace
<!--ID: 1619280752891-->


Jaky je vztah mezi matici $V$ a $U$ v SVD? #flashcard 
$u_i = \frac{1}{\sigma_i} Av_i$
<!--ID: 1619280752898-->


Dokaz, ze vektor $u_i$ z matice $U$ v SVD rozkladu je vlastni vektor matice $AA^T$ a ze je kolmy na vektor $u_j$ #flashcard 
Je vlastni vektor: $AA^Tu_i = expanduj = vyuzij\ vlastni\ vektor\ v_i = \sigma^2u_i$
Je kolmy: $u_i^Tu_j = expanduj = vyuzij\ vlastni\ vektor\ v_i = vykratit = \frac{\sigma_j}{\sigma_i} v_i^Tv_j  = 0$
<!--ID: 1619280752903-->


Jak ziskas SVD rozklad? #flashcard 
1) $A \in \mathbb{R}^{m, n} \rightarrow A^TA \in \mathbb{R}^{n, n}$
2) pro $A^TA$ hledame pomoci $QR$ alg. vlastni cisla $\sigma_i^2 \geq \sigma_r^2$ ($A^TA$ je positivne semi-definitni -> neostre usporadani)
3) najdeme vlastni vektor $v_i$ pro kazde vl. cislo $\sigma_i^2$. Vektory musime doplnit na ON bázi
4) $Av_i = \sigma_i u_i$, $u_i = \frac{1}{\sigma_i} Av_i$
Mame dokazano, ze $u_i$ jsou taky OG a ze jsou vlastni vektory.
<!--ID: 1619280752907-->


## Lec 07 - 30.03.2021 - Maticove faktorizace 3

Je pravda, že matice $A^TA$ a $AA^T$ jsou vždy symetrické? #flashcard 
ano
<!--ID: 1619280752912-->


Je pravda, že je každá symetrická matice diagonalizovatelná? #flashcard 
ano, je to pravda
<!--ID: 1619280752916-->


Jak v SVD rozkladu převedu vlastní vektory $v_i$ matice $A^TA$ na ortonormání bázi? #flashcard 
Buď [Gram-Schmidt process](https://en.wikipedia.org/wiki/Gram%E2%80%93Schmidt_process)
Nebo pomocí QR rozkladu -> platí, že $A=QR$ a platí, že $<slupce\ A> = <sloupce\ Q>$. Generují stejný podprostor a $Q$ je OG -> lze pak snadno převést na ON.
<!--ID: 1619280752921-->

## Lec 08 - 06.04.2021 - Optimalizace 1

Popiš jak vypadá standartní optimalizační problém #flashcard 
minimalizuj $f(x)$,
za podmínek $g(x)=0, h(x) \leq 0$ atd...
kde $f: D \to \mathbb{R}, g: D \to \mathbb{R}^p, h: D \to \mathbb{R}^m$, kde $D \subset \mathbb{R}^n$
<!--ID: 1620909090768-->


Popiš klasifikace optimalizačních úloh #flashcard 
minimalizujeme $f$, $g, h$ jsou podmínky
1) **nelineární programování** (nonlinear programmingNLP): předpokládáme spojitou diferencovatelnost (někdy i dvojitou)
2) **lineární programovnání** (linear programmingLP): f, g a h jsou afinní funkce
3) **kvadratické programování** (quadratic programming LP): f je kvadratická (tj.f(x) = aT· x +12xT· B· x)\*, g a h jsou afinní funkcea)
4) **konvexní optimalizace** (convex optimization): f je konvexní na M
5) **nehladká optimalizace** (non-smooth optimization): některá z funkcí není diferencovatelnáa)(smíšené) celočíselné programování a jeho varianty
<!--ID: 1620909090773-->


Kdy je funkce $f$ totálně diferencovatelná v bodě $a \in D$? #flashcard 
pokud existuje zobrazení $\lambda(x): D \to \mathbb{R}^m$ tž,
$\lim _{h \rightarrow 0} \frac{\|f(a+h)-f(a)-\lambda(h)\|}{\|h\|}=0$
<!--ID: 1620909090777-->


Co za vlastnost (souvisí s derivací) by měla mít funkce, kterou optimalizujeme? #flashcard 
Měla by být dvakrát spojitě diferencovatelná. Abychom mohli použít ty oblíbené iterační metody. Dál často používáme Taylorův rozvoj druhého řádu.
<!--ID: 1620909090781-->


Optimalizační metoda, kdy iterujeme přes posloupnost aproximací konvergující k nějakému minimu. Jaké základní metody pro počítání následující aproximace máme? #flashcard 
**line-search** - Následující aproximaci hledáme v nějakém daném směru $p_k$, směr se dá volit např. jako směr největšího spádu, newtonova metoda atd.
**region-trust** - Na okolí bodu $x_k$ vytvoříme nějakou aproximaci funkce $f$, označené $m_k$, a hledáme minimum této aproximace $m_k$ na okolí bodu $x_k$ 
<!--ID: 1620909090785-->


Optimalizační metoda, kdy iterujeme přes posloupnost aproximací konvergující k nějakému minimu. Je možné najít globální minimum? Zdůvodni a řekni jestli nám lokální minima vadí. #flashcard 
Je to teoreticky možné, ale téměř neupočitatelné. Z toho důvodu se spokojíme s lokálním minimem. Lokální minimum je dostačující, jelikož pro funkce s mnoho parametry je často velmi blízko tomu globálnímu. (například neuronky)
<!--ID: 1620909090789-->


Jaké jsou možné podmínky pro volbu délky kroku v line-search optimalizaci? #flashcard 
**Armijova podmínka** - next step musí být pod klesající přímkou (můžu si dovolit velký krok, jen musí být dost dobrý)
**Goldsteinova podmínka** - Jako Armijova podmínka, jen mám přímku i pro lower boud. - můžu tak minout minimum co bude pod hranicí, ale nedělám miniaturní kroky.
**Wolfeho podmínka** - **slabá** - přímka shora a derivace v next step je větší, než v bodě kde teď jsem (svah není moc strmý), **silná** - přímka shora, sklon je v absolutní hodnotě = krom spádu kouká i na růst
<!--ID: 1620909090792-->


Popiš metodu line-search pro optimalizační úlohu #flashcard 
Následující aproximaci hledáme v nějakém daném směru $p_k$.
$x_{k+1} = x_k + \alpha_kp_k$, kde $p_k$ je směr a $\alpha$ je délka kroku.
<!--ID: 1620909090796-->


Jak se dá volit směr v optimalizační úloze při metodě line-search? #flashcard 
line search $x_{k+1} = x_k + \alpha_kp_k$, kde $p_k$ je směr a $\alpha$ je délka kroku.
Častá volba směru: směr spádu: $p_k = -B_k^{-1}\nabla f(x_k)$
$Bk = I$ - metoda největšího spádu
$B_k = \nabla^2 f(x_k)$ - Newtonova metoda
$B_k \approx \nabla^2 f(x_k)$ - kvazi-Newtonova metoda
<!--ID: 1620909090800-->


Co je metoda největšího spádu při optimalizaci? #flashcard 
typ line-search metody, kdy směr následujícího kroku volíme jako směr, ve kterém funkce nejvíce klesá. To odpovídá směru -gradient v bodě kde právě jsem
<!--ID: 1620909090804-->


Jaká je motivace za exact line search a inexact line search? Proč se co používá? #flashcard 
Najít minimum na line může být dost složitý (exact), proto se hledá nějaká délka kroku, co zajistí dostatečný pokles funkční hodnoty (inexact)
<!--ID: 1620909090809-->


Armijova podmínka #flashcard 
Používá se v kontextu hledání vhodné délky kroku připotimalizaci
definujme pomocnou funkci $\phi(\alpha)$, co mi vrátí hodnotu $f$ pro další krok z bodu $x_k$  ve směru $p_k$, s délkou kroku $\alpha$
$\phi(\alpha) = f(x_k + \alpha p_k), \alpha \geq 0$
Armijova podmínka potom vypadá takto:
$\phi(\alpha_k) \leq \phi(0) + \alpha_kc\phi'(0)$
kde $0 < c < 1$
Tedy funkční hodnota má ležet pod zvolenou přímkou, nalezený krok by však neměl být příliš malý.
<!--ID: 1620909090813-->


Goldsteinova podmínka #flashcard 
Používá se v kontextu hledání vhodné délky kroku připotimalizaci
definujme pomocnou funkci $\phi(\alpha)$, co mi vrátí hodnotu $f$ pro další krok z bodu $x_k$  ve směru $p_k$, s délkou kroku $\alpha$
$\phi(\alpha) = f(x_k + \alpha p_k), \alpha \geq 0$
Goldsteinova podmínka potom vypadá takto:
$\phi(0) + \alpha_k (1-c)\phi'(0) \leq \phi(\alpha_k) \leq \phi(0) + \alpha_kc\phi'(0)$
kde $0 < c < \frac{1}{2}$
Tedy funkční hodnota má ležet mezi zvolenými přímkami: omezuje se nevhodná možnost, že nalezenýkrok bude příliš malý
Nevýhoda: můžeme minout optimálního hodnotu pro $\alpha_k$
<!--ID: 1620909090818-->


Wolfeho slabá podmínka #flashcard 
Používá se v kontextu hledání vhodné délky kroku připotimalizaci
definujme pomocnou funkci $\phi(\alpha)$, co mi vrátí hodnotu $f$ pro další krok z bodu $x_k$  ve směru $p_k$, s délkou kroku $\alpha$
$\phi(\alpha) = f(x_k + \alpha p_k), \alpha \geq 0$
Wolfeho slabá podmínka potom vypadá takto:
$\phi(\alpha_k) \leq \phi(0) + \alpha_kc_1\phi'(0)$
$\phi'(\alpha_k) \geq c_2\phi'(0)$
kde $0 < c_1 < c_2 < 1$
Tedy funkční hodnota má ležet pod zvolenou přímkou a derivace je v dalším kroku větší.
<!--ID: 1620909090822-->


Wolfeho silná podmínka #flashcard 
Používá se v kontextu hledání vhodné délky kroku připotimalizaci
definujme pomocnou funkci $\phi(\alpha)$, co mi vrátí hodnotu $f$ pro další krok z bodu $x_k$  ve směru $p_k$, s délkou kroku $\alpha$
$\phi(\alpha) = f(x_k + \alpha p_k), \alpha \geq 0$
Wolfeho silná podmínka potom vypadá takto:
$\phi(\alpha_k) \leq \phi(0) + \alpha_kc_1\phi'(0)$
$|\phi'(\alpha_k)| \leq c_2|\phi'(0)|$
kde $0 < c_1 < c_2 < 1$
Tedy funkční hodnota má ležet pod zvolenou přímkou a přidáním absolutní hodnoty zajistíme, aby derivace neměla příliš velké hodnoty. (svah i růst není tak strmý)
<!--ID: 1620909090826-->


## Lec 09 - 13.04.2021 - Optimalizace 2

Jaká je obecná myšlenka Newton method? #flashcard 
Předpokládá komplikovanou ztrátovou funkci. Aproximuje jí Taylorem 2. řádu a hledá minimum. Jelikož to je polynom, tak tu rovnici zvládneme vyřešit relativně snadno.
parciální derivace, gradient = 0, normální rovnice atd.
<!--ID: 1620909090830-->


Taylorův polynom 2. stupně pro funkci $f(x_k + p)$ #flashcard 
$f\left(x_{k}+p\right) \approx f\left(x_{k}\right)+\nabla f\left(x_{k}\right)^{T} p+\frac{1}{2} p^{T} \nabla^{2} f\left(x_{k}\right) p=m_{k}\left(x_{k}+p\right)$
<!--ID: 1620909090834-->


Odvoď směr $p_k$ v Newtonově metodě #flashcard 
Taylorův polynom 2. stupně funkce $f\left(x_{k}+p\right)$
$m_{k}\left(x_{k}+p\right) = f\left(x_{k}\right)+\nabla f\left(x_{k}\right)^{T} p+\frac{1}{2} p^{T} \nabla^{2} f\left(x_{k}\right) p$
hledáme $p_{k}=\underset{p}{\operatorname{argmin}} m_{k}\left(x_{k}+p\right)$
parciální derivace, gradient
$\nabla m_{k}\left(x_{k}+p\right)=0 \quad \Longleftrightarrow \quad \nabla f\left(x_{k}\right)+\nabla^{2} f\left(x_{k}\right) p=0$
směr dostaneme takto
$p_k = -(\nabla^2(fx_k))^{-1}\nabla f(x_k)$
Předpokládáme, že $\nabla^2(fx_k)$ je regulární
<!--ID: 1620909090838-->


Co se stane, když v Newtonově metodě není $\nabla^2(fx_k)$ pozitivně definitní? #flashcard 
není zaručeno, že je $p_k$ spádový směr.
<!--ID: 1620909090842-->


Co se dá udělat, když v Newtonově metodě není $\nabla^2(fx_k)$ pozitivně definitní? #flashcard 
Její inverze tedy nemusí existovat, potom je několik možných řešení.
A to nastavit $B_k = \nabla^2(fx_k) + E_k$ tak, aby byla pozitivn2 definitní
* změnou záporných vlastních čísel (bez porušení symetrie přičteš něco, co odstraní záporná vlastní čísla)
* přičtení kladné diag. matice (regularizace - posune všechna vlastní čísla (ridge regresion))
* modifikace nějakého rozkladu $\nabla^2(fx_k)$
* Kvazinewtonovské metody to částečně řeší
<!--ID: 1620909090846-->


Hlavní myšlenka Kvazinewtonových metod? #flashcard 
Kvazinewtonovské metody nějakým způsobem aproximují matici $\nabla^2(fx_k)$ a snaží se tak vylepšit celkově algoritmus, například tím, že matice $B_{k+1}$ se napočítává aktualizací matice $B_k$.
Je to další aproximace, ale velmi výrazně snižuje koplexitu algoritmu. Dá se ukázat, že má podobné vlastnosti jako Newtonova metoda a že konverguje.
<!--ID: 1620909090850-->


Do jake prednsky patri BFGS metoda, co dela? #flashcard 
Je to jedna z Kvazinewtonovskych metod, dela spojitou optimalizaci funkce.
<!--ID: 1620909090854-->


Jak se aproximuje chovani funkce $f$ v bode $x_k + p$ v BFGS metode? #flashcard 
$m_{k}\left(p\right)=f\left(x_{k}\right)+\nabla f\left(x_{k}\right)^{T} p+\frac{1}{2} p^{T} B_{k} p$
<!--ID: 1620909090858-->


Jaké jsou podmínky pro aproximaci matice $B_{k+1}$ na základě znalosti $B_k$ v BFGS metodě? #flashcard 
$m_{k+1}$ musí mít stejný gradient jako $f$ v bodech $x_k$ a $x_{k+1}$
<!--ID: 1620909090862-->


Odvoď rovnici pro aproximaci matice $B_{k+1}$ ze znalosti $B_k$ v metodě BFGS.  Co musí $B_{k+1}$ splňovat? #flashcard 
$m_{k}(p)=f\left(x_{k}\right)+\nabla f\left(x_{k}\right)^{T} p+\frac{1}{2} p^{T} B_{k} p$
jelikož $m_{k+1}$ musí mít stejný gradient jako $f$ v bodech $x_k$ a $x_{k+1}$, tak můžeme položit 
$\nabla m_{k+1}\left(-\alpha_{k} p_{k}\right)=\nabla f\left(x_{k+1}\right)-\alpha_{k} B_{k+1} p_{k}=\nabla f\left(x_{k}\right)$
a tedy
$B_{k+1}\alpha_{k} p_{k} = \nabla f\left(x_{k+1}\right) - \nabla f\left(x_{k}\right)$ a to zjednodušíme na
$B_{k+1}s_k = y_k$
aby rovnice měla řešení, musí pro pozitivně definitní $B_{k+1}$  platit $s_k^T * y_k > 0$, což zaručí wolfeho podmínky pro volbu kroku.
<!--ID: 1620909090866-->


V BFGS musíme invertovat matici $B_{k+1}$. To je jednak numericky nestabilní a druhak náročné. Jak získáme inverzi rovnou? #flashcard 
toto byla rovnice $B_{k+1}s_k = y_k$
jako inverzi si označím neznámou matici $H_{k+1}$
$H_{k+1}y_k = s_k$
pak tam jsou nejake kroky a dostáváme.
$H_{k+1}=\left(I-\frac{s_{k} \cdot y_{k}^{T}}{y_{k}^{T} \cdot s_{k}}\right) H_{k}\left(I-\frac{y_{k} \cdot s_{k}^{T}}{y_{k}^{T} \cdot s_{k}}\right)+\frac{s_{k} \cdot s_{k}^{T}}{y_{k}^{T} \cdot s_{k}}$
<!--ID: 1620909090871-->


Jak volíme matici $H_0$ v BFGS  metodě? #flashcard 
Lze volit jednotkovou matici.
<!--ID: 1620909090875-->


Je pravda, že least-squares problem je speciální případ obecné konvexní optimalizace? #flashcard 
Ano, je to pravda
<!--ID: 1620909090879-->


Je pravda, že konvexní optimalizace je speciální případ lineárního programování? #flashcard 
Ne, není to pravda. 
Lineární programování je speciální případ obecné konvexní optimalizace.
<!--ID: 1620909090883-->


Je pravda, že se dá každý problém převást na obecný konvexní problém? #flashcard 
Ne, není to pravda. 
Je složité poznat, že se dá problém převést na konvexní a je často složité ho poté převést. Když to zvládneme, je už relativně rozumně řešitelný.
Ne vše jde převést na obecný konvexní problém, takové problémy se řeší pomocí nonlinear optimization, na kterou neexistují žádné skutečně efektivní řešení. (global optimization může být i exponenciální)
počteníčko: https://web.stanford.edu/~boyd/cvxbook/bv_cvxbook.pdf
<!--ID: 1620909090886-->


Definuj konvexní množinu $\Omega \in \mathbb{R}^n$ a konvexní funkci $f: \Omega 
\to \mathbb{R}$ #flashcard 
Množina je konvexní, pokud $\alpha x + (1-\alpha)y \in \Omega$
pro $\forall x, y \in \Omega$ a $\forall \alpha \in [0, 1]$ (pro každé dva body lezí všechny body na úsečce mezi nimi v množině. (kružnice, elipsa atd))
funkce je konvexni, pokud $\Omega$ jek onvexni a pokud $f(\alpha x + (1-\alpha )y) \leq \alpha f(x) + (1-\alpha)f(y)$
funkce je ryze konvexni, pokud je tam ostra nerovnost.
<!--ID: 1620909090890-->


Dej mi nějaké vlastnosti konvexních množin  #flashcard 
* $c \in \mathbb{R}, \{x \in \Omega | f(x) \leq c \}$ je konvexní (sublevel set), kde konvexní $f:\Omega \to \mathbb{R}$
* Průnik (ne)konečně mnoha konv. množin je konvexní
* Afinní zobrazení konvexní množiny je konvexní
* Afinní transformace proměnných zachovává konvexitu funkce
* Je-li f konvexní a g konvexní a monotónní funkce, pak je g složeno s f konvexní
<!--ID: 1620909090895-->


Doplň nerovnost místo $(tady)$: $f:\Omega \to \mathbb{R}$ je spojitě diferencovatelná a $\Omega$ je konvexní. Pak platí, že $f$ je konvexní právě tehdy, když: $\forall x, y \in \Omega$,  $f(y)\ (tady) f(x) + \nabla f(x)^T \cdot (y-x)$ #flashcard 
$f(y) \geq + \nabla f(x)^T \cdot (y-x)$
<!--ID: 1620909090898-->


Doplň nerovnost místo $(tady)$: $f:\Omega \to \mathbb{R}$ je spojitě diferencovatelná a $\Omega$ je konvexní. Pak platí, že $f$ je konvexní právě tehdy, když: $\forall x, y \in \Omega, x=y$,  $f(y)\ (tady) f(x) + \nabla f(x)^T \cdot (y-x)$ #flashcard 
$f(y) = f(x) + \nabla f(x)^T \cdot (y-x) \iff f(y) = f(x) + \theta$
<!--ID: 1620909090902-->



Dokaž: $f:\Omega \to \mathbb{R}$ je spojitě diferencovatelná a $\Omega$ je konvexní. Pak platí, že $f$ je konvexní právě tehdy, když: $\forall x, y \in \Omega, f(y) \geq f(x) + \nabla f(x)^T \cdot (y-x)$ #flashcard 
![[konvexni_schema_veta.png]]
![[konvexn_dukaz.png]]
pokud navíc platí $x \neq y$, tak $f(y) > f(x) + \nabla f(x)^T \cdot (y-x)$ ($f$ je ryze konvexní)
<!--ID: 1620909090906-->


Co můžeme říci o bodu $x$, když máme konvexní, spojitě diferencovatelné funkci $f$ když víme, že $\forall y \in \Omega, \nabla f\left(x\right)^{T}\left(y-x\right) \geq 0$ #flashcard 
Můžeme říci, že bod $x$ je bodem globálního minima právě tehdy, když platí výraz výše.
<!--ID: 1620909090910-->


Víme, že $x$ je globální minimum konvexní, spojitě diferencovatelné funkce $f$. Doplň nerovnost za (tady) $\forall y \in \Omega, \nabla f\left(x\right)^{T}\left(y-x\right)\ (tady) 0$ #flashcard 
$\forall y \in \Omega, \nabla f\left(x\right)^{T}\left(y-x\right) \geq 0$
<!--ID: 1620909090914-->


Co můžeme říci o vlastních číslech matice pokud víme, že je matice pozitivně (semi)definitní? #flashcard 
Vlastní čísla pozitivně semi-definitní jsou nezáporná. -> nejmenší vl. číslo musí být nezáporné
Vlastní čísla pozitivně definitní jsou kladná. -> nejmenší vl. číslo musí být kladné
<!--ID: 1620909090918-->


$f:\Omega \to \mathbb{R}$ Platí, že Taylorova aproximace druhého řádu funkce $f$ je konvexní. Je konvexní i funkce $f$. Odůvodni pokud ano-ne #flashcard 
Ano, je to dokonce ekvivalence. Jelikož $f$ je tím pádem dvakrát spojitě diferencovatelná a $\forall x \in \Omega, \nabla^2f(x) \succeq 0$
<!--ID: 1620909090922-->


$f:\Omega \to \mathbb{R}$ je spojitě diferencovatelná a $\Omega$ je uzavřená konvexní množina. Pak platí, že je $f$ konvexní právě tehdy, když $\forall x \in \Omega, \nabla^2f(x) \succeq 0$. Ano/Ne a proč? #flashcard 
Ne, jelikož nevíme, jestli je $f$ dvakrát spojitě diferencovatelná a navíc $\Omega$ musí být otevřená množina.
<!--ID: 1620909090926-->

## Lec 09 - 20.04.2021 - Optimalizace 3

Máme konvexní funkci co minimalizujeme $f$ metodou nejmenšího spádu. funkce má $L$-Lipschitzovsky spojity gradient. Minimum $x^*$ a krok $\alpha_k = \alpha \leq 1/L$. Omez shora $f(x_k)-f(x^*)$ #flashcard 
$f(x_k)-f(x^*) \leq \frac{||x_0-x^*||^2_2}{2\alpha k}$
$\alpha$ je konstanta, důležité je $k$
Tato věta nám ukazuje konvergenci.
<!--ID: 1621103795248-->


dej mi gradient pro konvexní kvadratickou 
funkci $f(x) = a^T \cdot x + \frac{1}{2}x^T \cdot B \cdot x$, kde $x$ je nějaký vektor a $B$ je matice #flashcard 
$\nabla(a^T \cdot x) = a$
$\nabla(\frac{1}{2}x^T \cdot B \cdot x) = \nabla(\frac{1}{2} \sum_{i, j} B^{ij}x_ix_j) = B_{kk}x_k + \frac{1}{2} \sum_{j \neq k} B_{kj}x_j = Bx$
$\nabla f(x) = a + Bx$
<!--ID: 1621103795257-->


Definuj druhotnou Lagrangeovu funkci v kontextu se standartním optimalizačním problémem. #flashcard 
minimalizuj $f(x)$,
za podmínek $g(x)=0, h(x) \leq 0$
kde $f: D \to \mathbb{R}, g: D \to \mathbb{R}^p, h: D \to \mathbb{R}^m$, kde $D \subset \mathbb{R}^n$
přípustná řešení $M = \{x \in D: g(x) = 0 \land h(x) \leq 0\}$
Příslušná Lagrangeova funkce:
$L(x, \lambda, \mu) = f(x) + \lambda^T \cdot g(x) + \mu^T \cdot h(x)$
kde $\lambda$ a $\mu$ jsou vektory Lagrangeových multiplikátorů (**druhotných proměnných**)
Lagrangeova druhotná funkce: $q(\lambda, \mu)=\inf _{x \in D} L(x, \lambda, \mu)$
<!--ID: 1621103795265-->


Dokaž, že pro Lagrangeovu druhotnou funkci platí $q(\lambda, \mu) \leq p* = min f(x)_{x \in M}$ za předpokladu $\mu \geq 0$ #flashcard 
$L(x, \lambda, \mu)=f(x)+\lambda^{T} \underbrace{g(x)}_{=0}+\underbrace{\mu^{T}}_{\geq 0} \underbrace{h(x)}_{\leq 0} \leq f(x)$
pro bod minima $x* \in M$ dostaneme $q(\lambda, \mu) \leq f(x^*) = p*$
<!--ID: 1621103795273-->


Máme Lagrangeovu druhotnou funkci $q(\lambda, \mu)=\inf _{x \in D} L(x, \lambda, \mu)$, kde $L(x, \lambda, \mu) = f(x) + \lambda^T \cdot g(x) + \mu^T \cdot h(x)$ a $f: D \to \mathbb{R}$. A platí že $D$ je konkávní. Můžeme říct o $q$, že je konvexní? #flashcard 
Říct to můžeme, ale nebudeme mít pravdu :D
Víme jen, že pokud je $D$ konvexní, tak je $q$ konkávní.
<!--ID: 1621103795281-->


Je-li prvotní optimalizační problém konvexním problémem a platí-li Slaterova podmínka, pak VŽDY platí $\min f(x)_{x \in M} = \underset{\lambda, \mu \geq 0}{\max } q(\lambda, \mu)$ true/false? #flashcard 
Ano - trů
<!--ID: 1621103795288-->


Definuj Slaterovu podmínku (pro konvexní vázanou optimalizaci) #flashcard 
Existuje alespoň jeden přípustný bod $\overline{x}$ takový, že všechny nerovnostní neafinní podmínky jsou neaktivní (tedy platí ostrá nerovnost).
Jinými slovy = Některé podmínky jsou neostré $\leq, \geq$ atd. Pokud platí jejich ostrá varianta $<, >$, pak je Slaterova podmínka splněna.
<!--ID: 1621103795295-->


Uveď postačující podmínky existence lokálního ostrého minima pomocí Karushovy-Kuhnovy-Tuckerovy (KKT) podmínky. (aspoň vágně, vystihni princip) #flashcard 
Je-li $x^*$ řešení problému nelineárního programování a gradienty $\nabla f(x^∗)$, $\nabla g%j(x^∗)$ a $\nabla h%j(x^∗)$ existují a je splněna podmínka $CQ$, (constraint qualification - gradienty jsou LN (jinak je reseni nekonecne mnoho)) potom existují $λ^*$ a $μ^∗$ takové, že
1) $\nabla f\left(x^{*}\right)+\sum \lambda_{i}^{*} \nabla g_{i}\left(x^{*}\right)+\sum \mu_{j}^{*} \nabla h_{j}\left(x^{*}\right)=0$ (optimalita)
2) $\left(\mu^{*}\right)^{T} h_j\left(x^{*}\right)=0$ (zkráceně $\mu^* = 0 \lor h_j(x^*) = 0$ KKT podminka)
3) $\mu^{*} \geq 0$
U této otázky by bylo nejlepší vědět intiuitivně co co znamená, jinak si otevřít materiály a pochopit to.
<!--ID: 1621103795300-->
