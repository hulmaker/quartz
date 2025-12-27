TARGET DECK: NI-SPOL-2023::NI-PDP
FILE TAGS: NI-SPOL-2023 NI-SPOL-19 NI-PDP

prev::[[NI-SPOL-18]]
next::[[NI-SPOL-20]]

Přímé ortogonální a hyperkubické propojovací sítě paralelních počítačů (definice, vlastnosti, vnořování).


Do jakých kategorií dělíme přímé propojovací sítě paralelních počítačů #flashcard 
Ortogonální topologie: Konstruktor = kartézský součin.
* Binární hyperkrychle (= hypercube).
* Mřížky (= meshes).
* Toroidy (= tori).
Hyperkubické topologie.
* Ŕídké hyperkubické sítě typu motýlek.
* Tlusté stromy.
Closova topologie.
Dragonfly topologie
<!--ID: 1691966314091-->


Podle čeho rozlišujeme topologie grafů na řídké a husté? #flashcard 
Podle stupně. Pokud jsou stupně uzlů omezeny konstantou, tak je topologie řídká. Pokud stupně uzlů rostou splečně s n, pak je topologie hustá.
<!--ID: 1692466734722-->



Definujte pojmy průměr grafu a bisekční šířka grafu #flashcard 
Excentricita UZLU u: $\operatorname{exc}(u)=\max _{v \in V(G)} \operatorname{dist}_G(u, v)$, kde dist je nejkratší cesta mezi u, v
Průměr grafu: $\operatorname{diam}(G)=\max _{u, v} \operatorname{dist}_G(u, v)=\max _u \operatorname{exc}(u)$
Hranová bisekční šířka $bw_e(G)$: velikost nejmenšího hranového řezu co dělí G na poloviny
<!--ID: 1692463928510-->



Základní grafové vlastnosti binární hyperkrychle $Q_n$ - propojovací síť paralelních počítačů #flashcard 
$$
\begin{array}{ll}
V\left(Q_n\right)=\{0,1\}^n=\left\{x_{n-1} x_{n-2} \ldots x_0 ; x_i \in\{0,1\}\right\} & \left|V\left(Q_n\right)\right|=2^n \\
E\left(Q_n\right)=\left\{\left\langle x, \operatorname{neg}_i(x)\right\rangle ; x \in V\left(Q_n\right), 0 \leq i \leq n-1\right\} & \left|E\left(Q_n\right)\right|=n 2^{n-1} \\
\operatorname{diam}\left(Q_n\right)=n & \operatorname{deg}\left(Q_n\right)=\{n\} \\
\mathrm{bw}_{\mathrm{e}}\left(Q_n\right)=2^{n-1} &
\end{array}
$$
Je to regulární graf, bisekční šířka je největší možná, kvůli diam není řídká, hrana je mezi všemi vrcholy co jsou od sebe daleko 1 (hamming)
<!--ID: 1691966314092-->



Odvozené vlastnosti binární hyperkrychle $Q_n$ - propojovací síť paralelních počítačů #flashcard 
* hierarchicky rekurzivní
* optimálně souvislá (hran=vrch. souv.)
* vyvážený bipartitní graf (id partity odvodim z id vrcholu)
* hamiltonovský graf
* je symetrická topologie s $2^n\cdot n !$ automorfismy
* má $K$ různých disjunktních cest mezi $u, v$ o vzdálenosti $k$ a $n-k$ cest délky $k+2$
* logaritmický stupeň, škálovatelnost po mocninách dvojky
<!--ID: 1691966314093-->



Grafové vlastnosti n-rozměrné mřížky $M(z_1, \dots, z_n)$ - propojovací síť paralelních počítačů #flashcard 
$$
\begin{aligned}
& V(M(\ldots))=\left\{\left(a_1, a_2, \ldots, a_n\right) ; 0 \leq a_i \leq z_i-1 \forall i \in\{1, \ldots, n\}\right\} \\
& E(M(\ldots))=\left\{\left\langle\left(\ldots, a_i, . .\right),\left(\ldots, a_i+1, \ldots\right)\right\rangle ; 0 \leq a_i \leq z_i-2\right\} \\
& |V(M(\ldots))|=\Pi_{i=1}^n z_i \quad|E(M(\ldots))|=\Sigma_{i=1}^n\left(z_i-1\right) \prod_{\substack{j=1 \\
j \neq i}}^n z_j \\
& \operatorname{diam}(M(\ldots))=\Sigma_{i=1}^n\left(z_i-1\right)=\Omega(\sqrt[n]{|V(M(\ldots))|}) \\
& \operatorname{deg}(M(\ldots))=\{n, \ldots, n+j\}, j=\left|\left\{z_i ; z_i>2\right\}\right| \\
&\mathrm{bw}_{\mathrm{e}}(M(\ldots)) = \begin{cases}\left(\Pi_{i=1}^n z_i\right) / \max _i z_i & \text { pokud } \max _i z_i \text { je sudé } \\ \Omega\left(\left(\Pi_{i=1}^n z_i\right) / \max _i z_i\right) & \text { jinak }\end{cases}
\end{aligned}
$$
diam je úhlopříčka kvádru
<!--ID: 1691966314094-->



