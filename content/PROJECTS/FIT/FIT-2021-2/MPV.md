# Metody Počítačového Vidění

anki flashcards: [[MPV_anki]]

course links: [lectures](https://cw.fel.cvut.cz/wiki/courses/mpv/start),  [labs](https://cw.fel.cvut.cz/wiki/courses/mpv/labs/start)

## Lec 01 - 15.02.2021 - Introduction
### summary
Principy spojené s metodami počítačového vidění. Ukazovaly se různé úlohy, k čemu se používají konvoluční neuronové sítě, konvoluce, jaké architektury se používají a trendy ve vývoji nových architektur.

## Lab 01 - 17.02.2021 - Deep learning 1
nějaký laby se nahrávají automaticky, některý manuálně - jsou tam nějaký úkoly

python pouziva by default cpu, je dobre pouzivat pytorch protoze pouziva GPU
gitlab link - assignmenty, navod na condu, verze 3.6


## Lec 02 - 22.02.2021 - Deep learning 2
[Jak najit spravny lr](https://towardsdatascience.com/estimating-optimal-learning-rate-for-a-deep-neural-network-ce32f2556ce0)
Zeptal jsem se ho jake jsou triky pro tak vysoke acc. Mel jsem 0.87 a top byl 0.94

Hi,
Dropout and BatchNorm work together just fine -- you only need to not place them one after another, especially, BN after dropout. 

AdamW is a good choice. 

One of the keys of the reference submission is dropout before the last layer (clf).

Some of the additional tricks: 
- using Mish activation [link](https://arxiv.org/abs/1908.08681) 
- using 1-cycle policy (although cosine annealing is good as well)
- too much of augmentation (e.g. color) might be bad 
- MaxBlurPool for feature subsampling is good [link](https://kornia.readthedocs.io/en/latest/_modules/kornia/contrib/max_blur_pool.html)
- Test-time augmentation (crops + horizontal padding)


## Lec 03 - 01.03.2021 - Image correspondence 1

**local correspondence** - does not provide semantic correspondence, it only returns local correspondence - same object

3D reconstruction - city reconstruction with google images, flying drone - fast, less precise

panorama stitching - finding correspondances and then blending

imgage retrieval - mam obrazek a reknu najdi mi podobne obrazky, jde to udelat tak, ze hledam correspondences a podle toho jak to sedi to vratit

### summary
Predstavili jsme si problem image correspondance, jeho pipeline a aplikace. Potom keypoint (local feature) detekci pomoc9 Harris corner detektoru. Popsali si vlastnosti local feature a jak funguje Harris detektor.

## Lec 04 - 08.03.2021 - Image correspondence 2
[feature detection and description tut on opencv](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_feature2d/py_table_of_contents_feature2d/py_table_of_contents_feature2d.html)

### summary
Pokracovani v rozebirani detektoru a ruznych algoritmu. Hlavni bod prednasky byla scale, rotation detekce a na ni jsme si ukazovali nejake experimenty. Nakonec detekce a odstraneni affini transformace.

tut RANSAC
there is no match - asi tim mysli ze je treba vic sousedu? atd

## Lec 05 - 15.03.2021 - Image correspondence 3

## Lec 06 - RANSAC
### summary
Vysvetloval nam metody trenovani lokalnich descriptoru. Potom nam byla predstavena hlavni myslenka RANSAC - iterativni algoritmus co zkousi ruzne samply. Ty prolozi primkou a zmeri loss (zanedbava body co jsou dal, nez threshold). Kdyz je splneny zastavovaci criterion, vraci best fit.

## Filip poznamky
* correspondencies -> correspondences/correspondants
* ransac affine - nepochopil bych z toho vubec jak mam hledat affine matrix, neni tam 
* dobry popis toho, co vlastne ty geometries obsahuji a jak je interpretovat