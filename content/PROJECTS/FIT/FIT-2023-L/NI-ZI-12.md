TARGET DECK: NI-ZI-2023::NI-ADM
FILE TAGS: NI-ZI-2023 NI-ZI-12 NI-ADM

prev::[[NI-ZI-11]]
next::[[NI-ZI-13]]
# Linear Basis Expansion Model

Describe the ordinary least squares, and the residual sum of squares. #flashcard 
$RSS(w)=\sum^N_{i=1}(Y_i-w_Tx_i)^2=\mid\mid Y-Xw \mid\mid^2$
The minimum is given by the solution of the normal equation corresponding to 
$\nabla RSS(w)=0 \iff X^TY-X^TXw=0$
When $X^TX$ is regular, the solution is $\hat{w}_{OLS} = (X^TX)^{-1}X^TY$
<!--ID: 1691251771679-->



Jakou roli hraji bazove funkce v linear basis expansion model? Vyjmenuj nějaké příklady. (ADM) #flashcard 
Dovolují nám do modelu přidat nelinearitu. Bázické funkce transformují linear features.
Basis function choices:
* $\varphi(x) = x_i$
* $\varphi(x) = x_i^2$, or polynomial regression: $\varphi(x) = x_kx_\ell$
* $\varphi(x)=\log(x_i), \sqrt{x_i}, \sin(x_i), ...$
* $\varphi(x) = \max(0, x_i)$
<!--ID: 1691251771689-->



Define linear basis expansion model and provide examples of basis functions. (ADM) #flashcard 
value $\boldsymbol{x}=(x_1, ..., x_p)^T$ of $X$ gives us target variable $Y$
$$Y=x_1 \varphi_1(\boldsymbol{x}) + ..., x_M \varphi_M(\boldsymbol{x}) + \varepsilon = \boldsymbol{w}^T \boldsymbol{\varphi(x)} + \varepsilon$$
where $\boldsymbol{\varphi} : \chi \rightarrow \mathbb{R}^M$
Basis function choices:
* $\varphi(x) = x_i$
* $\varphi(x) = x_i^2$, or polynomial regression: $\varphi(x) = x_kx_\ell$
* $\varphi(x)=\log(x_i), \sqrt{x_i}, \sin(x_i), ...$
* $\varphi(x) = \max(0, x_i)$
<!--ID: 1691251771697-->



Describe the $RSS_\lambda(w)$ (residual sum of squares) for linear basis ridge regression #flashcard 
$RSS_\lambda(w) = \mid\mid \boldsymbol{Y-\Phi w} \mid\mid^2 + \lambda w^Tw$, where
$$
\boldsymbol{\Phi}=\left(\begin{array}{c}
\boldsymbol{\varphi}\left(\boldsymbol{x}_1\right)^T \\
\vdots \\
\boldsymbol{\varphi}\left(\boldsymbol{x}_N\right)^T
\end{array}\right)=\left(\begin{array}{ccc}
\varphi_1\left(\boldsymbol{x}_1\right) & \cdots & \varphi_M\left(\boldsymbol{x}_1\right) \\
\vdots & \ddots & \vdots \\
\varphi_1\left(\boldsymbol{x}_N\right) & \cdots & \varphi_M\left(\boldsymbol{x}_N\right)
\end{array}\right), \quad \boldsymbol{Y}=\left(\begin{array}{c}
Y_1 \\
\vdots \\
Y_N
\end{array}\right), \quad \boldsymbol{\varepsilon}=\left(\begin{array}{c}
\varepsilon_1 \\
\vdots \\
\varepsilon_N
\end{array}\right)
$$
<!--ID: 1691251771704-->



Describe normal equation,  $\hat{\boldsymbol{w}}_\lambda$ estimation and prediction $Y$ for the linear basis ridge regression #flashcard 
Normal equation: $\boldsymbol{\phi^TY -  \phi^T\phi w} - \lambda \boldsymbol{w = 0}$
solution for $\lambda > 0$: $\hat{\boldsymbol{w}}_\lambda = (\boldsymbol{\phi^T\phi} + \lambda \boldsymbol{I})^{-1} \boldsymbol{\phi^TY}$
prediction of $Y$ at $x$: $\hat{Y}=\boldsymbol{\hat{w}_\lambda^T \varphi(x)}$
<!--ID: 1691251771710-->



$RSS_\lambda(w) = \mid\mid \boldsymbol{Y-\phi w} \mid\mid^2 + \lambda w^Tw$, definujme $\boldsymbol{w = \phi^T \alpha}$, kde $\boldsymbol{\alpha} \in \mathbb{R}^N$. Jaká je (ne)rovnost mezi $\min RSS_\lambda(w)$ a $\min RSS_\lambda(\alpha)$? #flashcard 
$\min RSS_\lambda(w) \leq \min RSS_\lambda(\alpha)$, jelikož když používám $\alpha$, tak mám menší prostor než s $w$. 
Máme ale theorem, který říká, že jsou ta minima stejná a že se dají $w$ a $\alpha$ vzájemně pro to minimum převádět.
<!--ID: 1691251771715-->



# Jadrove metody, Jadrova Regrese,  Kernel Trick


