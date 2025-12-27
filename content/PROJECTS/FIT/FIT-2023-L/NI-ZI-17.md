TARGET DECK: NI-ZI-2023::NI-PON
FILE TAGS: NI-ZI-2023 NI-ZI-17 NI-PON

prev::[[NI-ZI-16]]
next::[[NI-ZI-18]]

# QR rozklad
metody výpočtu, použití při výpočtu odhadu metodou nejmenších čtverců, QR algoritmus pro hledání vlastních čísel.


Popiš princip algoritmu pro QR rozklad. #flashcard 
![[QR_rozklad_princip.png]]
Využívám toho, že násobení ortogonálních matic je ortogonální matice a že její inverze je její transpozice. Pro každou pozici v R, kde má být nula vyrobím jednu ortogonální matici, kterou když vynásobím X, tak mi vyrobí v R nulu. Ty matice potom spolu pronásobím a transponuju.
Giwensovy rotace - pro každou pozici jedna matice (skoro jednotková)
Hausholdovy reflexe - pro každý sloupec jedna matice
<!--ID: 1692383640279-->



$\mathbb{Q}$ je ortogonální. Co je výsledkem $\mathbb{Q}^T \mathbb{Q}$ a proč? #flashcard 
jednotková matice - protože dělám dot produkt ortogonálních vektorů = 0, pouze pro ientitu na diagonále to bude 1
<!--ID: 1692383640280-->



Jak získám inverzní matici k ortogonální matici $\mathbb{Q}$? #flashcard 
transponuju ji, jelikož $\mathbb{Q}^T \mathbb{Q} = \mathbb{E}$
<!--ID: 1692383640281-->



dokaž že $||\mathbb{Q}v||^2 = ||v||^2$, kde $\mathbb{Q}$ je ortogonalni #flashcard 
$$||\mathbb{Q}v||^2 = (\mathbb{Q} v)^T \mathbb{Q} v = v^T \mathbb{Q}^T \mathbb{Q} v = v^T \mathbb{E} v = v^T v = ||v||^2$$
<!--ID: 1692383640282-->




$B, A, P$ jsou matice, dokaz, ze $B$ a $A$ maji stejna vlastni cisla pokud plati: $B=PAP^{-1}$ #flashcard 
![[det_eigenvals.png]]
<!--ID: 1692383640283-->



Kdy jsou si matice $A, B$ podobne? #flashcard 
Pokud existuje regulární $P \in \mathbb{C}^{n, n}$ takova, ze $A = P^{-1}BP$
1. A je podobná A,
2. pokud A je podobná B, pak B je podobná A,
3. pokud A je podobná B a B je podobná D, pak A je podobná D.
<!--ID: 1692383640284-->



Popis zakladni myslenku QR algoritmu #flashcard 
Je to algoritmus pro hledani vlastnich cisel. Idealne v hustych maticich. Jelikoz je to slozite, tak si to iteracnim rozkladanim zjednodusujeme. A to si muzeme dovolit diky tomu, ze podobne matice maji stejna vlastni cisla.
![[EXTRAS/Media/QR_algorithm.png]]
```python
Aiter = A,
for i in range(N):,
    Q, R = np.linalg.qr(Aiter)  # QR rozklad
    Aiter = R.matmul(Q)
assert set(np.linalg.eigvals(Aiter)) == set(np.linalg.eigvals(A))
```
<!--ID: 1692383640285-->



Dokaž, že jsou vlastní čísla symetrické matice z $\mathbb{R}$. #flashcard 
![[vl_sym_z_r.jpg]]
Alternativa: $x$ je vl. vektor
jelikož $(\mathbb{A}x, y) = (x, \mathbb{A} y)$, tak to jde i  takhle
$\lambda\|x\|^{2}=(x, \lambda x)=(x, \mathbb{A} x)=(\mathbb{A} x, x)=(\lambda x, x)=\bar{\lambda}\|x\|^{2}$
Z toho plyne $\bar{\lambda} = \lambda$. Jelikož $x \neq \theta, ||x||= neq 0$
<!--ID: 1692383640286-->



Dokaž, že v QR rozkladu je j-ty sloupec matice X je lineární kombinací 0..j tych sloupců matice Q. #flashcard 
![[QR_rozklad_LZ_sloupcu_X.png]]
R je trojuhelnikova, takze $X_{:0} = Q_{1:} * R_{11}$.  ($R_{11}$ je nenula, zbytek sloupce $R_{:1}$ jsou nuly), takhle pokracuj a mas to pro j sloupcu, ale j <= p+1
<!--ID: 1692383640287-->



Dokaž pro $QR$ rozklad, že když rozdělíš matici $Q$ na $Q_1$ (p+1 sloupcu) a $Q_2$ (zbytek sloupcu), tak platí, že $X = QR = Q_1R$ #flashcard 
$R$ má od p+2 řádku až do konce jen nuly, takže když jí násobíme, tak stačí jen $Q_1$ a ten horní trojůhelník z R co nejsou nuly. Je to výpočetně i paměťově výhodný.
<!--ID: 1692383640288-->



Dokaž, že když násobím víc ortogonálních matic, tak je výsledek taky ortogonální #flashcard 
$$(Q_1 Q_2)^T Q_2 Q_1 = Q_1^T Q_2^T Q_2 Q_1 = Q_1^T E Q_1 = E$$
<!--ID: 1692383640289-->


Givensovy rotace #flashcard 
Hledáme ortogonální matici $S \in \mathbb{R}^{2, 2}$, která otočí nenulový vektor $x = (a, b)^T$ tak, že
výsledný vektor leží na ose $x$ a jeho druhá složka je tak nulová.
$$
Sx=
\left(\begin{array}{cc}
\alpha & \beta \\
-\beta & \alpha
\end{array}\right)\left(\begin{array}{l}
a \\
b
\end{array}\right)=\left(\begin{array}{c} 
\pm\|\boldsymbol{x}\| \\
0
\end{array}\right)=\left(\begin{array}{c} 
\pm \sqrt{a^2+b^2} \\
0
\end{array}\right)$$
![[givens.png]]
$$\alpha=\frac{a}{\sqrt{a^2+b^2}}=\cos \varphi \quad \text { a } \quad \beta=\frac{b}{\sqrt{a^2+b^2}}=\sin \varphi$$
<!--ID: 1692898577928-->



Householderovy reflexe #flashcard 
Hledáme ortogonální matici $\mathbf{P}$ takovou, aby reflektovala vektor $\boldsymbol{x}$ na osu $x$ a tak vyrábíme nuly.
$$\mathbf{P} \boldsymbol{x}=\mathbf{P}\left(\begin{array}{c}
x_1 \\
x_2 \\
\vdots \\
x_m
\end{array}\right)=\left(\begin{array}{c} 
\pm\|\boldsymbol{x}\| \\
0 \\
\vdots \\
0
\end{array}\right)$$
![[Pasted image 20230824172158.png]]
Nakonec se dostaneme k výrazu $\mathbf{P} \boldsymbol{y}=\boldsymbol{y}-2 \boldsymbol{u} \boldsymbol{u}^T \boldsymbol{y}$
<!--ID: 1692898577931-->
