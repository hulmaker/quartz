TARGET DECK: FIT-2021-2
FILE TAGS: MVP FIT-2021-2

## Lec 01 - 15.02.2021

popiš Rosenblatt perceptron (1956) #flashcard 
$y = sgn(x^T w + b)$ - skoková aktivační funkce
<!--ID: 1613648556094-->


chain rule - vypocitej $$\frac{\partial (x+y)z}{\partial x}$$ #flashcard 
$f$ se da rozlozit na $f=qz$, tak ze: $q = (x+y)$, neni potreba pocitat vsechno, staci zderivovat jen vyrazy ve kterych je $x$ postupne a ty spolu vynasobit.
$$\frac{\partial f}{\partial q} = z, \frac{\partial q}{\partial x} = 1$$
$$\frac{\partial f}{\partial x} = \frac{\partial f}{\partial q}\frac{\partial q}{\partial x}$$
<!--ID: 1613648556102-->


Definuj konvoluci jako $(f * g)(t)$  #flashcard 
$$(f * g)(t)=\int_{-\infty}^{\infty} f(x) \cdot g(t-x) \mathrm{d} x$$
<!--ID: 1613648556108-->


Co je separable kernel při konvoluci, dej příklad takového kernelu #flashcard 
Kernel je separable, pokud pro jeho vícerozměrnou funkci platí: $G(x, y) = g_{x}(x) \cdot g_{y}(y)$ Potom místo 2d konvoluce můžeme aplikovat 2 1d konvoluce, což je rychlejší. Např. Gaussian kernel.
<!--ID: 1613648556112-->


Co je dropout při trénování NN? #flashcard 
pro každý trénovací bod random vynechej několik (0.5 třeba) neuronů. Můžu  vynechávat i vrstvy atd. Je to levná a rychlá metoda regularizace, předchází výrazně overfittingu - nutí generalizovat, vytváří noise.
<!--ID: 1613648556117-->


Co je gradient? #flashcard
Parciální derivace ztrátové funkce podle vah. Gradient learning - pro každou váhu uděláme krok (learning step) proti směru parciální derivace podle té konkrétní váhy.
<!--ID: 1613648556123-->


Ktitika deep learning a back propagation? #flashcard 
Prone to overfitting, to many parameters, needs good initialization, too few labeled data, computationally intensive. (všechny tyto problémy umíme alespoň částečně překonat.)
<!--ID: 1613648556127-->


Vyjmenuj druhy vrstev v CNN #flashcard 
Konvoluční, max pooling, fully connected
<!--ID: 1613648556132-->


Co je stride, padding, max pooling a jaká operace je mezi filtrem a oknem v konvoluční vrstvě? #flashcard 
**Stride** - o kolik se posune sliding window
**padding** -  doplnění pixelů na okrajích, aby konvoluce nezmenšovala atd.
**max pooling** - sliding window projede obrázek a vybere maximum, stride je typicky jako velikost okna.
operace mezi filtrem a oknem v conv vrstvě - dot product
<!--ID: 1613648556138-->


Vyjmenuj nějaké aktivační funkce #flashcard 
Sigmoida, tanh, ReLU, Leaky ReLU, SeLU, ELU, GeLU
<!--ID: 1613648556143-->


jaká aktivační funkce zmírňuje vanishing gradient problem? #flashcard 
ReLU zmírňuje oproti nelineární sigmoidě.
<!--ID: 1613648556146-->


Co je data augmentation a jaké jsou příklady? #flashcard 
Obrázky jsou zdeformovány, posunuty, zrcadleny atd => vytvoří to víc dat, snižuje overfitting, lépe generalizuje a je invariantní vůči transformaci
<!--ID: 1613648556152-->


Příklady užití CNN #flashcard 
category recognition, category retrieval, similarity search, face recognition, face verification, age/gender estimation
<!--ID: 1613648556157-->


Dej nějaký CNN architektury #flashcard 
AlexNet (2012) - 5 conv vrstev
GoogLeNet (2015) - 22 vrstev
ResNet (2016) - 152 vrstev, residual modules
DenseNet (2017) - dense skip connections, higher acc with less params
MobileNet (2017 Google) - computationally efficient
ShuffleNet (2018) - acc jako AlexNet, ale 13x rychlejší
<!--ID: 1613648556161-->


