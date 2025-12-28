---
tags:
  - on/ai
  - on/llm
  - on/CV
---
[[Computer Vision (CV)]], [[Natural Language Processing (NLP)]], [[Generative AI]]

[[ChatGPT - Training Policy (Model Spec)]]

[[NI-MVI]]
#note/tidy 

## Attention mechanism

### Self Attention
self attention dovoluje pro každé slovo kouknout na ostatní pozice ve vstupu pro lepší kontext a tak vylepšit encoding slova. (Jednoduchý příklad je zájmeno - funguje jen s kontextem)
1. Vstupní vektory vynásobíme maticemi $W_Q, W_K, W_V$ a získáme tak pro každý vektor query, key a value. Matice jsou trainable parameter. (Vektory $q_i, k_i, v_j$ v matici $Q, K, V$)
2. Spočítáme similarity score jako $QK^T$ (cosine similarity je normovaný dot product)
3. Vyděl score $\sqrt{d_k}$ , kde $d_k$ je dimenze key a prožeň to celý softmaxem (stabilizuje, normalizuje, zabíjí malý hodnoty, děláme ze score distribuci)
4. Vynásob values a sečti. Maticově se dá celý proces zapsat jako:
$$\text{Attention}(Q, K, V)=\text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$
### Multi headed, masked, cross attention
**Multi headed attention** dělá celý proces paralelně a matice jsou pak skládány do tensorů/channelů.
**Masked attention**:
* Při použití maskingu má model přístup jen ke vstupům, které byly před bodem který se v danou chvíli snaží predikovat, veškeré budoucí pozice jsou maskovány tak, že se jejich váhy nastavují na -inf před vstupem do softmaxu, aby model nemohl podvádět a použít budoucí slova k predikci současného.
**Cross attention**:
* Keys a values jsou generovány z jiného výstupu než queries. 
* Konkrétně toto bývá u decoderu, kde se keys a values berou z encoderu a queries z předchozího výstupu stackovaného decoderu.


# Transformer
- Relevantní pro Language Processing i Computer Vision
- Loss: cross-entropy, nebo KL-divergence. Porovnáváme distribuce. Z dekodéru leze distribuce a jelikož děláme supervised learning, tak labely jsou taky dist.

**Schéma**
![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/34/Transformer%2C_full_architecture.png/1280px-Transformer%2C_full_architecture.png)



