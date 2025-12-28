---
tags:
  - on/ai
  - note/tidy
---

[[NI-MVI]]
[[Multi Layer Perceptron]]


## Early RNNs
Elman Nets (1990) - predict successive words in sentences (can be stacked)
Využívá Back Propagation Thru Time - BPTT kde se rekurence rozbalí a počítá se jako klasická dopředná síť.
![](https://cdn.mathpix.com/snip/images/L1K0Wqaik4WRfreEu8ga4OBDYhUWr5Etlr6NpQpitl8.original.fullsize.png)
$$
\operatorname{net}_j(t)=\sum_i^l x_i(t) v_{j i}+\sum_h^m s_h(t-1) u_{j h}+b_j
$$

Hopfield Network: single layered RNN, where states of neuron are +1/-1
![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Hopfield-net-vector.svg/220px-Hopfield-net-vector.svg.png)
* Hebb unsupervised learning – když se dva neurony aktivují společně, tak se mezi nimi posilují synapse (stejně jako v mozku).
* Hebb Rule - synaptic strengths in the brain change in response to experience


## Long-Short Term Memory (LSTM)
4 gates - forget gate, input gate, candidate memory, output gate (to jsou v poporade ty vetve nahoru)
![](http://dprogrammer.org/wp-content/uploads/2019/04/LSTM-Core-768x466.png)
Steps: 
1. decide what to forget: $f_t = \sigma\left(W_f \cdot\left[h_{t-1}, x_t\right]+b_f\right)$
2. Decide what new information to store in the cell $$\begin{aligned}i_t &= \sigma\left(W_i \cdot\left[h_{t-1}, x_t\right]+b_i\right) \\ \tilde{C}_t &= \tanh \left(W_C \cdot\left[h_{t-1}, x_t\right]+b_C\right) \\ \end{aligned}$$
3. Update the cell: $C_t = f_t * C_{t-1}+i_t * \tilde{C}_t$
4. Decide what to output: $$\begin{aligned} o_t &= \sigma\left(W_o\left[h_{t-1}, x_t\right]+b_o\right) \\ h_t &= o_t * \tanh \left(C_t\right) \end{aligned}$$

## GRU
![](http://dprogrammer.org/wp-content/uploads/2019/04/GRU.png)
1. update gate: $z_t=\sigma\left(W^{(z)} x_t+U^{(z)} h_{t-1}\right)$
2. reset gate: $r_t=\sigma\left(W^{(r)} x_t+U^{(r)} h_{t-1}\right)$
3. current memory content: $h_t^{\prime}=\tanh \left(W x_t+r_t \odot U h_{t-1}\right)$
4. final memory at current time step: $h_t=z_t \odot h_{t-1}+\left(1-z_t\right) \odot h_t^{\prime}$
Kde operátor $\odot$ je násobení po složkách (jako v numpy)


## Comparison RNN, LSTM, GRU
* GRU Novější RNN, méně parametrů než LSTM.
* GRU Nemá stav buňky, používá vnitřní stav k přenosu informací.
* Není jasné jestli je lepší LSTM nebo GRU, většinou je potřeba zkusit obojí
* RNN je rychlejší - vhodné pro krátké sekvence a krátkodobé vztahy
![](http://dprogrammer.org/wp-content/uploads/2019/04/RNN-vs-LSTM-vs-GRU-1024x308.png)