TARGET DECK: NI-SPOL-2023::NI-MPI
FILE TAGS: NI-SPOL-2023 NI-SPOL-03 NI-MPI

prev::[[NI-SPOL-02]]
next::[[NI-SPOL-04]]

# Funkce více proměnných
gradient, Hessián, definitnost matic, extrémy funkcí více proměnných bez omezení a s rovnostními omezeními.


Parciální derivace vícerozměrné funkce #flashcard 
Parciální derivace funkce f ve směru $x_i$ v bodě $b = (b_1, b_2, ... , b_n) \in D_f$ takovém, že $\exists H(b) \subset D_f$ , je
$$\lim _{h \rightarrow 0} \frac{f\left(b_1, b_2, \ldots, b_i+h, \ldots, b_n\right)-f\left(b_1, b_2, \ldots, b_i, \ldots, b_n\right)}{h}=L$$
<!--ID: 1692863693765-->



Gradient - definice #flashcard 
Gradient funkce $f$ v bodě $b \in D_f$ je vektor
$$\nabla f(\mathbf{b})=\left(\frac{\partial f}{\partial x_1}(\mathbf{b}), \frac{\partial f}{\partial x_2}(\mathbf{b}), \ldots, \frac{\partial f}{\partial x_n}(\mathbf{b})\right)$$
<!--ID: 1692863693773-->


Derivace ve směru #flashcard 
Nechť $v \in \mathbb{R}^{n, 1} = \mathbb{R}_n, ||v|| = 1$. Derivace funkce $f$ ve směru $v$ v bodě $b \in D_f$ takovém, že
 $\exists H(b) \subset D_f$, je
$$\nabla_{\mathbf{v}} f(\mathbf{b})=\lim _{h \rightarrow 0} \frac{f(\mathbf{b}+h \mathbf{v})-f(\mathbf{b})}{h}$$
<!--ID: 1692863693779-->



Jaké musí nastat podmínky aby platilo $\nabla_{\mathbf{v}} f(\mathbf{b})=\nabla f(\mathbf{b}) \cdot \mathbf{v}$ #flashcard 
Všechny parciální derivace funkce $f$  musí být na nějakém okolí bodu $b$ spojité
<!--ID: 1692863693784-->



Nutná podmínka existence lokálního extrému #flashcard 
Tady jsou dvě věty. Následující je nutná podmínka lokálního extrému:
Nechť má funkce $f : D_f \to \mathbb{R}, D_f \subset \mathbb{R}^n$, v bodě $b$ parciální derivaci podle i-té proměnné. Pokud $f$ má v bodě $b$ lokální extrém, potom:
$$\frac{\partial f}{\partial x_i}(\mathbf{b})=0$$
8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--
Nutná podmínka existence lokálního extrému. Necht $\mathbf{b} \in D_f$ je stacionární bod funkce $f: D_f \rightarrow \mathbb{R}, D_f \subset$ $\mathbb{R}^n$. Necht existuje okolí $H(\mathbf{b}) \subset D_f$ takové, že $f$ má na $H(\mathbf{b})$ spojité všechny druhé parciální derivace, potom
- je-li b lokální minimum, pak $\nabla^2 f(\mathbf{b})$ je pozitivně semidefinitní;
- je-li b lokální maximum, pak $\nabla^2 f(\mathbf{b})$ je negativně semidefinitní.
<!--ID: 1692863693789-->



Hessova matice definice #flashcard 
Máme funkci $f: D_f \rightarrow \mathbb{R}, D_f \subset \mathbb{R}^n$. Existují li druhé parciální derivace funkce $f$ v bodě $b$, pak se zaznamenávají do matice takto
$$\nabla^2 f(\mathbf{b})=\left(\begin{array}{ccc}
\frac{\partial^2 f}{\partial x_1^2}(\mathbf{b}) & \cdots & \frac{\partial^2 f}{\partial x_1 \partial x_n}(\mathbf{b}) \\
\vdots & & \vdots \\
\frac{\partial^2 f}{\partial x_n \partial x_1}(\mathbf{b}) & \cdots & \frac{\partial^2 f}{\partial x_n^2}(\mathbf{b})
\end{array}\right)$$
Matici $\nabla^2f(b)$ nazýváme Hessovou maticí funkce $f$ v bodě $b$ (též Hessián).
<!--ID: 1692863693795-->