Co dělá gaussian filter a jak ho aplikuji? #flashcard 
Dělá image smoothing a denoising, trochu rozmaže, aplikuji ho pomocí konvoluce.
<!--ID: 1613648556166-->

## Lec 02 - 22.02.2021

object detection precision metrics (IoU) #flashcard 
ground truth bounding box, estimated bounding box
$$IoU=\frac{\text{area of overlap}}{\text{area of union}} = \frac{GT_{BB} \cap prediction_{BB}}{GT_{BB} \cup prediction_{BB}}$$
<!--ID: 1614014219877-->


Define precision #flashcard 
$$precision = TPR = sensitivity = \frac{TP}{TP+FP}$$
It tells you the ration of how often you are right.
<!--ID: 1614014219882-->


Define recall #flashcard 
$$recall = \frac{TP}{TP+FN}$$
It tells you the ratio of how many positives did you discovered.
<!--ID: 1614014219887-->


Define precision-recall curve #flashcard 
binary classifier (logistic regression) has a decision threshold. By changing the threshold, we tune the recall and precision of the classifier. We can plot the precision-recall curve on 2D plane with x=recall and y=precision.
<!--ID: 1614014219891-->



Define AP - average precision and mAP - mean AP #flashcard 
**AP** - area under the precision-recall $p(r)$ curve $\int_{r} p(r) d r \approx \frac{1}{N} \sum_i{r(i)}$
**mAP** - mean AP over all classes $\frac{1}{C} \sum_{c} \mathrm{AP}_{c}$
<!--ID: 1614014219895-->


Approaches in object detection + drawbacks #flashcard 
Scanning window + CNN,
Region proposals + CNN
<!--ID: 1614014219899-->


Scanning window + CNN algorithm #flashcard 
slow, expensive
1. scan all possible bounding  boxes
2. crop and scale BB
3. run CNN
<!--ID: 1614014219904-->


Region proposals + CNN algorithm #flashcard 
run CNN on region proposals = areas suspected of containing an object
<!--ID: 1614014219907-->


Explain ideas used in Faster R-CNN # flashcard 
2 - refine proposals with regression
3 - RPN + fast R-CNN - shared convolutional features

Region proposals + CNN + Instance segmentation # flashcard 
Mask R-CNN

Examples of CNN architectures with and without region proposals #flashcard 
**Region proposals + CNN**
- R-CNN
- SPP net
- Fast R\-CNN, Faster R\-CNN, Mask R-CNN
**CNN without region proposals**
- R-CNN minus R
- YOLO, YOLO v2, YOLO 9000
- SSD
- RetinaNet
<!--ID: 1614014219912-->


What is the non maximum suppression in the object detection task? #flashcard 
First, you have many overlapping R'sOI, and you want to choose predictioins.
- $X :=$ set of R'sOI
1. select a prediction $p \in X$ with the highest confidence.
2. remove $p$ and all $x \in X$ if $IoU(x, p)$ is **higher** that the threshold.
3. repeat until $X$ is not empty
4. result: set of predictions $p$
<!--ID: 1614014219916-->



YOLO idea + advantages #flashcard 
less fals positives, fast, better generalization, first real time detector
1. Grid over image
	1. each cell predicts $n$ regions of interest
	2. each cell predicts itself a conditional class probability $P(Car \mid Object)$
2. deleting R'sOI with very low confidence
3. Non maximum supression over all ROI
<!--ID: 1614014219919-->


Co je noveho v YOLOv2 a YOLO 900 #flashcard 
batch normalization, higher resolution, finer grid, anchor boxes with k-means
<!--ID: 1614014219923-->


Idea of skip connections and where are they used #flashcard 
ResNet, U-Net, DenseNet
- propagates an information deeper to the network. (some semantic features tend to vanish quickly)
- Prevents the vanishing gradient problem.
	- residual connection: adding outputs y = F(x) + x  (ResNet)
	- concatenated connection - concatenating features to deeper outputs (DenseNet)
<!--ID: 1614014219927-->


