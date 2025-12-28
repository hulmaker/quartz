---
tags:
  - on/ai
  - source/paper
link: https://arxiv.org/pdf/1412.6980
---
Adam (adaptive moment estimation) is an algorithm for first-order gradient-based optimisation of stochastic objective functions, based on adaptive estimates of lower-order moments.

* Only needs first-order gradients
* computes adaptive [[Learning Rate]] for different parameters from estimates of first and second moments of the gradients
* uses roughly defined LR when gradient is unchanging and makes it smaller when it is wild
* memory efficient
* works well for sparse gradients
* Checkout [AdamW](https://pytorch.org/docs/stable/generated/torch.optim.AdamW.html), [arxiv](https://arxiv.org/pdf/1711.05101) with L2 weight regularization (decouped)
* Based on [[AdaGrad Optimiser]], and [[RMSProp Optimiser]]


Read [this](https://www.quora.com/What-is-the-first-order-and-second-order-moment-in-the-Adam-optimizer-What-does-adaptive-moment-estimation-mean) to understand $\beta_1$ and $\beta_2$ and moment estimates

- - -
**Algorithm**: $g_t^2$ indicates the elementwise square $g_t \odot g_t$. Good default settings for the tested machine learning problems are $\alpha=0.001$, $\beta_1=0.9, \beta_2=0.999$ and $\epsilon=10^{-8}$. All operations on vectors are element-wise. With $\beta_1^t$ and $\beta_2^t$ we denote $\beta_1$ and $\beta_2$ to the power $t$.
- - -
**Require**: $\alpha$ : Stepsize
**Require**: $\beta_1, \beta_2 \in[0,1)$ : Exponential decay rates for the moment estimates
**Require**: $f(\theta)$ : Stochastic objective function with parameters $\theta$
**Require**: $\theta_0$ : Initial parameter vector
    $m_0 \leftarrow 0$ (Initialize $1{ }^{\text {st }}$ moment vector)
    $v_0 \leftarrow 0$ (Initialize $2^{\text {nd }}$ moment vector)
    $t \leftarrow 0$ (Initialize timestep)
    **while** $\theta_t$ not converged do
        $t \leftarrow t+1$
        $g_t \leftarrow \nabla_\theta f_t\left(\theta_{t-1}\right)$ (Get gradients w.r.t. stochastic objective at timestep $t$ )
        $m_t \leftarrow \beta_1 \cdot m_{t-1}+\left(1-\beta_1\right) \cdot g_t$ (Update biased first moment estimate)
        $v_t \leftarrow \beta_2 \cdot v_{t-1}+\left(1-\beta_2\right) \cdot g_t^2$ (Update biased second raw moment estimate)
        $\widehat{m}_t \leftarrow m_t /\left(1-\beta_1^t\right)$ (Compute bias-corrected first moment estimate)
        $\widehat{v}_t \leftarrow v_t /\left(1-\beta_2^t\right)$ (Compute bias-corrected second raw moment estimate)
        $\theta_t \leftarrow \theta_{t-1}-\alpha \cdot \widehat{m}_t /\left(\sqrt{\widehat{v}_t}+\epsilon\right)$ (Update parameters)
    **end while**
    **return** $\theta_t$ (Resulting parameters)
- - -
