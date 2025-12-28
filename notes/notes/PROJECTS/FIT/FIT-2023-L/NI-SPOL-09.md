TARGET DECK: NI-SPOL-2023::NI-VSM
FILE TAGS: NI-SPOL-2023 NI-SPOL-09 NI-VSM

prev::[[NI-SPOL-08]]
next::[[NI-SPOL-10]]

# Markovské řetězce se spojitým časem

## Souvislost s Markovskými řetezci s diskrétním časem


Jaká je střední hodnota a rozptyl v bodě t pro markovský řetězec se spojitým časem? #flashcard 
$$E X_t=\int_{-\infty}^{\infty} x f_{X_t}(x) d x$$
$$\sigma^2(t)=E\left(X_t^2\right)-\left(E X_t\right)^2$$
<!--ID: 1691966314131-->



Definujte markovský řetězec se spojitým časem #flashcard 
Náhodný proces $\{X_t: t \geq 0\}$ s diskrétní množinou stavů $S$ nazýváme MŘsSČ, a splňuje markovskou podmínku
$$
P\left(X_{t_k}=s_k \mid X_{t_{k-1}}=s_{k-1}, \ldots, X_{t_0}=s_0\right)=P\left(X_{t_k}=s_k \mid X_{t_{k-1}}=s_{k-1}\right)
$$
Tedy, že k předpovězení stavu v čase $t + s$ stačí znát stav v čase $t$, na historii nezáleží
Rozdělení v čase $t$: $\boldsymbol{p}_i(t):=\mathrm{P}\left(X_t=i\right), \quad \boldsymbol{p}(t):=\left(\boldsymbol{p}_1(t), \boldsymbol{p}_2(t), \ldots\right)$
<!--ID: 1691966314132-->



Jak vypadá matice pravděpodobností přechodu pro markovské řetězce se spojitým časem? Co platí pro homogenní markovský řetězec? Co nám říká Chapman-Kolmogorov? #flashcard 
Matice pravděpodobností přechodu mezi časy $t \leq s$:
$\mathbf{P}_{i j}(t, s):=\mathrm{P}\left(X_s=j \mid X_t=i\right), \quad \mathbf{P}(t, s):=\left(\mathbf{P}_{i j}(t, s)\right)_{i, j \in S}$
Chapman-Kolmogorov: $\mathbf{P}(t, r)=\mathbf{P}(t, s) \cdot \mathbf{P}(s, r)$, kde $t \leq s \leq r$
Homogenita: $\mathbf{P}(t, t+s)=\mathbf{P}(0, s):=\mathbf{P}(s)$
* Chapman-Kolmogorov: $\mathbf{P}(t+s)=\mathbf{P}(t) \mathbf{P}(s)=\mathbf{P}(s) \mathbf{P}(t)$
* Rozdělení v $t$: $\boldsymbol{p}(t)=\boldsymbol{p}(0) \mathbf{P}(t)$
<!--ID: 1691966314133-->



Matice skokových intenzit (kontext: markov chain, spojitý čas) #flashcard 
Matice přechodu se těžko konstruuje, proto používáme matici skok. intenzit Q:
$Q=\lim _{h \rightarrow 0+} \frac{1}{h}(P(h)-E)$, přičemž $E=P(0)$
* Je to vlastně derivace: $Q=P'(0)$
* Diagonála je nekladná, ostatní prvky jsou nezáporné (součet řádků = 0)
<!--ID: 1691966314134-->



Stacionární rozdělení u markovských řetězců se spojitým časem #flashcard 
Stacionární rozdělení: $\pi = \pi \cdot P(0)$, neboli $\pi \cdot Q = 0$
Detailní rovnováha: $\pi_k \cdot Q_{k j}=\pi_j \cdot Q_{j k}$
Každé $\pi$ splňující detailní rovnováhu je stacionární, ale ne naopak
<!--ID: 1691966314135-->


## souvislost s Poissonovým procesem.

todo

Definujte Poissonův proces #flashcard 
Budte $\left\{X_j \mid j \in \mathbb{N}\right\}$ i.i.d náhodné veličiny s rozdělením $\text{Exp}(\lambda)$. 
Definujeme $\left\{T_n \mid n \in \mathbb{N}\right\}$ takto:
$$
T_0=0, \quad T_n=T_{n-1}+X_n=\sum_{j=1}^n X_j, \quad n \geq 1
$$
Pak nahodny proces $\left\{N_t \mid t \in[0,+\infty)\right\}$, kde $N_t(\omega):=\max \left\{n \in \mathbb{N}_0 \mid T_n(\omega) \leq t\right\}$ nazveme Poissonovym procesem
Alternativní definice: 
Proces $\left\{N_t \mid t \in[0,+\infty)\right\}$  je Poissonův proces, pokud:
* $N_0=0$ skoro jistě
* $N_t-N_s \sim \text { Poisson }(\lambda(t-s))$ pro všechna $t > s \geq 0$
* $\{N_t\}$ má nezávislé přírůstky, tj. $\forall k \in \mathbb{N}$ a pro všechny $0 \leq t_0<t_1<\cdots<t_k$ jsou $N_{t_1}-N_{t_0}, N_{t_2}-N_{t_1}, \ldots, N_{t_k}-N_{t_{k-1}}$ nezávislé.
<!--ID: 1691966314136-->



Jaká je souvislost markovského řetězce a Poissonovým procesem? #flashcard 
Spojitý markovský řetězec pak chápeme jako diskrétní, přičemž čas k provedení dalšího kroku je
řízen Poissonovým procesem s parametrem $\lambda_M$ , resp. Poissonův proces určuje číslo aktuálního
kroku.
<!--ID: 1691966314137-->
