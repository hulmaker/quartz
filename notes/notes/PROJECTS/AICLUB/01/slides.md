	%%
V comment bloku je vzdycky nejake vysvetleni ke slidu co tim chtel basnik rici

ANNOTATION:
V posledních měsících se stále častěji skloňují pojmy jako strojové učení a umělá inteligence. Jsou obaleny někdy až magickou aurou, a to díky úžasným pokrokům velkých jazykových modelů a generátorů obrázků. Chytré systémy ovšem hýbají světem mnohem déle, například v oblastech jako je robotika, automotive, zdravotnictví, zemědělství či doporučování obsahu. Běžný člověk tedy s AI přichází do kontaktu denně, téměř bez povšimnutí. Pojďme tento fascinující svět otevřít, pojďme se učit a diskutovat. V první části úvodního setkání si nejdříve představíme základní pojmy data science, hlavní směry a paradigmata. V druhé části otevřeme libovolnou diskuzi. Nakonec si naplánujeme obsah a formu následujících událostí.

%%

# AI Club 01 - Data Science
## 08.04.2024

* 60min talk + 60min debate
* Next session in 2 months
* You decide on a next topic #TODO slido na posledni slide a sem! (muzes si to vytisknout a nekam nalepit)
* Any of the concepts I introduce today can be a next topic! Simply pick a keyword

Today's topic: 

---
![[personal card]]

---
%%
Club je pojemnovan populisticky AI. Jazyk se sice posunuje, ale pro jistotu si pojdme ujasnit pojmy. Lide je pouzivaji AI a ML interchangebly, ale DL stabilne
%%

# AI vs. ML vs. DL
![[AIMLDL.excalidraw|1000]]

---

# Machine Learning paradigms
%% Rozdeleni domeny machine learning na nekolik kategorii podle pristupu %%
Let us consider a target variable $Y$ and a vector of features (inputs) $X$.  Our goal is to replicate $g: X \to Y$ 

* **Supervised learning**: $Y$ is known (*object detection, pattern recognition*)
* **Unsupervised learning**: $Y$ is unknown (*imagine pictures, data clustering*)
* **Semi-supervised learning**: Some $y \in Y$ are known, some are unknown.
* **Self-supervised learning**: Automatically generating labels to transform unsupervised problem into supervised ones.
* **Reinforcement learning**: An agent takes actions in an environment to accumulate reward.

%%
TODO: examples
%%

---
# Machine Learning Infographics
%% Rozhoduju se co pouziju na zacatku projektu %%

![[machine-learning-infographic.jpg]]

---

%%
Pojdme si nejdrive popsat cely standartni model pro applikovanou data science, zacina porozumenim domeny, konci deploymentem
%%
# Data Science Life Cycle

* **K**nowledge **D**iscovery and **D**ata **M**ining (KDDM process)
* **CR**oss **I**ndustry **S**tandard **P**rocess for **D**ata **M**ining (CRISP-DM 1996)
* CRISP-DM is the most popular KDDM process model across industry.

![[CRISP-DM.excalidraw|400]]

---

# CRISP-DM
%%
Podrobnejsi rozebrani jednotlivych kroku.
%%
![[CRISP-DM_DETAIL.excalidraw|1000]]

---
# Relative effort spent on specific steps in the KDDM process
%% data jsou king, jde jen o data, delejte dobre data science %%
* **Half** of the project effort is spent on **data** preparation.
* Applied machine learning is more about **data** than the modeling.
* Everything else is secondary to your **data**.

Kurgan, Lukasz & Musilek, Petr. (2006).
![[KDDMeffort.png|600]]

---
# Types of Data

numerical, categorical, time-series, text, visual data
nominal, ordinal, discrete, continuous

Uvod
Definice machine learning
Přehled technologií podle typu dat, pro každou kategorii si pšiprav příklad z praxe, jaká firma to dělá a co to umí.
* supervised learning, unsupervised learning, semi-supervised learning, reinforcement learning
* Tabulková data
* Obrazová data
* textová data
* data bez labelů - clustering
* datové řady
* reccomenders
* generative modeling
* autonomní robotika
Záver - shrnutí

---

Témata:
* Předzpracování dat
* problémy v datech
* data reduction - sample based
* data reduction - dimensionality reduction
* jednotlivé metody modelování
* anomally detection

# Anketa
* S jakymi daty nejcasteji pracuji
* Dej 3-5 temat o kterych chces slyset. serad je podle preferenci, to co chces nejvice dej prvni
* V jake domene se nejcasteji pohybuji? Supervised, unsupervised atd.
* Did the event meet your expectations?
* What would you highlight as particularly good?
* What would you improve or change about the event next time?
* Is there anything else you would like to tell us? Here is the space for it.

> [!note]
> Please write me a feedback at Slido!


priprav si nejaka temata pro pripad ze by se nikomu nechtelo moc mluvit

%%
priklady, data
Na zaklade prikladu si budou hledat jak to napojit na jejich data

Senzory, mereni, spektra, opakujici
elektricka mereni, bunky, vizualni data
konfokalni mikroskop

unspersid learning - [mnist](https://divamgupta.com/assets/images/posts/deep_cluster/teaser.png)

anomaly detectioin - jak tabulkova data, tak autonomni auta

na konci mit prikklady uloh



Training data is in the form of a set of pairs {(𝑥(1),𝑦(1)),…,(𝑥(𝑛),𝑦(𝑛))} where 𝑥(𝑖) represents an object to be classified, most typically a 𝑑-dimensional vector of real and/or discrete values, and 𝑦(𝑖) is an element of a discrete set of values. The 𝑦 values are sometimes called _target values_.

%%