Odvozené vlastnosti  n-rozměrné mřížky $M(z_1, \dots, z_n)$ - propojovací síť paralelních počítačů #flashcard 
* není regulární
* počet uzlů ve vzdálenosti $i$ je řádově $\mathcal{O}(i^{n-1})$(u krychle) -> povrch koule
* dimenzně směrovací algoritmus XYZ <- je ve stejném pořadí
* je vždy bipartitní (ne vždy vyvážená)
* součet souřadnic - sudost/lichost je partita v bipartitním grafu
* existuje vždy hamiltonovská cesta
* mřížka je Hamiltonovská, pokud má alespoň 1 strana sudou délku
<!--ID: 1691966314095-->



Grafové vlastnosti n-rozměrného toroidu $K(z_1, \dots, z_n)$ - propojovací síť paralelních počítačů #flashcard 
n-rozmerna kruznice
$$
\begin{aligned}
& V(K(\ldots))=V(M(\ldots)) \\
& E(K(\ldots))=\left\{\left\langle\left(\ldots, a_i, . .\right),\left(\ldots, a_i \oplus_{z_i} 1, \ldots\right)\right\rangle ; 0 \leq a_i<z_i\right\} \\
& |E(K(\ldots))|=n \times \Pi_{i=1}^n z_i \\
& \operatorname{diam}(K(\ldots))=\Sigma_{i=1}^n\left\lfloor z_i / 2\right\rfloor \\
& \operatorname{deg}(K(\ldots))=\{2 n\} \\
& \mathrm{bw}_{\mathrm{e}}(K(\ldots))=2 \mathrm{bw}_{\mathrm{e}}(M(\ldots))
\end{aligned}
$$
stupen: je regularni, souvislost i bisekční šířka je dvounásobná, je uzlově symetrická, diam: excentricita, prům. vzdálenost, poloměr je cca. dvakrát menší
<!--ID: 1691966314096-->



Odvozené vlastnosti  n-rozměrného toroidu $K(z_1, \dots, z_n)$ - propojovací síť paralelních počítačů #flashcard 
* je regulární
* je uzlově symetrický
* mokud mám kružnice sudé délky, tak je bipartitní
* pokud jsou všechny kružnice sudé délky, je vyvážený
* nejpoužívanější řešení pro počítače
* je uzlově symetrická
* je osově symetrická
<!--ID: 1691966314097-->




