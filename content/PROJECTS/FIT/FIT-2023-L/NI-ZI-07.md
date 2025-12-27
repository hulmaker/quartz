TARGET DECK: NI-ZI-2023::NI-MVI
FILE TAGS: NI-ZI-2023 NI-ZI-07 NI-MVI

prev::[[NI-ZI-06]]
next::[[NI-ZI-08]]
# Učení dopředných neuronových sítí + regularizace


Perceptron - Jak se učí, jak zjistíme směr updatu? #flashcard 
$$y=f\left(\sum_{i=1}^N \omega_i \cdot x_i-\theta\right)$$
kde $f$ je sigmoida nebo ReLU (se sigmoidou je to vlastně logistická regrese)
Ztráta je MSE
Učí se gradientním sestupem, pro něj potřebujeme target $t$, output $o$:
$$
\begin{aligned}
\Delta w_j &=-\eta \frac{\partial E}{\partial w_j}
			=-\eta (\frac{\partial}{\partial w_j} \frac{1}{2} \sum\left(t^{(i)}-o^{(i)}\right)^2) \\
			&=-\eta \sum_i\left(t^{(i)}-o^{(i)}\right)\left(-x_j^{(i)}\right) \\
			&=\eta \sum_i\left(t^{(i)}-o^{(i)}\right) x_j^{(i)}
\end{aligned}
$$
Krok updatu je proti směru gradientu, to je popsáno výše.
<!--ID: 1691966314071-->



Chain rule - pravidlo, které uplatníme při učení multi layer perceptron #flashcard 
Řetězové pravidlo pojednává o derivacích vnořených funkcí $h^{\prime}(x)=f^{\prime}(g(x)) g^{\prime}(x)$, alternativně: $\frac{d z}{d x}=\frac{d z}{d y} \cdot \frac{d y}{d x}$
Platí za podmínek existence a spojitosti funkce na otevřeném okolí bodu a platí za podmínky diferencovatelnosti obou funkcí.
Pro výpočet gradientu rekurzivně aplikujeme řetězové pravidlo na jednotlivé perceptrony v síti.
$$\frac{\partial E}{\partial w_{i j}^{(L)}}=\sum_{n=1}^{N_L} \frac{\partial E}{\partial n_n^{(L)}} \frac{\partial n_n^{(L)}}{\partial w_{i j}^{(L)}}$$
$w$ je váha v MLP, $E$ je ztrátová funkce. Typicky MSE
<!--ID: 1691966314072-->



Jak se provede update vah v multi layer perceptronu? Uvažujme, že už máme spočítané gradienty. #flashcard 
$w_{i j}^{(\ell)}(t+1)=w_{i j}^{(\ell)}(t)-\alpha \frac{\partial E}{\partial w_{i j}^{(\ell)}(t)}$
$b_j^{(\ell)}(t+1)=b_j^{(\ell)}(t)-\alpha \frac{\partial E}{\partial b_j^{(\ell)}(t)}$
kde $\alpha$ je learning rate $w$ je váha, $b$ je bias a $t$ je čas.
todo: Jde jit jeste dal a odvodit to se sensitivity vektorem, az tomu budes rozumet vic, tak si to preorganizuj
<!--ID: 1691966314073-->



Backpropagation - není nutné odvozovat, jen zkráceně, pro MSE. #flashcard 
* Set $\alpha$, initialize weights
* for step $t=1, 2, ...$ repeat until convergence:
	1. set $a^{(0)} = x^{(t)}$ randomly picked from the training set
	2. for $\ell = 1, 2, ..., L$, compute: $$\mathbf{n}^{(\ell)}=\mathbf{a}^{(\ell-1)} \mathbf{W}^{(\ell)}+\mathbf{b}^{(\ell)} \quad \mathbf{a}^{(\ell)}=f^{(\ell)}\left(\mathbf{n}^{(\ell)}\right)$$
	3. Compute for $n=1, 2, ..., N_L$: $$s_n^{(L)}=2\left(\mathbf{a}_n^{(L)}-\mathbf{t}_n(t)\right) \dot{f}^{(L)}\left(\mathbf{n}_n^{(L)}\right)$$
	4. For $\ell=L-1, ..., 2, 1$, and $j=1, 2, ..., N_\ell$, compute: $$s_j^{(\ell)}=\dot{f}^{(\ell)}\left(n_j^{(\ell)}\right) \sum_{i=1}^{N_{\ell+1}} w_{j i}^{(\ell+1)} s_i^{(\ell+1)}$$
	5. For $\ell=1, 2, ..., L$ update:  $$\begin{aligned}  w_{i j}^{(\ell)}(t+1) &=w_{i j}^{(\ell)}(t)-\alpha a_i^{(\ell-1)}(t) s_j^{(\ell)}\\ (t) \\ b_j^{(\ell)}(t+1) &=b_j^{(\ell)}(t)-\alpha s_j^{(\ell)}(t)\\ \end{aligned}$$
