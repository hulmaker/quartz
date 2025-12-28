TARGET DECK: NI-ZI-2023::NI-MVI
FILE TAGS: NI-ZI-2023 NI-ZI-09 NI-MVI

prev::[[NI-ZI-08]]
next::[[NI-ZI-10]]

# Rekurentní neuronové sítě a jejich učení, neuroevoluce


Elman Nets - schéma, princip #flashcard 
* Elman net (1990) to predict successive words in sentences
* feed forward networks with partial recurrency
* kontextové vrstvy si krátkodobě zapamatuje výstupy skryté vrstvy
* memory cell for each neuron in hidden layer
* umožňuje detekci časově-proměnlivých příznaků.
![[Elman_net.png]]
<!--ID: 1692816447624-->



Jak se učí Elman Network? #flashcard 
![](https://cdn.mathpix.com/snip/images/L1K0Wqaik4WRfreEu8ga4OBDYhUWr5Etlr6NpQpitl8.original.fullsize.png)
$$
\operatorname{net}_j(t)=\sum_i^l x_i(t) v_{j i}+\sum_h^m s_h(t-1) u_{j h}+b_j
$$
Ztráta je normálně MSE:
$$C=\frac{1}{2} \sum_p^n \sum_k^o\left(d_{p k}-y_{p k}\right)^2$$
![[elman.png]]
Využívá Back Propagation Thru Time - BPTT kde se rekurence rozbalí a počítá se jako klasická dopředná síť.
<!--ID: 1692816447629-->



Hopfield Network - schéma #flashcard 
![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Hopfield-net-vector.svg/220px-Hopfield-net-vector.svg.png)
* single layered recurrent networks
* All the neurons are feedback from all other neurons in the network
* The states of neuron is either +1 or -1 instead of (1 and 0) (the training data too)
* None of the input nodes should be equal to any of the output nodes
<!--ID: 1692816447636-->



Hopfield Network - učení #flashcard 
* Hebb unsupervised learning – když se dva neurony aktivují společně, tak se mezi nimi posilují synapse (stejně jako v mozku).
* Hebb Rule - synaptic strengths in the brain change in response to experience
Algoritmus:
1. Training set: $\mathrm{T}=\left\{x_k \mid x_k=\left(x_{k 1}, \ldots, x_{k n}\right) \in\{-1,1\}^n, k=1, \ldots, p\right\}$
2. Váhy se inicializují na nulu
3. Na trénovacích datech opakuj: $$w_{j i}=\sum_{k=1}^p x_{k j} x_{k i} \quad 1 \leq j \neq i \leq n$$
Active mode:
1. Inicializuj $y=x$
2. vypočítej vnitřní potenciál $\xi_j=\sum_{i=1}^n w_{j i} y_i$
3. Pokud $\xi_j = 0$, tak $y_i = 0$, jinak $y_i = sign(\xi_j)$
8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--
Lze trénovat jako energy function: $E(y)=-\frac{1}{2} \sum_{j=1}^n \sum_{i=1}^n w_{j i} y_j y_i$
Učíme se různé patterny, jako třeba binární obrázek. Po natrénování do sítě pošleme corrupted obrázek a po několik iteracích se obrázek opraví. Lokální minima tedy představují uložené vzory, které fungují jako atraktory.
<!--ID: 1692816447639-->



Reservoirs - Echo State Networks - princip #flashcard 
Používá se k black-box modelingu nelineárních dynamických systémů. Využívá lineárních metod pro nelineární modelování.
* Lze trénovat supervizovaně online i offline
* Vstup je jednoduchý signál co způsobí oscilace. Výstupní signál modeluje složitý děj.
* Typicky velká síť, trénujeme pomocí MSE a každý neuron reaguje na excitaci jinak
<!--ID: 1692816447644-->



LSTM - architektura, lifecycle #flashcard 
4 gates - forget gate, input gate, candidate memory, output gate (to jsou v poporade ty vetve nahoru)
![](http://dprogrammer.org/wp-content/uploads/2019/04/LSTM-Core-768x466.png)
Steps: 
1. decide what to forget: $f_t = \sigma\left(W_f \cdot\left[h_{t-1}, x_t\right]+b_f\right)$
2. Decide what new information to store in the cell $$\begin{aligned}i_t &= \sigma\left(W_i \cdot\left[h_{t-1}, x_t\right]+b_i\right) \\ \tilde{C}_t &= \tanh \left(W_C \cdot\left[h_{t-1}, x_t\right]+b_C\right) \\ \end{aligned}$$
3. Update the cell: $C_t = f_t * C_{t-1}+i_t * \tilde{C}_t$
4. Decide what to output: $$\begin{aligned} o_t &= \sigma\left(W_o\left[h_{t-1}, x_t\right]+b_o\right) \\ h_t &= o_t * \tanh \left(C_t\right) \end{aligned}$$
<!--ID: 1692816447647-->



GRU - architektura #flashcard 
![](http://dprogrammer.org/wp-content/uploads/2019/04/GRU.png)
1. update gate: $z_t=\sigma\left(W^{(z)} x_t+U^{(z)} h_{t-1}\right)$
2. reset gate: $r_t=\sigma\left(W^{(r)} x_t+U^{(r)} h_{t-1}\right)$
3. current memory content: $h_t^{\prime}=\tanh \left(W x_t+r_t \odot U h_{t-1}\right)$
4. final memory at current time step: $h_t=z_t \odot h_{t-1}+\left(1-z_t\right) \odot h_t^{\prime}$
Kde operátor $\odot$ je násobení po složkách (jako v numpy)
<!--ID: 1692816447651-->



Porovnání LSTM, GRU, RNN #flashcard 
* GRU Novější RNN, méně parametrů než LSTM.
* GRU Nemá stav buňky, používá vnitřní stav k přenosu informací.
* Není jasné jestli je lepší LSTM nebo GRU, většinou je potřeba zkusit obojí
* RNN je rychlejší - vhodné pro krátké sekvence a krátkodobé vztahy
![](http://dprogrammer.org/wp-content/uploads/2019/04/RNN-vs-LSTM-vs-GRU-1024x308.png)
<!--ID: 1692816447654-->



Neuroevoluce obecně - formulace #flashcard 
Používáme evoluční programování k modelování topologie sítě, ale často se pouští evoluční algoritmus i na váhy. To dělá problém velmi složitým.
Lze použít na topologii sítě, spojení mezi neurony, váhy, output threshold, gramatika co popisuje konstrukci NN
Kódování:
- genom může mít pevnou nebo proměnnou délku 
- lepší než binární kódování jsou objekty nebo struktury
Operátory křížení:
- ideálně korektní co produkují jen validní potomky (může být složité)
Operátory mutace:
- parametrické: váhy mutucí gaussovským šumem
- strukturální: přidávání a odebírání neuronů a spojů
<!--ID: 1692816447658-->



SANE - Symbiotic, Adaptive Neuro-Evolution (1998) #flashcard 
Based on coevolution:
* simultaneous evolution of multiple populations, mutually influencing each other:
* neurons – weights of links incoming to neuron,
* blueprints - „plans“ of connecting neurons to whole networks.
How to compute fitness:
* neuron – fitness of 5 best networks, which it appeared in
* blueprint – fitness of the describing network
<!--ID: 1692816447660-->



NEAT - NeuroEvolution of Augmenting Topologies (2001) #flashcard 
Postupně staví topologie - malé FCNN propojuje a staví složitější. 
* Délka genomu je proto proměnlivá.
Inovační číslo: "the creation date” of a particular gene
- značí pořadí genetických změn u jedince. Lze díky nim měřit podobnost jediců
Mutace (parametrické i strukturalni)
- Přidáme spoj mezi dva nespojené neurony.
- Interpolace: Mezi dva spojené neurony přidáme další.
Křížení:
- Seřadíme genotypy podle inovačních čísel a postupně slučujeme do potomka
Niching: 
* Noví potomci bez optimálních vah mají slabší fitness, ale nechceme je znevýhodnit kvůli potenciální inovaci.
* niching dělí jedince do kategorií - Jedinci se mezi nimi můžou přenášet.
* gives them time to optimize their weights and “show” that the structural innovation was beneficial
<!--ID: 1692816447664-->



Direct vs. Indirect Encodings - neuroevoluton #flashcard 
Direct encoding: each link (weight) is represented by a dedicated gene
* Not suitable for Large-scale ANN's
Indirect encoding: developmental approaches 
* Cellular encoding
* HyperNEAT/HyperGP
<!--ID: 1692816447667-->



Compositional Pattern Producing Networks (CPPNs) #flashcard 
![](https://www.researchgate.net/profile/Jeff-Clune/publication/224242931/figure/fig1/AS:670039971729429@1536761386593/Compositional-pattern-producing-networks-CPPNs-compose-mathematical-functions-to.jpg)
* Neuronky popisující komplexní vzory. Používá různé kompozice aktivačních funkcí (symetrické, periodické...)
* ptáme se na hodnotu nějaké váhy a ona ji vygeneruje jakožto kompozici nějakých jiných funkcí
Časté aktivace: Bipolar sigmoid, Linear, Gaussian, absolute value, sine, cosine
<!--ID: 1692816447671-->



HyperNEAT - neuroevolution #flashcard 
Vyvíjí NN za použití principů NEAT algoritmu
- technika pro evoluci vysoce škálovaných NN, která využívá pravidelných geometrických tvarů (inspirace přírodou), používá CPNNs
- Rosmisťuje neurony na souřadnice v substrate (prostor s nějakými pravidly, jak propojovat, rekurentní vztahy, minimální threshold atd)
- CPPN dostane na vstup tyto souřadnice a vrátí váhu. 
- Lze škálovat substrate density. Mezi neurony na nějakých pozicích lze vložit další souřadnice a zvýšit tak rozlišení problému při zachování funkce původní sítě.
**HyperGP** = NEAT replaced by Genetic Programming: faster than HyperNEAT
<!--ID: 1692816447674-->
