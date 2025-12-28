TARGET DECK: Obsidian::ML
#note/tidy 
[[NI-ZI-07]], [[NI-ZI-08]], [[NI-ZI-09]], [[NI-ZI-10]]


## Feed forward neural networks
[[Multi Layer Perceptron]]

Perceptron - Jak se učí, jak zjistíme směr updatu? #flashcard 
$$y=f\left(\sum_{i=1}^N \omega_i \cdot x_i-\theta\right)$$
kde $f$ je [[Activation Functions]] (se sigmoidou je to vlastně logistická regrese)
Ztráta je MSE
Učí se gradientním sestupem. Krok updatu je proti směru gradientu.
<!--ID: 1729010154097-->



Chain rule - pravidlo, které uplatníme při učení multi layer perceptron #flashcard 
Řetězové pravidlo pojednává o derivacích vnořených funkcí $h^{\prime}(x)=f^{\prime}(g(x)) g^{\prime}(x)$, alternativně: $\frac{d z}{d x}=\frac{d z}{d y} \cdot \frac{d y}{d x}$
Platí za podmínek existence a spojitosti funkce na otevřeném okolí bodu a platí za podmínky diferencovatelnosti obou funkcí.
Pro výpočet gradientu rekurzivně aplikujeme řetězové pravidlo na jednotlivé perceptrony v síti.
$$\frac{\partial E}{\partial w_{i j}^{(L)}}=\sum_{n=1}^{N_L} \frac{\partial E}{\partial n_n^{(L)}} \frac{\partial n_n^{(L)}}{\partial w_{i j}^{(L)}}$$
$w$ je váha v MLP, $E$ je ztrátová funkce. Typicky MSE
<!--ID: 1729010154098-->


## Convolutional Neural Networks
[[Convolutional Neural Networks (CNN)]]


1D, 2D diskrétní konvoluce, můžeš si zkusit i spojitou #flashcard 
$$(x * w)[t]=\sum_\tau x[t-\tau] w[\tau]$$
multiple copies of x translated and scaled by w
$$(x * w)[s, t]=\sum_{\sigma, \tau} x[s-\sigma, t-\tau] w[\sigma, \tau]$$
$$(f * g)(t)=\int_{-\infty}^{\infty} f(x) \cdot g(t-x) \mathrm{d} x$$
<!--ID: 1729010154099-->


Co je pooling, padding, stride a dropout v kontextu conv nets? #flashcard 
**Pooling**: Rozdělíme feature map na bloky. Nad nimi provedeme redukci (max, avg...)
**Stride**: O kolik pixelů se filter posouvá nad feature map. Default=1
**Padding**: Kovoluce ztrácí pixely na periferiích. Padding udělá kolem polštář aby k tomu nedocházelo.
**Dropout**: Pro každý trénovací krok vynechej každý neuron s nějakou nízkou pravděpodobností
<!--ID: 1729010154100-->



Co jsou to residual connections v kontextu neural networks? K čemu slouží? #flashcard 
- Res. connection: connects the output of one earlier convolutional layer to the input of another future convolutional layer several layers later
- overcoming [[Vanishing Gradient Problem]], [[Exploding Gradient Problem]]
<!--ID: 1729010154101-->



Co je to regularizace v kontextu machine learning? #flashcard 
Regularization is a set of strategies used in Machine Learning to reduce the generalization error. Most models, after training, perform very well on a specific subset of the overall population but fail to generalize well. This is also known as overfitting. Regularization strategies aim to reduce overfitting and keep, at the same time, the training error as low as possible.
<!--ID: 1729010154102-->




Jaké techniky regularizace neuronových sítí znáš? #flashcard 
* **L1, L2** - $L_{n e w}(w)=L_{\text {original }}(w)+\lambda\|w\|_1$
* **Weight decay**: $L_{n e w}(w)=L_{\text {original }}(w)+\lambda w^T w$ (weight decay is specified in the weight update rule, L2 reg. is is specified in the objective function)
* **[[Dropout]]** - drops a unit (and connections) at training with probability
* **Label smoothing** - Předpokládáme noise v datech, replace hard 0, 1 target class with a softmax $\frac{\epsilon}{k-1}, 1-\epsilon$
* **Early stopping** - stops training when updates don't help on a validation
* **Weight sharing** - forces a group of parameters to be equal
* Batch, layer, instance, group, **normalization**: normalizace skupiny vah
<!--ID: 1729010154103-->



