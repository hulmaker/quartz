---
tags:
  - on/ai
---
[[NI-MVI]], [[NI-ZI-07]]

## Perceptron
$$y=f\left(\sum_{i=1}^N \omega_i \cdot x_i-\theta\right)$$
kde $f$ je [[Activation Functions]] (se sigmoidou je to vlastně logistická regrese)

## Gradient Descent
MLP se učí se gradientním sestupem.
pro něj potřebujeme target $t$, output $o$:
$$
\begin{aligned}
\Delta w_j &=-\eta \frac{\partial E}{\partial w_j}
			=-\eta (\frac{\partial}{\partial w_j} \frac{1}{2} \sum\left(t^{(i)}-o^{(i)}\right)^2) \\
			&=-\eta \sum_i\left(t^{(i)}-o^{(i)}\right)\left(-x_j^{(i)}\right) \\
			&=\eta \sum_i\left(t^{(i)}-o^{(i)}\right) x_j^{(i)}
\end{aligned}
$$

### Chain Rule
pravidlo, které uplatníme při učení multi layer perceptron #flashcard 
Řetězové pravidlo pojednává o derivacích vnořených funkcí $h^{\prime}(x)=f^{\prime}(g(x)) g^{\prime}(x)$, alternativně: $\frac{d z}{d x}=\frac{d z}{d y} \cdot \frac{d y}{d x}$
<!--ID: 1729010153939-->
