TARGET DECK: NI-ZI-2023::NI-PDD
FILE TAGS: NI-ZI-2023 NI-ZI-04 NI-PDD

prev::[[NI-ZI-03]]
next::[[NI-ZI-05]]
# Metody pro hodnocení a výběr příznaků


Co je obecným cílem feature selection v kontextu zpracování dat? #flashcard 
- cílem je vybrat ty hodnoty, které nesou největší informační hodnotu, nejlépe oddělují data
- zjednodušení dat vede k snížení dimenzionality => může vést k zrychlení modelu
- snaha o nalezení ideální podmnožiny dat, která data zredukuje, ale zachová (případně i zlepší) celkovou informaci, kterou se snažíme z dat získat
- Snaha odpovědět na otázku: “Jak moc je příznak Xi relevantní pro predikování Y”
<!--ID: 1691342018905-->



Taxonomie metod pro výběr příznaků (NI-PDD) #flashcard 
* Univariate method: considers one variable (feature) at a time.
* Multivariate method: considers subsets of variables (features) together.
8<--8<--8<--8<--8<--8<--8<--8<--8<--8<--
* Filter method: ranks features or feature subsets independently of the predictor (classifier). (relevance, robust, may not select the most useful features, statistical tests)
* Wrapper method: uses a classifier to assess features or feature subsets. (usefulness, prone to overfitting, cross validation)
* Embedded method: like wrapper, the search is controlled by the algorithm constructing classifier (je tam nejaka zpetna vazba co meni selekci na zaklade performace) (usefulness, cross validation, less prone to overfitting, heuristic, stochastic, exhaustive search)
* Mutual Information - míra vzájemné závislosti mezi dvěmi náhodnými proměnnými.
<!--ID: 1691342018910-->



Jaké metriky hodnocení relevance se používají pro feature selection v kontextu zpracování dat? #flashcard 
t-test: slouží k ověření hypotéz o konkrétní střední hodnotě/zda dvě normální rozdělení mají stejný rozptyl/střední hodnotu
korelace: Lineární závislost mezi proměnnými (přímá/nepřímá), používá se Pearson, Spearman
entropie: očekávané množství informace, které příznak nese
<!--ID: 1691342018914-->



Jaký je vzorec pro informační entropii? #flashcard 
$H=-\sum_i P_i \log P_i$
<!--ID: 1691342018917-->



Jaký je vzorec pro Pearsonův korelační koeficient? #flashcard 
$$\rho_{X, Y}=\frac{\operatorname{cov}(X, Y)}{\sigma_X \sigma_Y}=\frac{E\left\{\left(X-\mu_X\right)\left(Y-\mu_Y\right)\right\}}{\sigma_X \sigma_Y}$$
<!--ID: 1691342018919-->



Vzorec pro metriku vzájemné informace mezi dvěmi náhodnými proměnnými. Mutual Information #flashcard 
$$
MI(X, Y) = \int P(X, Y) \log \frac{P(X, Y)}{P(X)P(Y)} dXdY
$$
<!--ID: 1691342018922-->



# Selektivní/adaptivní metody redukce počtu instancí