Definuj pozitivne definitni, semi-definitivni, negativne .... a indefinitni matici #flashcard 
$\boldsymbol{A} \in \mathbb{R}^{n, n}$ is 
positive semi-definite: $x^TAx \geq 0, \forall x \in \mathbb{R}^{n, n}$
positive definite: $x^TAx \gt 0, \forall x \in \mathbb{R}^{n, n}$
negative definite: $x^TAx \lt 0, \forall x \in \mathbb{R}^{n, n}$
negative semi-definite: $x^TAx \leq 0, \forall x \in \mathbb{R}^{n, n}$
$A$ is indefinite $\iff \exists x, y \in \mathbb{R}^{n, n}, x^TAx \gt 0 \land y^TAy \lt 0$
<!--ID: 1691251771721-->



Define kernel function $k(x, y)$, define Gram matrix (ADM) #flashcard 
$k(\boldsymbol{x}, \boldsymbol{y}) = \boldsymbol{\varphi(x)^T}\boldsymbol{\varphi(y)}$, where $\boldsymbol{\varphi(x)} = (\varphi_1(\boldsymbol{x}), ..., \varphi_M(\boldsymbol{x}))^T$
Gram matrix: Given a kernel function $k$ and inputs $\boldsymbol{x}_1, . . . ,\boldsymbol{x}_n \in  \chi$, the $n \times n$ matrix $G = (G_{i,j})$, where $G_{i,j} = k(\boldsymbol{x}_i, \boldsymbol{x}_j)$
<!--ID: 1691251771726-->



Formulate the linear model for regression and classification in terms of a dual representation. Using the kernel trick, the basis functions are then given implicitly. #flashcard 
$RSS_\lambda(\alpha) = \mid\mid Y-G\alpha \mid\mid^2 + \lambda\alpha^TG\alpha$, where $G_{i, j}=k(x_i, x_j)$
Minimiser for $\lambda > 0$ is given: $\hat{\alpha}=(G+\lambda I)^{-1}Y$
Prediction of $Y$ at $x$ is: $\hat{Y}=\sum^N_{x=1}\hat{\alpha}_ik(x_i, x)=\hat{\alpha}^Tk(x)$
* input vector $x$ enters only in the form of scalar products
* The replacement of scalar products with a kernel function is known as the kernel trick
* Now the natural extension is to start with a kernel without specifying the basis functions explicitly (allows us to use feature spaces of high, even infinite, dimensionality)
<!--ID: 1691251771731-->



Write examples of kernels used in linear models (ADM) #flashcard 
* Linear kernel: $k(x, y)=x^Ty$
* Polynomial kernel: $k(x, y)=(x^Ty+1)^n$
* RBF kernel: $k(\boldsymbol{x}, \boldsymbol{y})=\mathrm{e}^{-\frac{\|x-y\|^2}{2 \sigma^2}}$
* Kernel for comparing documents: $k\left(\boldsymbol{x}_i, \boldsymbol{x}_j\right)=\frac{\boldsymbol{x}_i^T \boldsymbol{x}_j}{\left\|\boldsymbol{x}_i\right\|\left\|\boldsymbol{x}_j\right\|}$
<!--ID: 1691251771736-->



What are kernel machines, vector machines and sparse vector machines? (ADM) #flashcard 
Kernel machine is model $f(x)=\sum^K_{j=1}\alpha_jk(x, \mu_j)$, where $\mu_1, ... \mu_K \in \chi$ are some centers
Kernel machines corresponds to linear basis expansion with $\varphi_j(\cdot)=k(\cdot, \mu_j)$
Vector machines are special case of Kernel machines $f(x)=\sum^K_{j=1}\alpha_jk(x, x_j)$
Sparse vector machines are vector machines where $\alpha_j = 0$ for many points
<!--ID: 1691251771742-->


# Support Vector Machine (SVM): separabilní a neseparabilní případ

Popiš SVM - lineárně separabilní případ #flashcard 
* Discriminant function: bod lze rozdělit na 2 vektory. Jeden je paralelní a druhý kolmý s decision boundary. Kolmý vektor je úměrný vzdálenosti bodu od hranice. Bodům přidělíme znaménko v závislosti na jaké straně od hranice jsou.
Vzdalenost i-teho bodu $\varphi(x_i)$ je $r_i=\frac{f(x_i)}{\mid\mid w \mid\mid}$. Hledáme tudíž:
$$\max_{w, w_0} \min_i \frac{Y_i(w^T\varphi(x_i)+w_0)}{\mid\mid w \mid\mid} \propto \min_i\frac{1}{\mid\mid w \mid\mid}$$
Řešíme ekvivalentní problém $\min_{w, w_0} \frac{1}{2}\mid\mid w\mid\mid^2 \text{ subject to } Y_i(w^T\varphi(x_i)+w_0)\geq 1 \text{ for all } i$
<!--ID: 1691251771747-->




Popiš SVM - lineárně neseparabilní případ #flashcard 
Řešení, kde $Y_i(w^T\varphi(x_i)+w_0)\geq 1$ neexistuje, proto relaxujeme a penalizujeme body na špatné straně. $\xi_i= \mid Y_i - f(x_i)\mid \text{ (for the wrong side) } 0 \text{ otherwise}$
Pak optimalizujeme: $\mid_{w, w_0, \xi} \frac{1}{2} \mid\mid w\mid\mid^2 + C\sum^N_{i=1}\xi_i$
<!--ID: 1691251771753-->