$w$: weights, $b$: bias, $s$: sensitivity vector, $\alpha$: learning rate, $t$: target, $\ell$: layer, $f$: activatioin?
<!--ID: 1691966314074-->



Jak vypadá update vah s momentum při backpropagation? #flashcard 
The momentum term is proportional to the change in the weights in the previous
step
$$\Delta w_{i j}^{(\ell)}(t+1)=\alpha a_i^{(\ell-1)}(t) s_j^{(\ell)}(t)+\mu \Delta w_{i j}^{(\ell)}(t)$$
where the momentum parameter $\mu$ lies in the range (0, 1). and $a, s$ are as follows:
$$
\begin{aligned}
\mathbf{a}^{(0)} &= x^{(t)} \\
\mathbf{a}^{(\ell)} &= f^{(\ell)}\left(\mathbf{n}^{(\ell)}\right) \\
\mathbf{n}^{(\ell)} &= \mathbf{a}^{(\ell-1)} \mathbf{W}^{(\ell)}+\mathbf{b}^{(\ell)} \\
s_n^{(L)} &= 2\left(\mathbf{a}_n^{(L)}-\mathbf{t}_n(t)\right) \dot{f}^{(L)}\left(\mathbf{n}_n^{(L)}\right) \\
\end{aligned}
$$
<!--ID: 1691966314075-->


# konvoluční neuronové sítě a regularizace


1D, 2D diskrétní konvoluce, můžeš si zkusit i spojitou #flashcard 
$$(x * w)[t]=\sum_\tau x[t-\tau] w[\tau]$$
multiple copies of x translated and scaled by w
$$(x * w)[s, t]=\sum_{\sigma, \tau} x[s-\sigma, t-\tau] w[\sigma, \tau]$$
$$(f * g)(t)=\int_{-\infty}^{\infty} f(x) \cdot g(t-x) \mathrm{d} x$$
<!--ID: 1691966314076-->




Namalujte diagram architektury typické konvoluční sítě a popište jednotlivé části #flashcard 
![[cnn.png]]
<!--ID: 1691966314077-->



Jak funguje pooling u konvolučních neuronových sítí? #flashcard 
Vrstvy redukují dimenzionalitu a tak nějak redukují výstupy. 
1. rozdělíme feature map na čtverce o velikosti $n + (n-1)\times s$
	* $s$ je parametr pro stride a $n$ je pool size
	* Takže vybereme $n\times n$ pixelů v mřížce a mezi nimi bude $s$ vynechaných míst
2. Na každý pool provedeme redukci (max, average)
3. Výsledky uspořádáme na souřadnice čtverců.
<!--ID: 1691966314078-->



Co je separable kernel při konvoluci, dej příklad takového kernelu #flashcard 
Kernel je separable, pokud pro jeho vícerozměrnou funkci platí: $G(x, y) = g_{x}(x) \cdot g_{y}(y)$ Potom místo 2d konvoluce můžeme aplikovat 2 1d konvoluce, což je rychlejší. Např. Gaussian kernel.
<!--ID: 1691966314079-->



Co je dropout při trénování NN? #flashcard 
pro každý trénovací bod random vynechej několik (0.5 třeba) neuronů. Můžu  vynechávat i vrstvy atd. Je to levná a rychlá metoda regularizace, předchází výrazně overfittingu - nutí generalizovat, vytváří noise.
<!--ID: 1691966314080-->



Co jsou dilated (atrous) konvoluce? #flashcard 
same number of parameters with larger receptive field - convolution filter is distributed to larger area, there is a space between adjoining filter bits.
![[dilated_convolution.png]]
<!--ID: 1691966314081-->



Co je to regularizace v kontextu machine learning? #flashcard 
Regularization is a set of strategies used in Machine Learning to reduce the generalization error. Most models, after training, perform very well on a specific subset of the overall population but fail to generalize well. This is also known as overfitting. Regularization strategies aim to reduce overfitting and keep, at the same time, the training error as low as possible.
<!--ID: 1691966314082-->



Jaké techniky regularizace neuronových sítí znáš? #flashcard 
* L1, L2 - $L_{n e w}(w)=L_{\text {original }}(w)+\lambda\|w\|_1$
* Weight decay: $L_{n e w}(w)=L_{\text {original }}(w)+\lambda w^T w$ (weight decay is specified in the weight update rule, L2 reg. is is specified in the objective function)
* Dropout - drops a unit (and connections) at training with probability
* Label smoothing - Předpokládáme noise v datech, replace hard 0, 1 target class with a softmax $\frac{\epsilon}{k-1}, 1-\epsilon$
* Early stopping - stops training when updates don't help on a validation
* Weight sharing - forces a group of parameters to be equal
* Batch, layer, instance, group, normalization: normalizace skupiny vah
<!--ID: 1691966314083-->