Dilated (Atrous) Convolutions #flashcard 
same number of parameters with larger receptive field - convolution filter is distributed to larger area, there is a space between adjoining filter bits.
![[dilated_convolution.png]]
<!--ID: 1614014219931-->


Deep fake principle, architecture # flashcard 
todo nahravka, autoencoders

Adversarial attacks on neural networks #flashcard 
CNN's can be easily fooled - adding adversrial noise/object to the image so that the CNN thinks it is a different object
todo equation
Possible in the real world - glasses, t-shirt, sticker
all networks are vulnurable to these attacks, active research
<!--ID: 1614014219935-->


Generative Adversarial Networks GANs #flashcard 
- random noise -> generator - generates adversarial image
- training set - set of real images
- the discriminator tries to distinguish real (dataset) and fake images (generator)
- the generator and the discriminator compete.
<!--ID: 1614014219939-->


What is a Cycle GAN #flashcard 
A -> B -> A' (day -> night -> day')
Mas 2 generatory (tam a zpet), loss jsou 2 GAN lossy + cycle loss (= L(A, A'))
<!--ID: 1614014219943-->

## Lec 03 - 01.03.2021 - Image correspondence 1

co je to label smoothing v klasifikaci a k čemu je dobrý? #flashcard 
[towardsdatascience](https://towardsdatascience.com/what-is-label-smoothing-108debd7ef06)
Technika co funguje proti overfittingu a overconfidence. Mám k tříd, jen jedna je správně. Neřeknu že je 100% (0, ..., 0, 1, 0, ..., 0), ale přiřadím i nějaké pravděpodobnosti ostatním třídám s tím, že největší má ta správná. 
Př. one-hot smoothing: $(\alpha, ..., \alpha, 1-k\alpha, \alpha, ..., \alpha)$
Potom zabraňuji tomu, aby byl klasifikátor příliš sebevědomý.
<!--ID: 1615588131266-->


co je to batch normalization? #flashcard 
[wiki](https://en.wikipedia.org/wiki/Batch_normalization)
Technika co zrychluje síť, zvyšuje úspěšnost a zajímavé je, že funguje proti gradient explosion, umožňuje mít vyšší lr, regularizuje síť (takže líp generalizuje).
Vliv různých parametrů, jako inicializace vah, náhodnost v datech atd. Ty vlivy způsobují změnu distribuce vstupních dat. Říkají tomu **internal covariate shift**. 
Používá se BN layer, který vstup do layeru normalizuje.
<!--ID: 1615588131272-->


Co je to interpolace a lineární interpolace? #flashcard 
Interpolace (=vylepšit vkládáním) je metoda vhodná pro odhadnutí hodnoty funkce v intervalu, ve kterém máme naměřené jen některé body. Lineární interpolace je aproximace funkční hodnoty mezi dvěma body přímkou, která jimi prochází.
![[interpolation.png]]
<!--ID: 1615588131277-->


Co je occlusion? #flashcard 
Zakrytí. Např. když trackuješ lidi a oni ti mizí za stromem. Algoritmus co je robust to occlusion by se s tím měl vypořádat.
<!--ID: 1615588131281-->


Co je to aliasing? Podmínky aby nevzniknul. #flashcard 
Když jsou samply dvou různých signálů nerozpoznatelné. (vzájmené aliasy) samplovat=diskretizovat. Když vezmu vzorek v bodě, kdy se hodnoty signálů podobají, tak je ze vzorku nerozpoznám. (moire pattern)
![[aliasing.png]]
![[moire_pattern2.png]]
**Nyquist thorem** - Aby nedošlo k aliasingu, musí bt vzorkovací frekvence 2x vyšší, než nejvyšší frekvence harmonických složek ve vzorkovacím signálu.
antialiasing - odfiltrju frekvence vyšší, než Nyquist theorem. Dělá se to pomocí filterů, gaussian blur pomáhá.
<!--ID: 1615588131285-->


Jaké jsou vlastnosti pro local feature? (interest point/patch) v image correspondance? #flashcard 
Invariantní vůči změně pohledu, geometrické transformaci, změně iluminace. Musí být robustní vůči occlusion -> víc local features. Musí být rozpoznatelní od svého okolí.
<!--ID: 1615588131290-->

Co je SLAM v image processing kontextu? #flashcard 
SLAM (simultaneous localization and mapping) - detekuješ svoje okolí a zároveň v něm odhaduješ svojí pozici. Používá se např v autonomnch vozidlech.
<!--ID: 1615680027690-->


Dej příklady corner detectorů #flashcard 
Harris corner detector
FAST corner detector (součást state-of-the-art SLAM v algoritmu ORB)
SUSAN - předchůdce FAST (nebyla naučená ML)
<!--ID: 1615680027695-->



Harris corner detector idea #flashcard 
Mám sliding window a jezdím s ním po obrázku. Detekuju ta místa, která mají velko změnu v hodně směrech.
![[harris_detector-idea.png]] 
<!--ID: 1615588131294-->


Popiš auto correlation function v Harris Detektoru $E\left(x_{0}, y_{0} ; u, v\right)$, kde $x_{0}, y_{0}$ jsou souřadnice a $u, v$ posun. #flashcard 
$$E\left(x_{0}, y_{0} ; u, v\right)=\sum_{(x, y) \in W\left(x_{0}, y_{0}\right)} w(x, y)(I(x, y)-I(x+u, y+v))^{2}$$
$I(x, y)$ - Image
$w(x, y)$ - kernel (konstantní / gauss ...)
$W\left(x_{0}, y_{0}\right)$ - okno s centrem v $\left(x_{0}, y_{0}\right)$
Lidsky = vezmu 2 patche z $I$ (jeden je posunutý). Odečtu je, umocním a udělám dot produkt s kernelem. To sečtu pro všechny posuny. 
Algoritmus pro corner detection s min z auto-correlation function jde i bez sliding window (code) odečtu obrázky pro všechny posuny, udělám gaussian blur a pro každý pixel vyberu ze všech posunů min. hodnotu
![[harris_code.png]]
<!--ID: 1615588131298-->


Harris corner detector optimization #flashcard 
Aby se nemusela počítat auto corelace pro všechny pozice a z nich vybírat minimum, můžeme použít následující alg.
Aproximujeme intensity function v posunu taylorovým polynomem. Pro nás to znamená, že potřebujeme parciální derivace obrázku podle x a y.
$$I(x+u, y+v) \approx I(x, y)+\left[I_{x}(x, y), I_{y}(x, y)\right]\left[\begin{array}{l}u \\ v\end{array}\right]$$
kde $I_{x} a I_{y}$ jsou parciální derivace $I(x, y)$
Nebudeme počítat pro všechny směry, stačí nám jen x a y. Z toho si spočítáme díky vlastním číslům R (corner) response a v ní najdu lokální maximum.
<!--ID: 1615588131302-->


## Lec 04 - 08.03.2021 - Image correspondence 2

Describe the FAST algorithm for corner detection #flashcard 
[opencv](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_feature2d/py_fast/py_fast.html)
We gradually compare intensity change between center and edge of the circle. Then we check if signs between pixels on edge are oposite/equal. Some heuristic tells us if it is a corner.
Je tam pot5eba non-maxima-supression, musíš mít správně velký okno.
<!--ID: 1615680027699-->


Jaká je slabina Harris corner detectoru? Jak se dají řešit? #flashcard 
Detektor není invariantní vůči scale obrázku. Když obrázek zmenším, tak je hrana najednou roh atd.
Řešení - můžu používat různý velikosti okna a tak detekovat různý rohy. Nebo si pro každý obrázek najdu vhodnou velikost okna, což musím udělat pomocí nějaké funkce.
<!--ID: 1615680027703-->


Proč se používají blob detectory? #flashcard 
corner jen měří, jestli je změna intenzity ve dvou ortogonálních směrech. Nedefinuje roh jako bod, ale jako škálu. Blob je škála sama o sobě. 
<!--ID: 1615680027706-->

Definuj Image moment a rekni k cemu je #flashcard 
Vazeny prumer (moment) intenzity pixelu obrazku. Daji se pouzit k odhadu orientace, affini transformace atd.
$$M_{p q}=\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} x^{p} y^{q} f(x, y) d x d y$$
Kdyz beru v uvahu, ze obrazek neni spojity a ze je grayscale a $I(x, y)$ znaci intenzitu v bode $(x, y)$, tak je vzorec nasledujici.
$$M_{i j}=\sum_{x} \sum_{y} x^{i} y^{j} I(x, y)$$
<!--ID: 1615719482968-->


Jak se dělá blob detekce pomocí Hessian detektoru? #flashcard 
Blob je extrém ve funkci obrázku, kt. získám jeho derivací. Chci odhalit sedlové body, tak potřebuju i druhou derivaci. To udělám konvolucí s druhou derivací Gausse nebo Laplace. Pak spočítám determinant Hessovy matice a detekuju následovně.
![[hessian_detector.png]]
<!--ID: 1615680027711-->


Jak získám scale invariant detector? #flashcard 
Vytvořím si gaussian scalespace -> vezmu několik velikostí filtrů pro každý z nich vytvořím kopii obrázku a filtruju.
Na nich hledám lokální maxima a promítám do výsledku.
<!--ID: 1615680027715-->


Describe dominant gradient orientation estimation. #flashcard 
1) Compute first order derivations dx, dy
2) calculate gradient magnitude $\sqrt{dx^2+dy^2}$
3) calculate angles $atan2(dx, dy)$
4) either weight mag with gaussian, or use pixels only in the incircle of the patch (edges of patches may bias the orientation)
5) calculate histogram of angles, but weight them with magnitudes. (instead of adding 1 to bin, add corresponging magnitude value. (so that it represents dominant gradinets))
6) smooth the histogram with the gaussian1d
7) estimated orientation is in argmax(histogram)
<!--ID: 1617270928023-->


