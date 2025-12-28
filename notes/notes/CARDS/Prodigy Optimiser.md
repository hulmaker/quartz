---
tags:
  - ML
  - AI
  - paper
link: https://arxiv.org/pdf/2306.06101
---
[github](https://github.com/konstmish/prodigy)

Parametry:
```
"decouple=True",
"weight_decay=0.01, "d_coef=0.8",
"d0=5e-5",
"use_bias_correction=True",
"betas=0.9,0.99"
```

popis parametrů v kodu: [github docu](https://github.com/konstmish/prodigy/blob/main/prodigyopt/prodigy.py)

Paper ViT training:
* tuned Adam with D-Adaptation outperforms Prodigy!!!! (Prodigy se tuní trochu víc samo)
weight decay **NEZNAMENÁ**, že se zapomíná tréning!!!! OMG, OMG [tady](https://civitai.com/articles/3105/essential-to-advanced-guide-to-training-a-lora#heading-920)
* weight_decay and decoupled = AdamWne
* weight_decay, not decoupled = Adam + L2 regularization
* L2 - mění momenty - přičítá se ke gradientu, pro adaptivní LR to prý regularizuje váhy s velkým gradientem relativně méně než menší váhy
* decoupled - by mělo regularizovat všechny váhy relativně stejně bez ohledu na jejich velikost. Více popsáno v AdamW paperu pod Alg2
* decoupled měj True, AdamW by měl fungovat lépe než AdamL2 podle paperu (black magic)
* "roste to moc rychle" - možná vyzkoušej ladit growth_rate
* d0 nech default, to nic neudělá - leda že fakt víš na čem začít
* **d_coef**
* use_bias_correction - true (adam dělá odhady momentů, protože nemá nekonečnou řadu, tak má bias. bias correction normalizuje momenty kvůli tomu že jsou odhadnuté) - prodigy to má defaultně off, adam defaultně on