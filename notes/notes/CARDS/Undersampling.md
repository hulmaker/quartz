---
tags:
  - on/ai
  - on/statistics
  - note/tidy
  - on/DS
---

[[Oversampling]]
[[NI-PDD]], [[NI-ZI-04]]

Máme nevybalancovaný dataset, hrozí overfitting. Můžeme použít tyto metody.
* **under sampling** - odeberu nějaké datové body z dominantních tříd
* **over sampling** - dogeneruju data do malých tříd - obecně lepší než undersampling.

## Selektivní algoritmy
**Selektivní algoritmy** (vybírají v datech vhodné prvky, ostatní zahazují)
- Všechny metody jako (CNN, editing, proximity graphs)
- RNN - výstup z CNN je dále redukován (iteračně zkouší odebrat prvek po prvku a následně je do vybrané podmnožiny vrací na základě zhoršení/zlepšení kvality predikce)
- DROP3 - postupné odebírání prvků, pokud jejich smazání nemění/neovlivní klasifikaci


## Adaptivní algoritmy
**Adaptivní algoritmy** (proaktivně vytváří nové prvky, kterými nahrazuje ty původní)
- Prototype - spojuje páry bodů, které jsou k sobě nejblíže (a patří do stejné třídy) tím, že je “zmerguje” a výsledný 1 bod bude v prostoru mezi původními 2 body
Chenův algoritmus - umožňuje nastavit požadovanou velikost výsledné podmnožiny, nové body jsou těžiště originálních dat (shluků dat)

## Tomek Links
Najdem tomkovy spoje a odstraníme z nich body z majoritní třídy
![[Tomek Links#Tomek Links]]

## Condensing Methods
### Condensed Nearest Neighbour (CNN)
Aim is to reduce the number of training samples
Retain only the samples that are needed to define the decision boundary
Brute force version in $\mathcal{O}(n^3)$.
1. Initialize subset with a single training example
2. Classify all remaining samples using the subset, and transfer any incorrectly classified samples to the subset
3. Return to 2 until no transfers occurred or the subset is full

### Reduced Nearest Neighbour
Remove a sample if doing so does not cause any incorrect classifications

### Proximity Graphs
![[Proximity Graphs]]

## Editing
### Wilson Editing (1972)
Iteratively removes points that do not agree with the majority of their k nearest neighbours

### Multi-Edit method
Multi-edit metoda pro redukci dat
* Repeatedly apply [[Undersampling#Wilson Editing (1972)|Wilson Editing]] to random partitions
* Classify with the 1-NN rule
1. Diffusion: divide data into N ≥ 3 random subsets
2. Classification: Classify Si using 1-NN with S(i+1)Mod N as the training set (i = 1..N)
3. Editing: Discard all samples incorrectly classified in (2)
4. Confusion: Pool all remaining samples into a new set
5. Termination: If the last I iterations produced no editing then end; otherwise go to (1)

## Neighbourhood Cleansing Rule (NCR)
Třídy V (velká), M (malá), bod b, 3 neighbors. Odstraň $b$, pokud je z V a sousedi ho přehlasují. Odstraň sousedy, pokud jsou z V a b je z M.

## Extended Nearest Neighbour
odebere jakýkoli bod, jehož třída se liší od třídy alespoň 2 ze 3 jeho NN

## IB3
podobný přístup jako [[Undersampling#Condensed Nearest Neighbour (CNN) | CNN]], ale vybírá prvky na základě statistického testování, povoluje porušení 100% klasifikace
Odstraní špatně klasifikované body.