Patch orientation estimation methods. #flashcard 
**gradient, derivatives** - Compute image derivatives relative to the dominant direction of gradient. (This is fast if you have already computed derivatives.) Then create a weighted angular histogram of angles (weight is magnitue) and return orientation (hist bin) with hisghest value.
**for FAST features** - Take edvantage of patches gradient. Each patch is a corner. Corners have properties that one fraction is dark and the rest is bright (or contrary). We can calculate center of mass and then estimate the orientation with vecrot from center.
**neural network** - learned orientation regression with CNN (how to train it in next lecture) it might be more robust
<!--ID: 1615719482975-->


Harris/Hessian Affine Detector. #flashcard 
todo refactor
Z porstredka vysles paprsky co zastavis v maximu funkce. Vyextrahujes geometricke momenty a aproximujes patch pomoci elipsy. Ta elipsa by mel byt kruh. Udelas affini transformaci aby to byl kruh. Zkusis vytvorit elipsu znovu a pokud to nebude kruh, tak zase transformujes... 
![[affine_detector.png]]
<!--ID: 1615719482981-->

## Lec 05 - 15.03.2021 - Image correspondence 3


SIFT detector # flashcard 
[opencv tut](https://docs.opencv.org/3.4/da/df5/tutorial_py_sift_intro.html)
[great tutorial](https://aishack.in/tutorials/sift-scale-invariant-feature-transform-features/)
Input is oriented patch with some scale. You need to calculate gradient and magnitues of angles. Then split the patch into nxn matrix. Each window is then converted into an angular histogram of angles weighted by the magnitude. Concatenate histograms , normalize, clamp, again normalize and then you have your SIFT descriptor.
![[SIFT-descriptor.png]]


## Lec 06 - 22.03.2021 - RANSAC
How to train a detector and a descriptor for local features #flashcard 
Train desc and detector at once, use two losses for - repetability (img pairs should be correlated), reliability (score how good the keypoint is)
<!--ID: 1617270928026-->


Describe formula for the repetability loss #flashcard 
cosine similarity + peaky = 
$$\begin{aligned} \mathcal{L}_{r e p}\left(I, I^{\prime}, U\right)=& \mathcal{L}_{c o s i m}\left(I, I^{\prime}, U\right) \\ &+\lambda\left(\mathcal{L}_{\text {peaky }}(I)+\mathcal{L}_{\text {peaky }}\left(I^{\prime}\right)\right) \\ \mathcal{L}_{\text {cosim }}\left(I, I^{\prime}, U\right)=1-\frac{1}{|\mathcal{P}|} \sum_{p \in \mathcal{P}} \operatorname{cosim}\left(S[p], \boldsymbol{S}_{U}^{\prime}[p]\right) \\ \mathcal{L}_{\text {peaky }}(I)=1-\frac{1}{|\mathcal{P}|} \sum_{p \in \mathcal{P}}\left(\max _{(i, j) \in p} \boldsymbol{S}_{i j}-\operatorname{mean}_{(i, j) \in p} \boldsymbol{S}_{i j}\right) \end{aligned}$$
<!--ID: 1617270928030-->


Popiš co můžeme použít jako reliability loss #flashcard 
triplett loss, nebo average precision loss
$\mathcal{L}_{A P \kappa}(i, j)=1-\left[A P(i, j) \boldsymbol{R}_{i j}+\kappa\left(1-\boldsymbol{R}_{i j}\right)\right]$
<!--ID: 1617270928034-->


SuperPoint learned local feature detector #flashcard 
1) Supervised training on synthetic dataset
	- we know what good keypoints are (corner, blob etc...) so we can create or generate a synthetic ds
2) fine-tune the detector on real world by augmentation
Fast and reliable (not good for big occlusion and deformation, but it works well for real world somehow), Not great for 3D reconstruction, but suitable for SLAM. (fast and robust)
<!--ID: 1617270928037-->