K čemu je [[Batch Normalization]] v machine learning? #flashcard 
- Makes the training faster and more stable.
- Reduces the internal covariate shift. Works well as a regularisation, reduces the need of [[Dropout]]. Useful with large batches, especially in computer vision.
<!--ID: 1729010154104-->




Co je to [[Autoencoder]] - základní myšlenka. Využití jednoduchého AE #flashcard 
Je to feed forward NN 
![[autoencoder_schema.png]]
Lze je použít např. na  kompresi dat, redukci dimenzionality, generování datových bodů, recommender, překlad.
Trénuje se pomocí reconstruction error - MSE mezi vstupem a výstupem
<!--ID: 1729010154105-->



Jak lze využít autoencoder v computer vision? #flashcard 
Často se používá architektura U-net, která mezi encoder a decoder přidává residual connections:
Superresolution, denoising, image compression, dogenerování barev, oldify, image classification, image generation, semantic segmentation
<!--ID: 1729010154106-->



Autoencodery lze použít na generování. Jaký typ AE se nejčastěji používá a jaké úlohy znáš? #flashcard 
Používají se variational autoencoder (VAE), a generative AI algorithm that uses deep learning to generate new content, detect anomalies and remove noise. Dále se dají použít pro generování textu, časových řad, ale i videa.
VAE se používá jako základ pro stable diffusion.
<!--ID: 1729010154107-->