Grafové vlastnosti zabaleného motýlku $wBF_n$ - propojovací síť paralelních počítačů #flashcard 
$$
\begin{aligned}
& V\left(w B F_n\right)=\left\{(i, x) ; 0 \leq i<n \wedge x \in\{0,1\}^n\right\} \\
& E\left(w B F_n\right)=\{\left\{\left\langle(i, x),\left(i \oplus_n 1, x\right)\right\rangle\right. \left.\left\langle(i, x),\left(i \oplus_n 1, \operatorname{neg}_i(x)\right)\right\rangle \mid(i, x) \in V\left(w B F_n\right)\right\} \\
&\left|V\left(w B F_n\right)\right|= n 2^n \\
&\left|E\left(w B F_n\right)\right|= n 2^{n+1} \\
& \operatorname{diam}\left(w B F_n\right)=n+\left\lfloor\frac{n}{2}\right\rfloor \\
& \operatorname{deg}\left(w B F_n\right)=\{4\} \\
& \operatorname{bw}_{\mathrm{e}}\left(w B F_n\right)=2^n
\end{aligned}
$$
<!--ID: 1691966314098-->



Odvozené vlastnosti zabaleného motýlku $wBF_n$ - propojovací síť paralelních počítačů #flashcard 
* regulární, řídký
* když je $n$ sudé, tak je vyvážený bipartitní
* Hamiltonovský graf
* uzlově symetrický
<!--ID: 1691966314099-->



Grafové vlastnosti obyčejného motýlku $oBF_n$ - propojovací síť paralelních počítačů #flashcard 
$$
\begin{array}{ll}
V\left(o B F_n\right)=\left\{(i, x) ; 0 \leq i \leq n \wedge x \in\{0,1\}^n\right\} \\
E\left(o B F_n\right)=\left\{\langle(i, x),(i+1, x)\rangle,\left\langle(i, x),\left(i+1, \operatorname{neg}_i(x)\right)\right\rangle \mid i<n\right\} \\
\left|V\left(o B F_n\right)\right|=(n+1) 2^n & \left|E\left(o B F_n\right)\right|=n 2^{n+1} \\
\operatorname{diam}\left(o B F_n\right)=2 n & \operatorname{deg}\left(o B F_n\right)=\{2,4\} \\
\mathrm{bw}_{\mathrm{e}}\left(o B F_n\right)=2^n &
\end{array}
$$
<!--ID: 1691966314100-->


Odvozené vlastnosti obyčejného motýlku $oBF_n$ - propojovací síť paralelních počítačů #flashcard 
* NENí regulární
* řídký
* NENÍ uzlově symetrický
* bipartitní
* je řádkově symetrický
* je hierarchicky rekurzivní
* když je motýlek obousměrný, tak je topologicky ekvivalentní s tlustým stromem
<!--ID: 1691966314101-->



Definice vnoření v kontextu propojovacích sítí paralelních počítačů #flashcard 
Vnoření $G \to H$ je dvojice zobrazení $\varphi, \xi$:
$\varphi : V(G) \to V(H)$ a $\xi : E(G) \to P(H)$ , kde  $P(H)$ je množina všech cest v $H$
<!--ID: 1691966314102-->


Jaká jsou měřítka kvality vnoření v propojovacích sítích paralelních počítačů? #flashcard
Max. zatížení hostitelského uzlu $$\operatorname{load}(\varphi, \xi)=\max _{v \in V(H)}|\{u \in V(G) ; \varphi(u)=v\}|$$
Expanze vnoření:$$ \operatorname{vexp}(\varphi, \xi)=\frac{|V(H)|}{|V(G)|} $$
Maximální dilatace zdrojových hran v hostitelské síti: (max. délka cesty v cíli, kde ve zdroji byly vrcholy sousedi.)$$ \operatorname{dil}(\varphi, \xi)=\max _{e_1 \in E(G)} \operatorname{len}\left(\xi\left(e_1\right)\right) $$
Maximální zahlcení hostitelské hrany: (kolik má cílová hrana přes sebe cest)$$\operatorname{ecng}(\varphi, \xi)=\max _{e_2 \in E(H)}\left|\left\{e_1 \in E(G) ; e_2 \subseteq \xi\left(e_1\right)\right\}\right| $$
<!--ID: 1692467830553-->



Definuj kvazizometrické grafy a s tím spojené pojmy - propojovací sítě paralelních počítačů #flashcard 
* Grafy G a H jsou kvaziizometrické, pokud existuje vnoření z G do H, které má konstantní hodnoty měřítek kvality vnoření.
* H simuluje G se zpomalením h, pokud každý jeden krok výpočtu na G může být simulován v O(h) krocích na H
* G a H jsou výpočetně ekvivalentní, pokud G dokáže simulovat H s konstantním zpomalením a naopak.
Z toho plyne, že kvaziizometrické sítě jsou výpočetně ekvivalentní, ale ne naopak.
<!--ID: 1691966314103-->



Vnoření mezi mřížkou a toroidem - propojovací sítě paralelních počítačů #flashcard 
Stejné mřížky a toroid jsou kvaziizometrické a proto i výpočetně ekvivalentní. 
Důkaz:
1. $M \subset K \implies K$ simuluje $M$ bez zpomaleni
2. konstrukce:
![[mrizka-toroid.png]]
<!--ID: 1691966314104-->



Vnoření hyperkrychle do mřížky $Q_{2k} \to M(2^k, 2^k)$ - propojovaci site #flashcard 
s load=1 je dolí mez na dilataci $\frac{diam(M)}{diam{Q}}=\frac{2^k-1}{k}$
Chceme minimilaizovat dilataci - hledáme mapování id uzlů Q na id uzlů M:
Varianta 1: lexikograficy seřadím a mapuju 1:1 po řádcích/sloupcích
Varianta 2: Mortonova křivka - fraktální "Z" pattern (sttřídavě lexikograficky tvořím Z ve směru osy x/y (dilatance: $2^{k-1}$)
Druhá varianta se hodí u rekurzivního výpočtu co vede na binom. strom. Ten je totiž ve vzoru hyperkrychle.
<!--ID: 1691966314105-->



Vnoření mezi otevřeným a zabaleným motýlkem $oBF_n, wBF_n$- propojovací sítě paralelních počítačů #flashcard 
Jsou kvaziizometrické, tudíž i výpočetně ekvivalentní. 
$oBF_n \to wBF_n$ dukaz trivialni, load=2, dil=1
$wBF_n \to oBF_n$, load=1, liche dil=3, sude dil=2
![[motylek.png]]
<!--ID: 1691966314106-->
