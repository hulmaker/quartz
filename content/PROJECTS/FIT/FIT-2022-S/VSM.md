TARGET DECK: FIT-2022-S
FILE TAGS: VSM FIT-2022-S

# Vybrané statistické metody

## Přednášky


- [x] | 01 | 15.2
- [x] | 02 | 17.2
- [x] | 03 | 22.2
- [x] | 04 | 24.2
- [ ] | 05 | 1.3.


### 03 - Náhodné vektory,

Co je náhodný vektor? #flashcard 
Vektor náhodných veličin. Sdružené rozdělení je rozdělení nad vektorem jako celkem. Sčítá se na jedničku, má vlastnosti jako klasické rozdělení.
<!--ID: 1691141660886-->


Co je marginální rozdělení? #flashcard 
Mám náhodný vektor $X$. Když z toho vektoru vyberu libovolnou podmnožinu $k$ náhodných veličin (prvky náh. vektoru), bude to taky náh. vektor, označme $X_k$. Potom sdružené rozdělení vektoru $X_k$ je marginální rozdělení.
<!--ID: 1691141660889-->



Napiš distribuční funkci součtu diskrétních a nezávislých náhodných veličin $Z=X+Y$. #flashcard 
$\mathrm{P}(Z=z)=\sum_{x \in \mathcal{X}} \mathrm{P}(X=x) \mathrm{P}(Y=z-x)$
<!--ID: 1691141660890-->



$X, Y$ jsou náh. veličiny. $var(X \pm Y) = ?$ #flashcard 
$var(X \pm Y) = var(X) + var(Y) \pm 2covar(X, Y)$
Všimni si, že to je analogie pro vzorec $(a \pm b)^2$
<!--ID: 1691141660892-->


Varianční matice náh. vektoru. Vlastnosti. #flashcard 
$$\operatorname{var} \boldsymbol{X}=\left(\begin{array}{cccc}\operatorname{var} X_{1} & \operatorname{cov}\left(X_{1}, X_{2}\right) & \cdots & \operatorname{cov}\left(X_{1}, X_{n}\right) \\ \operatorname{cov}\left(X_{2}, X_{1}\right) & \operatorname{var} X_{2} & \cdots & \operatorname{cov}\left(X_{2}, X_{n}\right) \\ \vdots & \vdots & \ddots & \vdots \\ \operatorname{cov}\left(X_{n}, X_{1}\right) & \operatorname{cov}\left(X_{n}, X_{2}\right) & \cdots & \operatorname{var} X_{n}\end{array}\right)$$
Platí toto: $$\operatorname{cov}\left(X_{i}, X_{j}\right)=\mathrm{E}\left(X_{i}-\mathrm{E} X_{i}\right)\left(X_{j}-\mathrm{E} X_{j}\right)$$
Pak to jde napsat i takhle: $$\operatorname{var} \boldsymbol{X}=\mathrm{E}(\boldsymbol{X}-\mathrm{E} \boldsymbol{X})(\boldsymbol{X}-\mathrm{E} \boldsymbol{X})^{T}$$
Matice je symetrická a pozitivně semidefinitní.
<!--ID: 1691141660893-->


### 04 -  Vícerozměrné normální rozdělení