Jak principielně funguje variational autoencoder (VAE) #flashcard 
A variational autoencoder (VAE) provides a _probabilistic_ manner for describing an observation in latent space. Thus, rather than building an encoder which outputs a single value to describe each latent state attribute, we'll formulate our encoder to describe a probability distribution for each latent attribute.
![[vae.png]]
Z distribucí co dostaneme v latentním prostoru pak můžeme samplovat a dostaneme tak různé výstupy ve stejné distribuci.
[tohle](https://www.jeremyjordan.me/variational-autoencoders/) je super článek.
<!--ID: 1729010154108-->



Jak počítáme ztrátu pro variational autoencoder? Aspoň principielně... #flashcard 
![](https://www.jeremyjordan.me/content/images/2018/03/Screen-Shot-2018-03-17-at-11.31.15-PM.png)
Our loss function for this network will consist of two terms, one which penalizes reconstruction error (which can be thought of maximizing the reconstruction likelihood as discussed earlier) and a second term which encourages our learned distributioni $q(z\mid x)$ to be similar to the true prior distribution $p(x)$, which we'll assume follows a unit Gaussian distribution, for each dimension of the latent space.
$$\mathcal{L}(x, \hat{x})+\sum_j K L\left(q_j(z \mid x) \| p(z)\right)$$
<!--ID: 1729010154109-->


## RNN
[[Recurrent neural network (RNN)]]

Blok rekurentní architektury LSTM - stačí intuitivně #flashcard 
4 gates - forget gate, input gate, candidate memory, output gate (to jsou v poporade ty vetve nahoru)
![](http://dprogrammer.org/wp-content/uploads/2019/04/LSTM-Core-768x466.png)
Steps: 
1. decide what to forget: $f_t = \sigma\left(W_f \cdot\left[h_{t-1}, x_t\right]+b_f\right)$
2. Decide what new information to store in the cell $$\begin{aligned}i_t &= \sigma\left(W_i \cdot\left[h_{t-1}, x_t\right]+b_i\right) \\ \tilde{C}_t &= \tanh \left(W_C \cdot\left[h_{t-1}, x_t\right]+b_C\right) \\ \end{aligned}$$
3. Update the cell: $C_t = f_t * C_{t-1}+i_t * \tilde{C}_t$
4. Decide what to output: $$\begin{aligned} o_t &= \sigma\left(W_o\left[h_{t-1}, x_t\right]+b_o\right) \\ h_t &= o_t * \tanh \left(C_t\right) \end{aligned}$$
<!--ID: 1729010154110-->



Blok rekurentní architektura GRU - stačí intuitivně #flashcard 
![](http://dprogrammer.org/wp-content/uploads/2019/04/GRU.png)
1. update gate: $z_t=\sigma\left(W^{(z)} x_t+U^{(z)} h_{t-1}\right)$
2. reset gate: $r_t=\sigma\left(W^{(r)} x_t+U^{(r)} h_{t-1}\right)$
3. current memory content: $h_t^{\prime}=\tanh \left(W x_t+r_t \odot U h_{t-1}\right)$
4. final memory at current time step: $h_t=z_t \odot h_{t-1}+\left(1-z_t\right) \odot h_t^{\prime}$
Kde operátor $\odot$ je násobení po složkách (jako v numpy)
<!--ID: 1729010154111-->



Porovnání rekurentní architektury: LSTM, GRU, RNN #flashcard 
* GRU Novější RNN, méně parametrů než LSTM.
* GRU Nemá stav buňky, používá vnitřní stav k přenosu informací.
* Není jasné jestli je lepší LSTM nebo GRU, většinou je potřeba zkusit obojí
* RNN je rychlejší - vhodné pro krátké sekvence a krátkodobé vztahy
![](http://dprogrammer.org/wp-content/uploads/2019/04/RNN-vs-LSTM-vs-GRU-1024x308.png)
<!--ID: 1729010154112-->



## Transformery
[[Transformer, Attention]]

Popiš self attention mechanismus. Co je multi-headed attention? #flashcard 
self attention dovoluje pro každé slovo kouknout na ostatní pozice ve vstupu pro lepší kontext a tak vylepšit encoding slova. (Jednoduchý příklad je zájmeno - funguje jen s kontextem)
1. Vstupní vektory vynásobíme maticemi $W_Q, W_K, W_V$ a získáme tak pro každý vektor query, key a value. Matice jsou trainable parameter. (Vektory $q_i, k_i, v_j$ v matici $Q, K, V$)
2. Spočítáme similarity score jako $QK^T$ (cosine similarity je normovaný dot product)
3. Vyděl score $\sqrt{d_k}$ , kde $d_k$ je dimenze key a prožeň to celý softmaxem (stabilizuje, normalizuje, zabíjí malý hodnoty, děláme ze score distribuci)
4. Vynásob values a sečti. Maticově se dá celý proces zapsat jako:
$$\text{Attention}(Q, K, V)=\text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$
Multi headed attention je celý proces paralelně a matice jsou pak skládány do tensorů/channelů.
<!--ID: 1729010154113-->



Namalujte architekturu transformeru #flashcard 
![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/34/Transformer%2C_full_architecture.png/1280px-Transformer%2C_full_architecture.png)
<!--ID: 1729010154114-->


Jaká se používá ztrátová funkce při trénování transformerů? A proč? #flashcard 
**cross-entropy**, nebo **KL-divergence**
Zjednodušeně z dekodéru leze distribuce. Protože děláme supervised learning, tak máme očekávaný překlad. Porovnáváme tedy distribuce.
<!--ID: 1729010154115-->



## Transfer a meta learning

**Meta learning** - Co to je? (kontext deep learning) #flashcard 
Budování high-level systému, který pomáhá tvořit bottom-level systémy. Automatizované učení se učit. 
* Může být za účelem zmenšování modelů, zefektivnění
* Může být dobrý k budování struktury bottom-layer systémů
**Příklady**: 
* neuroevoluce - high-level pomocí evoluce modeluje architekturu sítě
* Hyper Networks - Velká síť učí malou
* RL algoritmy jako IMPALA - actor-critic, actors communicate trajectories of experience (sequences of states, actions, and rewards) to a centralized learner.
Je běžné ukládat meta-znalosti learnera do meta-databáze
<!--ID: 1729010154116-->



**Transfer learning** - co to je, příklady, čím se liší od multi-task learning #flashcard 
* knowledge learned from a task is re-used in order to boost performance on a related task
* Vezmu pre-trained CNN na ImageNet a použiju transfer learning - přeučím na svoji doménu.
* modely fungují lépe, jelikož už mají naučené základní principy. V computer vision se hodně dat vyplýtvá na prvních pár layerů.
* Multi-task learning je současné učení na více úkolech, které si vzájemně můžou benefitovat a stavbilizují se.
<!--ID: 1729010154117-->

