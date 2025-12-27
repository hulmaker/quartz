TARGET DECK: NI-ZI-2023::NI-MVI
FILE TAGS: NI-ZI-2023 NI-ZI-10 NI-MVI

prev::[[NI-ZI-09]]
next::[[NI-ZI-11]]

# Transformery

## Attention mechanism

Popiš self attention mechanismus. Co je multi-headed attention? #flashcard 
self attention dovoluje pro každé slovo kouknout na ostatní pozice ve vstupu pro lepší kontext a tak vylepšit encoding slova. (Jednoduchý příklad je zájmeno - funguje jen s kontextem)
1. Vstupní vektory vynásobíme maticemi $W_Q, W_K, W_V$ a získáme tak pro každý vektor query, key a value. Matice jsou trainable parameter. (Vektory $q_i, k_i, v_j$ v matici $Q, K, V$)
2. Spočítáme similarity score jako $QK^T$ (cosine similarity je normovaný dot product)
3. Vyděl score $\sqrt{d_k}$ , kde $d_k$ je dimenze key a prožeň to celý softmaxem (stabilizuje, normalizuje, zabíjí malý hodnoty, děláme ze score distribuci)
4. Vynásob values a sečti. Maticově se dá celý proces zapsat jako:
$$\text{Attention}(Q, K, V)=\text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$
Multi headed attention je celý proces paralelně a matice jsou pak skládány do tensorů/channelů.
<!--ID: 1691267649592-->



Attention mechanismus kouká na vstup jako celek. Slova jsou pak zpracovávána paralelně a vytrácí se slovosled. Jak se s tímhle problémem vypořádáme? #flashcard 
Použijeme positional encoding, který ke každému tokenu přidá index slova. Na úrovni matice je to přilepení time vektoru.
<!--ID: 1691267649598-->



Namalujte architekturu transformeru. #flashcard 
![[transformer.jpg]]
![[transformer_resideual_layer_norm_3.png]]
<!--ID: 1691267649603-->



Jaká je ztrátová funkce při trénování transformerů? #flashcard 
Zjednodušeně z dekodéru leze distribuce. Protože děláme supervised learning, tak máme očekávaný překlad. Porovnáváme tedy distribuce. Použijeme cross-entropy, nebo KL-divergence.
<!--ID: 1691267649618-->



Co je masked attention a cross attention. Kde se použijí? #flashcard 
Masked attention:
* Při použití maskingu má model přístup jen ke vstupům, které byly před bodem který se v danou chvíli snaží predikovat, veškeré budoucí pozice jsou maskovány tak, že se jejich váhy nastavují na -inf před vstupem do softmaxu, aby model nemohl podvádět a použít budoucí slova k predikci současného.
Cross attention:
* Keys a values jsou generovány z jiného výstupu než queries. 
* Konkrétně toto bývá u decoderu, kde se keys a values berou z encoderu a queries z předchozího výstupu stackovaného decoderu.
Obojí se uplatní v decoderu.
<!--ID: 1691267649621-->



Jak fungují transformery v computer vision? #flashcard 
Obrázek projde CNN, čímž získáme feature map. Tu pak rozdělíme na vektory a zbytek jde do transformeru jako byl popsán pro NLP. Lze to ale i bez prvotního encodingu. Obrázek se rozřezá na patche, které pak fungují jako vstupní vektory.
<!--ID: 1691267649624-->


# transfer a meta learning

Meta learning - co to je? #flashcard 
Budování high-level systému, který pomáhá tvořit bottom-level systémy. Automatizované učení se učit. 
* Může být za účelem zmenšování modelů, zefektivnění
* Může být dobrý k budování struktury bottom-layer systémů
Příklady: 
* neuroevoluce - high-level pomocí evoluce modeluje architekturu sítě
* Hyper Networks - Velká síť učí malou
* RL algoritmy jako IMPALA - actor-critic, actors communicate trajectories of experience (sequences of states, actions, and rewards) to a centralized learner.
Je běžné ukládat meta-znalosti learnera do meta-databáze
<!--ID: 1691267649626-->



Transfer learning - co to je, příklady, čím se liší od multi-task learning #flashcard 
* knowledge learned from a task is re-used in order to boost performance on a related task
* Vezmu pre-trained CNN na ImageNet a použiju transfer learning - přeučím na svoji doménu.
* modely fungují lépe, jelikož už mají naučené základní principy. V computer vision se hodně dat vyplýtvá na prvních pár layerů.
* Multi-task learning je současné učení na více úkolech, které si vzájemně můžou benefitovat a stavbilizují se.
<!--ID: 1691267649629-->

