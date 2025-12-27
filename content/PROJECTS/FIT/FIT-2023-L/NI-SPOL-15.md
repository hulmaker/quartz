TARGET DECK: NI-SPOL-2023::NI-KOP
FILE TAGS: NI-SPOL-2023 NI-SPOL-15 NI-KOP

prev::[[NI-SPOL-14]]
next::[[NI-SPOL-16]]

# Princip simulovaného ochlazování, význam parametrů a způsoby jejich řízení

Popište princip simulovaného ochlazování #flashcard 
Lokální heuristické metoda pro prohledávání stavového prostoru. Je to pravděpodobnostní optimalizační metoda.
Jedná se o analogii ochlazování taveniny. Na začátku se diverzifikuje a pak postupně intenzifikuje.
Teplota má vliv na přijímání zhoršujících akcí a také může ovlivnit velikost kroku
Řeší tak uváznutí v lokálním minimu, což je dále řešeno i restarty.
```python
def simulated_annealing(s0, k_max):
	s = s0
	for k in range(k_max):
		T = temperature(1-(k+1)/k_max)
		s_new = random_neighbor(s)
		delta = E(s_new)-E(s)
		if random() < exp(-delta/T):
			s = s_new
	return s
```
`E()` je energy function - vyhodnocuje kvalitu řešení, `P()` je pravděpodobnost přijetí (typicky podíl u zhoršující akce), ochlazování je pak typicky naškálovaná exponenciální distribuce.
<!--ID: 1691966314107-->



Jaké ukončovací podmínky lze implementovat v algoritmu simulovaného ochlazování? #flashcard 
* Maximální počet kroků
* koncová teplota
* max. počet změn
* max. počet přijatých zlepšujících řešení
Okolo lokálního minima se sníží počet přijímaných zlepšujících řešení. Proto musíme chvíli počkat.
Dokud se zlepšujeme, nemá smysl končit.
<!--ID: 1691966314108-->



Jaké omezující podmínky lze zavést pro algoritmus simulovaného ochlazování? #flashcard 
* pouze validní stavy (možnost nenalezení lok. min)
* relaxace -> nevalidní stavy penalizujeme (lepší průchod stavovým prostorem)
	* Nevalidní řešení má nižší fitness
	* Dobrá nevalidní řešení můžou mít lepší fitness, než špatná validní
<!--ID: 1691966314109-->



Jak lze provádět lazení parametrů pro simulované ochlazování? #flashcard 
whitebox/blackbox e.g. trénovací, testovací sada
Je dobré si udělat graf ceny řešení v průběhu: z něj lze poznat zda máme dost vysokou teplotu
<!--ID: 1691966314110-->



Jaké jsou parametry simulovaného ochlazování? #flashcard 
Počáteční teplota: ladí se na základě běhů. Vysoká přijímá velká zhoršení, nízká uvázne v lok. min.
Koncová teplota: Vysoká uvázne v lok. min. protože dost neexplorovala, ale asi ani neintenzifikovala. Nízká zbytečně dlouho chodí po lok. min.
Koeficient ochlazování a ekvilibrium: 0.8-0.999, ekvilibrium lze řídit na základě jeho délky. Vysoká délka: dlouhý výpočet bez zlepšení, Nízká délka: uváznutí, málo explorace
<!--ID: 1691966314111-->
