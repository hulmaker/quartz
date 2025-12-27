TARGET DECK: NI-SPOL-2023::NI-VSM
FILE TAGS: NI-SPOL-2023 NI-SPOL-08 NI-VSM

prev::[[NI-SPOL-07]]
next::[[NI-SPOL-09]]

# Markovské řetězce s diskrétním časem


Deinujte náhodný proces #flashcard 
Buďte $(\Omega, \mathcal{F}, P)$ pravděpodobnostní prostor a $T \subseteq R$ indexová množina.
Systém náhodných veličin 
$$\boldsymbol{X}=\left\{X_t \mid t \in T\right\}, \quad X_t: \Omega \rightarrow \mathbb{R}$$
nazyvame realny nahodny proces.
* je-li $t$ spočetná - máme diskrétní čas $\left\{X_n \mid n \in \mathbb{N}_0\right\}$
* je-li $t$ nespočetná - mame spojitý čas $\left\{X_t \mid t \geq 0\right\}$
<!--ID: 1691337743751-->



Definujte markovský řetězec s diskrétním časem a markovskou podmínku #flashcard 
Markovská podmínka:
$$
(\forall n \in \mathbb{N}, \text { a } \forall s, s_0, \ldots, s_{n-1} \in S):
$$
$$
\mathrm{P}\left(X_n=s \mid X_{n-1}=s_{n-1}, \ldots, X_1=s_1, X_0=s_0\right)=\mathrm{P}\left(X_n=s \mid X_{n-1}=s_{n-1}\right)
$$
Náhodný proces $\left\{X_n \mid n \in \mathbb{N}_0\right\}$ s nejvýše spočetnou množinou stavů $S$ nazýváme markovský řetězec s diskrétním časem, pokud splňuje markovskou podmínku.
<!--ID: 1691337743753-->



# limitní vlastnosti


Jaká je střední hodnota a rozptyl v bodě t pro markovský řetězec s diskrétním časem? #flashcard 
$$E X_t=\sum_{x \in X} x_i P\left(X_t=x_i\right)$$
$$\sigma^2(t)=E\left(X_t^2\right)-\left(E X_t\right)^2$$
<!--ID: 1691337743755-->



Jak definujeme autokorelační a autokovarianční funkci mezi náhodnými veličinami markovského procesu ve dvou různých časech? #flashcard 
Autokovarianční, Autokorelační (v tomto pořadí):
$$c_X(t, s)=E\left(\left(X_t-E X_t\right) \cdot\left(X_s-E X_s\right)\right)$$
$$R(t, s)=\frac{c_X(t, s)}{\sqrt{\operatorname{var} X_t} \cdot \sqrt{\operatorname{var} X_s}}$$
<!--ID: 1691337743756-->



Jak klasifikujeme stavy markovského řetězce? #flashcard 
Trvalý: $\mathrm{P}\left(\exists n \in \mathbb{N}: X_n=i \mid X_0=i\right)=1, i\in S$
Přechodný: $\mathrm{P}\left(\exists n \in \mathbb{N}: X_n=i \mid X_0=i\right)<1, i\in S$
Nenulový: stav je přechodný a stř. doba návratu je konečná, tj. $\mu_i < +\infty$, jiak **nulový**
Dosažitelný: z j do i se lze dostat v konečném čase. Pokud jsou stavy vzajemne dosazitelne, pak jsou stejneho typu.
Pohlcující: pokud je **uzavřená množina stavů** tvořena jedním stavem, pak je ten stav pohlcující
<!--ID: 1691337743757-->



Střední doba návratu do stavu v markovském řetězci s disk. časem. Definujte i periodicitu stavu. #flashcard 
$i\in S$, str. dobu navratu definujeme jako:
$$
\mu_i:=\mathrm{E}\left(\tau_i \mid X_0=i\right)= \begin{cases}\sum_{n=1}^{\infty} n f_{i i}(n) & \text { je-li } i \text { trvalý } \\ +\infty & \text { je-li } i \text { přechodný }\end{cases}
$$
kde $f_{ij}(n)$ je pst. ze pst, že řetězec někdy navštíví j, startoval-li v i $f_{i j}(n):=\mathrm{P}\left(\tau_j=n \mid X_0=i\right), n \geq 1, \quad f_{i j}(0):=0$
Perioda stavu: $d(i)=\operatorname{gcd}\left\{n \in \mathbb{N} \mid \mathbf{P}_{i i}(n)>0\right\}$ tj. největší spol. děl. časů, kdy se řetězec vrátí do stavu i.
Stav je periodicky pokud d(i) > 1, stav je aperiodicky, pokud d(i) = 1
<!--ID: 1691337743759-->



Jak zní Chapman-Kolmogorova rovnice pro matice přechodu markovského řetězce? #flashcard 
$\forall n \leq m \leq r \in \mathbb{N}_0$
$\mathbf{P}(n, r)=\mathbf{P}(n, m) \cdot \mathbf{P}(m, r)$
<!--ID: 1691337743760-->



Kdy je markovský řetězec homogenní? #flashcard 
pokud $\forall n \in \mathbb{N} \text { a } \forall i, j \in S$ plati $\mathrm{P}\left(X_{n+1}=j \mid X_n=i\right)=\mathrm{P}\left(X_1=j \mid X_0=i\right)$
Pro homogenni retezec definujeme jednokrokovou matici prechodu:
$\mathbf{P}:=\mathbf{P}(0,1)=\left(\mathrm{P}\left(X_1=j \mid X_0=i\right)\right)_{i j \in S}$
<!--ID: 1691337743762-->



Definujte stacionární rozdělení v kontextu markovských řetězců.
$\left\{X_n \mid n \in \mathbb{N}_0\right\}$ homogenní markovský řetězec s maticí přechodu $P$.
Pokud existuje vektor $\pi$ takový, že
$$
(i) $\forall i \in S: \boldsymbol{\pi}_i \geq 0$,
$$
$$
(ii) $\sum_{i \in S} \boldsymbol{\pi}_i=1$,
$$
pro ktery plati ze: $\pi \cdot P = \pi$. Nazyvame jej stacionarnim rozdelenim retezce
$$\boldsymbol{p}(0)=\boldsymbol{\pi} \Longrightarrow \boldsymbol{p}(n)=\boldsymbol{\pi} \mathbf{P}^n=\boldsymbol{\pi} \mathbf{P}^{n-1}=\cdots=\boldsymbol{\pi} \mathbf{P}=\boldsymbol{\pi}$$
Stac. rozdeleni ma vlastnost: $\mathrm{P}_{\boldsymbol{\pi}}\left(X_n=i\right)=\boldsymbol{\pi}_i$



todo Pohlceni
![[transition_matrix.png]]