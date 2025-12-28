TARGET DECK: NI-SPOL-2023::NI-MPI
FILE TAGS: NI-SPOL-2023 NI-SPOL-04 NI-MPI

prev::[[NI-SPOL-03]]
next::[[NI-SPOL-05]]
# Darbouxova konstrukce integralu


Definujte hodní a dolní Darbouxův součet funkce (NI-MPI) #flashcard 
Funkce f je definovaná na intervalu $[a, b]$ a $\sigma={x_0, x_1, ..., x_n}$ je rozdělení toho intervalu. Potom:
$M_i=\sup _{x \in\left[x_{i-1}, x_i\right]} f(x) \quad\quad m_i=\inf _{x \in\left[x_{i-1}, x_i\right]} f(x)$
pro každé $i=1, 2, .., n$. Potom
$$
S_f(\sigma)=\sum_{i=1}^n M_i \Delta_i \quad\quad s_f(\sigma)=\sum_{i=1}^n m_i \Delta_i
$$
kde, $\Delta_i=x_i-x_{i-1}$ Nazýváme horním, resp. dolním, (Darbouxovým) součtem funkce $f$ při rozdělení $\sigma$
<!--ID: 1691269982272-->



Definujte Darbouxův integrál #flashcard 
Horní a dolní Darbouxův integrál fce f na intervalu ab
$D_f=\inf \left\{S_f(\sigma): \sigma \text { je rozdělení }[a, b]\right\}$
$d_f=\sup \left\{s_f(\sigma): \sigma \text { je rozdělení }[a, b]\right\}$
Pokud $D_f = d_f$, nazýváme tuto funkci Darbouxovým integrálem funkce f na intervalu $[a, b]$. 
Značíme to takto: $\int_a^b f(x) \mathrm{d} x=D_f=d_f$
Pokud je f spojitá na ab, tak tam existuje integrál. Pro normální rozdělení pak a lim v n horního a dolního součtu je rovna tomu integrálu.
<!--ID: 1691269982276-->


# Integrál funkcí více proměnných (Darbouxova konstrukce).

Definujte horní a dolní Darbouxovu sumu pro obdélníkovou oblast. #flashcard 
Rozdeleni $\sigma$ je cross product rozdeleni podel jednotlivych os. $D=[a, b] \times [c, d]$
$$S_f(\sigma)=\sum_{i=1}^n \sum_{j=1}^m M_{i, j}\left(x_i-x_{i-1}\right)\left(y_j-y_{j-1}\right)$$
$$s_f(\sigma)=\sum_{i=1}^n \sum_{j=1}^m m_{i, j}\left(x_i-x_{i-1}\right)\left(y_j-y_{j-1}\right)$$
<!--ID: 1691269982280-->


Horní a dolní Darbouxův integrál na obdélníkové oblasti #flashcard 
$D_f=\inf \left\{S_f(\sigma): \sigma \text { je (obdélníkové) rozdělení } D\right\}$
$d_f=\sup \left\{s_f(\sigma): \sigma \text { je (obdélníkové) rozdělení } D\right\} \text {. }$
Pokud $D_f = d_f$ , tak tuto hodnotu nazýváme (dvojitým) Darbouxovým integrálem funkce $f$ na $D$
a značíme ji 
$$\iint_D f(x, y) \mathrm{d} x \mathrm{~d} y=D_f=d_f$$
<!--ID: 1691269982283-->



Jak převést výpočet dvojitého integrálu na dva jednodimenzionální? #flashcard 
Buď $f (x, y)$ integrabilní funkce na $D = [a, b] \times [c, d]$. Pokud existuje jeden z integrálů
$$
\int_a^b\left(\int_c^d f(x, y) \mathrm{d} y\right) \mathrm{d} x \quad \text { nebo } \quad \int_c^d\left(\int_a^b f(x, y) \mathrm{d} x\right) \mathrm{d} y
$$
Potom je roven dvojitemu integralu $\iint_D f(x, y) \mathrm{d} x \mathrm{~d} y$
<!--ID: 1691269982286-->



Dejte předpis pro integrál funkce nad oblastí definované na obrázku. 
![[MPI_integral_oblast.png]] #flashcard 
![[MPI_integral_oblast_reseni.png]]
<!--ID: 1691269982289-->
