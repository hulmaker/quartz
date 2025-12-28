---
tags:
  - on/ai
  - on/statistics
  - on/DS
---

### Tomek Links
Remove both noise and borderline examples
Tomek link:
* $E_i, E_j$ belong to different classes, $d(E_i, E_j)$ is the distance between them.
* A $(E_i, E_j)$ pair is called a Tomek link if there is no example $E_\ell$, such that $d(E_i, E_\ell) < d(E_i, E_j)$ or $d(E_j , E_\ell) < d(E_i, E_j)$.
![[tomek_links.png]]
Na redukci se to pouziva tak, ze odebereme bud Ei, nebo Ej podle toho kdo z nich patri do majoritni tridy. Cisti to prostor kolem decision boundary a odstranuje to noise ve prospech minority.