Vysvětlete princip selektivních metod pro redukci počtu instancí. Udejte příklady. #flashcard 
**Selektivní algoritmy** (vybírají v datech vhodné prvky, ostatní zahazují)
- Všechny metody jako (CNN, editing, proximity graphs)
- CNN - postupně přidává prvky dokud správně neklasifikuje všechny body. [NI-ZI-5](https://docs.google.com/document/d/1x5XcmXPiHFP-MClmiXOrQoSfMhyhye839eQYkExmlvY/edit?usp=sharing)
- RNN - výstup z CNN je dále redukován (iteračně zkouší odebrat prvek po prvku a následně je do vybrané podmnožiny vrací na základě zhoršení/zlepšení kvality predikce)
- IB3 - podobný přístup jako CNN, ale vybírá prvky na základě statistického testování, povoluje porušení 100% klasifikace
- DROP3 - postupné odebírání prvků, pokud jejich smazání nemění/neovlivní klasifikaci
<!--ID: 1691342018924-->



Vysvětlete princip adaptivních metod pro redukci počtu instancí. Udejte příklady. #flashcard 
**Adaptivní algoritmy** (proaktivně vytváří nové prvky, kterými nahrazuje ty původní)
- Prototype - spojuje páry bodů, které jsou k sobě nejblíže (a patří do stejné třídy) tím, že je “zmerguje” a výsledný 1 bod bude v prostoru mezi původními 2 body
Chenův algoritmus - umožňuje nastavit požadovanou velikost výsledné podmnožiny, nové body jsou těžiště originálních dat (shluků dat)
<!--ID: 1691342018927-->





Jak funguje Condensed Nearest Neighbor (CNN) metoda? #flashcard 
Aim is to reduce the number of training samples
Retain only the samples that are needed to define the decision boundary
Brute force version in $\mathcal{O}(n^3)$.
1. Initialize subset with a single training example
2. Classify all remaining samples using the subset, and transfer any incorrectly classified samples to the subset
3. Return to 2 until no transfers occurred or the subset is full
<!--ID: 1691342018931-->


## Proximity graphs


Jaké proximity graphs znáš a jak spolu souvisí? (NI-PDD) #flashcard 
NNG = Nearest Neighbour Graph
MST = Minimum Spanning Tree
RNG = Relative Neighbourhood Graph
GG = Gabriel Graph
DT = Delaunay Triangulation
$NNG \subseteq MST \subseteq RNG \subseteq GG \subseteq DT$
<!--ID: 1691342018934-->



Konstrukce Delaunay triangulation #flashcard 
Three points are each others neighbours if their tangent sphere contains no other points
* dual of Voronoi diagram
* Voronoi editing: retain those points whose neighbours (as defined by the Delaunay Triangulation) are of the opposite class
* expensive for higher dimensions
![[delaunay.png]]
<!--ID: 1691342018937-->



Konstrukce Gabriel graph #flashcard 
Points are neighbours only if their (diametral) sphere of influence is empty
* The Gabriel graph is a subset of the Delaunay Triangulation
* Does not preserve the identical decision boundary, but most changes occur outside the convex hull of the data points
* more efficient than DT
![[gabiel.png]]
<!--ID: 1691342018940-->



Konstrukce Relative Neighbourhood Graph (proximity graph) #flashcard 
Two points are neighbours if the “lune” defined by the intersection of their radial spheres is empty
* The Relative Neighbourhood Graph (RNG) is a subset of the Gabriel graph
* Further reduces the number of neighbours
![[rng.png]]
<!--ID: 1691342018943-->



# Wilsonova editace,  Multi-edit metoda


Popis Wilsonovy editace (1972). Metoda pro redukci dat. #flashcard 
Iteratively removes points that do not agree with the majority of their k nearest neighbours
<!--ID: 1691342018946-->



Multi-edit metoda pro redukci dat #flashcard 
* Repeatedly apply Wilson editing to random partitions
* Classify with the 1-NN rule
1. Diffusion: divide data into N ≥ 3 random subsets
2. Classification: Classify Si using 1-NN with S(i+1)Mod N as the training set (i = 1..N)
3. Editing: Discard all samples incorrectly classified in (2)
4. Confusion: Pool all remaining samples into a new set
5. Termination: If the last I iterations produced no editing then end; otherwise go to (1)
<!--ID: 1691342018950-->




Popis Tomkovy spoje - redukce dat #flashcard 
To remove both noise and borderline examples
Tomek link:
* $E_i, E_j$ belong to different classes, $d(E_i, E_j)$ is the distance between them.
* A $(E_i, E_j)$ pair is called a Tomek link if there is no example $E_\ell$, such that $d(E_i, E_\ell) < d(E_i, E_j)$ or $d(E_j , E_\ell) < d(E_i, E_j)$.
![[tomek.png]]
Na redukci se to pouziva tak, ze odebereme bud Ei, nebo Ej podle toho kdo z nich patri do majoritni tridy. Cisti to prostor kolem decision boundary a odstranuje to noise ve prospech minority.
<!--ID: 1691342018953-->