Platí li následující výraz, uveďte za jakých podmínek.$$\frac{\partial^2 f}{\partial x \partial y}(\mathbf{b}) =? \frac{\partial^2 f}{\partial y \partial x}(\mathbf{b})$$ #flashcard 
Pokud existuje $\frac{\partial^2 f}{\partial x \partial y}(\mathbf{b})$ a pokud je funkce $\frac{\partial^2 f}{\partial x \partial y}$ spojitá, pak existuje i $\frac{\partial^2 f}{\partial y \partial x}$ a výraz platí.
<!--ID: 1692863693799-->



Jak lze alternativně vyjádřit následující výraz? $\nabla_{\mathbf{v}}\left(\nabla_{\mathbf{v}} f\right)(\mathbf{b})$ #flashcard 
$\nabla_{\mathbf{v}}\left(\nabla_{\mathbf{v}} f\right)(\mathbf{b})=\mathbf{v}^T \cdot \nabla^2 f(\mathbf{b}) \cdot \mathbf{v}$
Platí to za obvyklých podmínek: existuje bod, má spojité druhé derivace na okolí atd.
<!--ID: 1692863693805-->



Definitivnost matic - definice #flashcard 
Definice 4.5 - Definitnost matic. Mějme $\mathbf{A} \in \mathbb{R}^{n, n}$. Řekneme, že matice $\mathbf{A}$ je
1. pozitivně semidefinitní, pokud $\mathbf{x}^T \mathbf{A x} \geq 0$ pro $\forall \mathbf{x} \in \mathbb{R}^{n, 1}$;
2. pozitivně definitní, pokud $\mathbf{x}^T \mathbf{A x}>0$ pro $\forall \mathbf{x} \in \mathbb{R}^{n, 1}, \mathbf{x} \neq 0$;
3. negativně semidefinitní, pokud $\mathbf{x}^T \mathbf{A x} \leq 0$ pro $\forall \mathbf{x} \in \mathbb{R}^{n, 1}$;
4. negativně definitní, pokud $\mathbf{x}^T \mathbf{A x}<0$ pro $\forall \mathbf{x} \in \mathbb{R}^{n, 1}, \mathbf{x} \neq 0$;
5. indefinitní, pokud není pozitivně ani negativně semidefinitní.
<!--ID: 1692863693811-->



Souvislost definitivnosti matic a jejich vlastních čísel. #flashcard 
Buď $A \in R^{n,n}$ symetrická matice. Potom platí následující:
* Matice $A$ je pozitivně semidefinitní právě tehdy, když všechna její vlastní čísla jsou nezáporná.
* Matice $A$ je pozitivně definitní právě tehdy, když všechna její vlastní čísla jsou kladná.
* Matice $A$ je negativně semidefinitní právě tehdy, když všechna její vlastní čísla jsou nekladná.
* Matice $A$ je negativně definitní právě tehdy, když všechna její vlastní čísla jsou záporná.
* Matice $A$ je indefinitní právě tehdy, když má alespoň jedno kladné a alespoň jedno záporné vlastní číslo.
<!--ID: 1692863693816-->



Sylvestrovo kritérium (symetrická matice, definitivnost) #flashcard 
Sylvestrovo kritérium. Buď $\mathbf{A} \in \mathbb{R}^{n, n}$ symetrická matice. Pro matici $\mathbf{A} \in \mathbb{R}^{n, n}$ definujeme matice $A_1, A_2, \ldots, A_n$ takto: $A_k \in \mathbb{R}^{k, k}$ je čtvercová matice v levém horním rohu matice $\mathbf{A}$. Platí:
- Matice $\mathbf{A}$ je pozitivně definitní právě tehdy, když je determinant všech matic $A_1, A_2, \ldots, A_n$ kladný.
- Matice A je negativně definitní právě tehdy, když je determinant matic $A_k$ záporný pro $k$ liché a kladný pro $k$ sudé.
<!--ID: 1692863693821-->



