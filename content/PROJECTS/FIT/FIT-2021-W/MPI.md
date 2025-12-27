# Lec 07 - strojová čísla
![[Pasted image 20220104170920.png]]

### Machine epsilon
Vzdálenost 1 od nejbližšího většího čísla.

### Tvrzení 14.1
Vzdálenost normalizovaného čísla x od jeho sousedů je nejméně $\varepsilon \frac{|x|}{2}$ nejvíce $\varepsilon |x|$

### Absolutní, relativní chyba
$a \in \mathbb{R}$ , $fl(a) = \alpha$

Absolutní: $|a - \alpha|$

Relativní: $\frac{|a - \alpha|}{|a|}$

### zaokrouhlovací jednotka - u
Zaokrouhlovací jednotka u je horní závora pro relativní chybu. Pro float platí $u=2^{-23}$

### Tvrzení 14.3
$x$ je normalizované kladné číslo, potom $fl(x) = x(1 + \delta)$, kde $|\delta| \leq u$, kde $u$ je zaokrouhlovací jednotka. 

TLDR: Strojová reprezentace čísla x je nejhůře $xu$. Tj $|fl(x)-x| \leq ux$. Tvrzení 14.4 dodává, že tahle chyba platí i po aritmetických operacích. (pokud nedojde k přetečení)

### Tvrzení 14.5 - Krácení
Chyba vznikající při odčítání. Dochází ke změně exponentu, čísla co jsme neznali musíme doplnit nulami.

**Opezení kolik ztratíme bitů při odečítání:**
$0 < y < x$ jsou strojová čísla, $p, q \in \mathbb{N}$ Platí  že $2^{-p} \leq 1-\frac{y}{x} \leq 2^{-q}$.  Potom je při operaci $x=y$ ztraceno min. $q$ a max $p$ platných bitů.

# Lec 08 - soustavy lin. rovnic
### Dopředná a zpětná chyba
$V$ je algoritmus, $d$ je vstup, $V*(d)$ je přesný výstup.
* Dopředná chyba: $\Delta v = V*(d) - V(d)$
* Zpětná chyba: $\Delta d: V(d+\Delta d) = V*(d)$

### Podmíněnost
Závislost změny výstupu na změně vstupu. Pokud je blízko 1, tak je úloha dobře podmíněná. Tj. Změna na vstupu způsobí podobně velkou změnu na vstupu.

### Věta 4.2 - Spektrální poloměr
Spektrální poloměr je absolutní hodnota největšího vl. č. matice: $\rho(M) := max\{|\lambda|: \lambda \text{ je vlastním číslem } M\}$

**Věta 4.2**:

$M \in \mathbb{C}^{n, n}$,

$lim_{k \to \infty} M^k = 0 \iff \rho(M) < 1$

**Náznak důkazu**: Regulární matice se dá rozložit na diagonální, kde jsou na diagonále vlastní čísla. Pokud budou menší jak jedna, jejich mocnina bude v limitě 0. Pokud budou větší, tak bude nekonečno.

### Algoritmus
Q je reglární. Většinou i ortogonální.
```python
for i in range(maxiter):
	xi = Q_inv @ (np.dot(Q - A, xi) + b)  # update
	if use_refinement:                    # iteration refinement
		rk = b - A@xi
		xi = xi + A_inv@rk
	if stopping_criterion(A, xi, b, tol): # ||Ax-b|| < eps, or |xi - xi-1| < eps
		return xi, i+1
```

# Lec 17 - vlastní čísla

## Mocninná metoda
Iterativní algoritmus vhodný k hledání největšího vlastního čísla.

$x_0 \in \mathbb{C}^n$, potom posloupnost zadaná vztahem $x_{k+1} = Mx_k, k\in\mathbb{N}$ konverguje. 

Potom máme definovanou transformaci, která umí z $x_k$ vytáhnout vlastní vektor příslušející největšímu vlastnímu číslu matice M. No a z něho si potom zjistíme snadno to číslo.