When do we want to use the RANSAC algorithm #flashcard 
for example line fitting problem when we have a lot of outliers -> least squares method would not work becouse of them.
<!--ID: 1617270928041-->


Define manifold #flashcard 
**manifold** is a [topological space](https://en.wikipedia.org/wiki/Topological_space "Topological space") that locally resembles [Euclidean space](https://en.wikipedia.org/wiki/Euclidean_space "Euclidean space") near each point. More precisely, an n\-dimensional manifold, or _n\-manifold_ for short, is a topological space with the property that each point has a [neighborhood](https://en.wikipedia.org/wiki/Neighbourhood_(mathematics) "Neighbourhood (mathematics)") that is [homeomorphic](https://en.wikipedia.org/wiki/Homeomorphic "Homeomorphic") to the Euclidean space of dimension n.
One-dimensional manifolds include [lines](https://en.wikipedia.org/wiki/Line_(geometry) "Line (geometry)") and [circles](https://en.wikipedia.org/wiki/Circle "Circle"), but not [figure eights](https://en.wikipedia.org/wiki/Lemniscate "Lemniscate") (because no neighborhood of their crossing point is homeomorphic to Euclidean 1-space). Twodimensional manifolds are also called [surfaces](https://en.wikipedia.org/wiki/Surface_(topology) "Surface (topology)"). Examples include the [plane](https://en.wikipedia.org/wiki/Plane_(geometry) "Plane (geometry)"), the [sphere](https://en.wikipedia.org/wiki/Sphere "Sphere"), and the [torus](https://en.wikipedia.org/wiki/Torus "Torus"), which can all be [embedded](https://en.wikipedia.org/wiki/Embedding "Embedding") (formed without self-intersections) in three dimensional real space
<!--ID: 1617270928045-->



Describe a RANSAC error function #flashcard 
![[ransac_error.png]]
<!--ID: 1617270928048-->


Describe q principle of the RANSAC algorithm #flashcard 
```python
"""
Input:
	X: data points
	e(S) = theta: estimated model parameters
	f(x, theta): error function
	eta: required confidence, from <0, 1>
Output: theta - parameters that minimize the cost function
"""
satisfied = False
i = 0
while not satisfied:
	S = Select_random_from(X, m) 			# m = sample size = |S|
	theta = e(S) 							# estimate parameters
	L[theta] = sum([f(x, theta) for x in X])# loss
	if L[theta] < L[best_theta]:  			# so-far-the-best
		best_theta = theta
	satisfied = P(better solution exists) < 1-eta
return theta
```
<!--ID: 1617270928053-->


Describe the stopping criterion of the RANSAC algorithm #flashcard 
$P(better\ solution\ exists) < 1 - \eta$
$\varepsilon = Q/N$ - number of inliers/N -> inlier ratio. So far the best model is a lower bound for the $\varepsilon$
$P(bad\ model\ k\ times) = (1-P(inlier\ sample))^k < 1-\eta$ - k is the iteration number
if $k \geq log(1-\eta) / log(1-\varepsilon^m)$ -> we found solution with confidence $\eta$
<!--ID: 1617270928057-->

## Lec 11  - 26.04.2021 - KLT

Define tracking #flashcard 
many different definitions
 * Tracking is the problem of generation an inference about the motion of an object given a sequence of images.
 * given an initial estimate of its position, locate X in a sequence of images
<!--ID: 1632748827474-->


Application domains of visual tracking #flashcard 
monitoring: assistence, surveillance, 
robotics: autonomous car driving, 
measurements: sports, meteorology, medicine
human computer interaction
augmented reality
movies: motion capture, editing
action and activity recognition, image stabilization, emotion analysis
<!--ID: 1632748827478-->


Popiš tracking jako correspondence a jako segmentation #flashcard 
**Correspondence search**: Pro každý obrázek najdi point-to-point correspondences pro pixely nějaké sledované entity.
**Segmentation**: označ pixely co patří sledovanému objektu v každém obrázku ze sekvence
<!--ID: 1632748827482-->


Rozdíl mezi short term a long term tracking #flashcard 
**Short tearm tracking** nepočítá s tím, že objekt zmizí z obrazu, bude kompletně překryt atd. Určuje polohu objektu v každém framu -> short term tracking nakonec vždycky selže
**Long term tracking** počítá s tím, že se objekt může ztratit, určí polohu ve framech, kde je objekt vidět - learn object model a reidentifikuj
<!--ID: 1632748827486-->


Kdy u object tracking potrebujes correspondence, kdy segmentation a kdy oboji? #flashcard 
segmentation se hodi pro surveillance a editing ve filmove produkci
correspondence pro image stabilization, augmented reality, human-computer interaction ...
Oboji najednou se hodi pro autonomni vozidla, robotiku, index search, activity recognition, medicine, meteorology ...
<!--ID: 1632748827491-->


Pokud jde ve videu z jednoho obrazku zjistit rychlost pohybujiciho se objektu, řekni jak. #flashcard 
Jop, jde - podle rozmazání. Záleží na rychlosti záklopky, ale většinou je shutter speed stejna jako FPS
<!--ID: 1632748827495-->


Příklad: Mám skleničku. Je dokonale průhledná. Jsou vidět možná nějaký jemný obrysy. Jak jí budu trackovat jeji pohyb? #flashcard 
Budu trackovat pohyb objektů co skleničkou hýbají. Např. ruku člověka atd. Když děláme object tracking, tak je často hodně výhodné trackovat i objekty co nepotřebujeme, jelikož podle toho můžeme řešit dost vedlejších efektů. Např. trackujeme objekt co není vidět. Ten je ale vysoce korelovaný s nějakým, co vidět je. Třeba hadr na tyči. Nevidíme hadr, ale podle tyče poznáme kde je.
<!--ID: 1632748827499-->


Popiš ztrátovou funkci pro KLT tracking #flashcard 
$\hat{d} = \arg \min _d \sum_{p \in R(x)} |I_{t+1}(p+d) - I_t(p)|^2$, kde $t$ je čas, $R(x)$ je funkce, co vráti bbox (nebo nějakou množinu pixelů) pro pixel $x$, funkce $I$ je intenzita a konečně $d$ je vektor posunutí.
<!--ID: 1632748827504-->


Jak se da kontrolovat kvalita v KLT trackingu? #flashcard 
Dá se hledat posun buď z obrázku $img_k-1$ na obrázek $img_{k}$, nebo z prvotního obrázku $img_0$ na obrázek $img_k$.
První varianta může vytvořit posun a chyba se umocňuje časem, druhá varianta může dávat špatný matching = objekt se hodně změní v mezičase.
Nejčastěji se to kombinuje a kontroluje se kvalita nějakým hybridem.
<!--ID: 1632748827509-->


Co za trik se používá v KLT abychom odhadli směr $d$ pomocí OLS a ne bruteforce? #flashcard 
$I_{t+1}(p+d)$ ve ztrátové funkci nahradím taylorovým polynomem prvního stupně a úlohu tak mohu formulovat jako OLS. Pro větší dosah použiji image pyramid (různý scale obrázků)
<!--ID: 1632748827513-->