Matice je indefinitní. Má pak na diagonále dva prvky s různým znaménkem? #flashcard 
Ne nutně. Ta implikace funguje obráceně.
Má li matice na diagonále dva prvky s různým znaménkem, pak je indefinitní.
<!--ID: 1692863693827-->



Postačující podmínka existence extrému a sedlového bodu. #flashcard 
Nechť $\mathbf{b} \in D_f$ je stacionární bod funkce $f: D_f \rightarrow \mathbb{R}, D_f \subset \mathbb{R}^n$. Nechť existuje okolí $H(\mathbf{b}) \subset D_f$ takové, že $f$ má na $H(\mathbf{b})$ spojité všechny druhé parciální derivace, potom:
- je-li $\nabla^2 f(\mathbf{b})$ pozitivně definitní, pak **b** je ostré lokální minimum;
- je-li $\nabla^2 f(\mathbf{b})$ negativně definitní, pak **b** je ostré lokální maximum;
- je-li $\nabla^2 f(\mathbf{b})$ indefinitní, pak **b** je sedlový bod.
<!--ID: 1692863693832-->



Lagrangeova funkce #flashcard 
Funkce $L: \mathcal{M} \times \mathbb{R}^m \times \mathbb{R}^p \rightarrow \mathbb{R}$ je definována:
$$L(x ; \lambda ; \mu)=f(x)+\sum_{j=1}^m \lambda_j g_j(x)+\sum_{k=1}^p \mu_k h_k(x)$$
Koeficienty $\lambda=\left(\lambda_1, \ldots, \lambda_m\right) \quad \text { a } \quad \mu=\left(\mu_1, \ldots, \mu_p\right)$ jsou Lagrangeovy multiplikátory.
<!--ID: 1692863693838-->



Postačující podmínka pro existenci lokálního minima pro vázanou optimalizaci: #flashcard 
Nechť $f, g_j, h_k$ pro $j \in \hat{m}, k \in \hat{p}$ mají spojité všechny druhé parciální derivace na nějaké otevřené nadmnožině $\tilde{\mathcal{M}} \supset \mathcal{M}$. Pokud trojice $\left(x^* ; \lambda^* ; \mu^*\right) \in \mathbb{R}^n \times \mathbb{R}^m \times \mathbb{R}^p$ splňuje podmínky:
1. (0. derivace) $x^* \in \mathcal{M}$;
2. (1. derivace) $\forall i, \frac{\partial L}{\partial x_i}\left(x^* ; \lambda^* ; \mu^*\right)=0$;
3. (aktivní a neaktivní vazby) Pro každé $k \in \hat{p}, \mu_k=0$ nebo $h_k\left(x^*\right)=0$;
4. (2. derivace) pro každý vektor $0 \neq v \in \mathbb{R}^n$ splňující
$$
\begin{aligned}
& v^T \cdot \nabla g_j\left(x^*\right)=0, \quad \text { pro všechna } j \in \hat{m}, \\
& v^T \cdot \nabla h_k\left(x^*\right)=0, \quad \text { pro všechna } k \in \hat{p}, \mu_k^* \neq 0, \text { platí } \\
& v^T \cdot \nabla_x^2 L\left(x^* ; \lambda^* ; \mu^*\right) \cdot v>0,
\end{aligned}
$$
kde $\nabla_x^2 L$ je Hessova matice funkce $L$ vzhledem k proměnným $x=\left(x_1, x_2, \ldots, x_n\right)$;
5. (správný "směr od hranice $\mathcal{M}$ ) $\mu_k \geq 0$, pro každé $k \in \hat{p}$.
Potom je $x^*$ bodem ostrého lokálního minima
<!--ID: 1692863693844-->
