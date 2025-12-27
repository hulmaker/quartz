# 01
$S$ - set of states
$A$ - set of actions
$R_i$ - reward for action $A_i$
$q_*(a)$ - $E[R_t | A_t = a]$  je to value of action = stredni odmena
$Q_t$ - empiricky prumer akce. Podle toho volime v kazdem stavu nejlepsi akci
$Q_t(a)$ - (sum of rewards for a) / (no. times a happend)
$G_t$ - optimalizacni kriterim od casu t dal. Definice nize.
$G_t = \sum^{\infty}_{k=0} \gamma^k R_{t+1+k}$, kde $\gamma \in [0, 1]$ je discount factor

# 02
$v_\pi(s)$ - state-value function. Stredni odmena ve stavu. Optimalizujem (def nize)
$v_\pi(s) = E_\pi[G_t | S_t = s]$
$q_\pi(s, a)$ - action-value function. Stredni odmena akce ze stavu. Optimalizujem. (def nize)
$q_\pi(s, a) = E_\pi[G_t | S_t = s, A_t = a]$



