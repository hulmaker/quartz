TARGET DECK: NI-SPOL-2023::NI-KOP
FILE TAGS: NI-SPOL-2023 NI-SPOL-14 NI-KOP

prev::[[NI-SPOL-13]]
next::[[NI-SPOL-15]]

# Princip genetických algoritmů, význam selekčního tlaku pro jejich funkci.


Jaké máme základní pojmy v kontextu genetických algoritmů? #flashcard 
* Jedinec (fenotyp) – konfigurace
* genetická reprezentace jedince (genotyp) – kódování konfigurace
	* binární řetěz
	* vektor proměnných
* gen – proměnná kódování (obsahuje alelu)
* alela – hodnota proměnné
* generace, populace – aktuální množina konfiguraci
* mutace – unární operátor
* křížení – binarni operátor
* fitness – optimalizační kritérium
* degenerace – rozšíření konfigurace uvázlé v lokálním minimu
* konvergence – rozšíření kvalitní konfigurace
* biodiverzita – diverzita populace (jak moc se od sebe jedinci liší)
	* vysoká – mnoho stavových prostorů je prozkoumáváno zároveň
	* nízka – degenerace populace, jedinci jsou téměř totožní
<!--ID: 1691578042113-->




Popište v bodech princip genetického algoritmu. #flashcard 
1. Na začátku inicializujeme úvodní populaci
2. Vybereme nejzdatnější jedince
3. Ty křížíme mezi sebou
4. Provedeme mutaci
5. Výslední jedinci tvoří novou generaci, na kterou v další iteraci opět aplikujeme operátory
![[evoluce.png]]
<!--ID: 1691578042115-->



Jaké známe typy simulované evoluce? #flashcard 
* Genetické algoritmy – pracují nad binárním řetězcem, hledají obecně ideální konfiguraci
* Genetické programování – pracuje nad rozkladovým stromem výrazu, hledá ideální vzorec
* Evoluční programování – pracuje nad automatem, sestavuje ideální program
* Evoluční strategie – pracuje nad vektorem reálných čísel
<!--ID: 1691578042116-->



Jaké omezující podmínky zavádíme při křížení a mutaci pro nevalidní řešení v kontextu simulované evoluce? #flashcard 
* Relaxace – penalizace zdatnosti
	* špatné řešení musí být lepší než nevalidní jedinci
* Trest smrti – zahodíme neplatné řešení 
	* Dost radikální (omezení stavového prostoru, neplatné řešení může být mezikrokem k validnímu a lepšímu řešení)
* Doménové operátory – mutaci a křížení volíme tak, aby vždy vyšlo validní řešení
	* Někdy dobré řešení, ale může být těžké takové operátory vyrobit.
* Dekodéry – volíme reprezentaci tak, aby každý možný genotyp odpovídal nějakému řešení (stavový prostor má jen validní stavy)
<!--ID: 1691578042117-->



Jaké jsou možná opatření proti uváznutí v lokálním minimu v kontextu genetických algoritmů? #flashcard 
* Adaptivní mutace – dočasně zvýšíme pravděpodobnost mutace 
	* Zvýšíme tak diverzifikaci populace a vytvoříme šum
* Operátor Katastrofy – zahodíme většinu populace a doplníme ji náhodnými jedinci
	* Můžeme buď ponechat jen nejlepší jedince nebo můžeme ponechat jedince, kteří se od sebe výrazně liší
* Generování náhodných potomků – místo křížení vygenerujeme náhodného jedince.
* Restarty - spustíme algoritmus s jinou počáteční konfigurací a budeme doufat že nedegeneruje
<!--ID: 1691578042119-->



Jaký vliv má velký/malý selekční tlak na průběh genetického algorimu? #flashcard 
Selekční tlak: Pravděpodobnost výběru nejlepšího jedince.
* Velký selekční tlak – nebezpečí degenerace populace (rychlé snížení diverzity)
* Malý selekční tlak – nebezpečí pomalé konvergence (pomalé snižování diverzity)
* Při malém selekčním tlaku může šum vzniklý mutací převážit nad pomalou konvergencí a může dojít k divergenci
* Regulace selekčního tlaku se musí zvolit podle výběrového mechanismu
<!--ID: 1691578042120-->



Jaké mechanismy výběru (selekce) pro genetické algoritmy znáš? #flashcard 
Ruleta: Každý jedinec má výseč kruhu úměrnou jeho zdatnosti.
* možnost opakovaného vybrání, špatné škálování vede k degeneraci
* Linear scale: fitness lineárně transformujeme a zmenšíme tak rozdíl mezi silnými/slabými
* Ranking: Místo zdatnosti použijeme pořadí.
Tournament (turnaj): Z náhodného výběru m jedinců jde do další populace k nejlepších jedinců.
Zkrácený výběr: Vem m nejlepších jedinců z celé populace (velmi vysoký selekční tlak)
* Proto je dobré rozdělit populaci na několik skupin podle zdatnosti (typicky 4) a z každé vzít m/4 jedinců.
<!--ID: 1691578042121-->



Jaké znáš typy křížení pro genetický algoritmus? #flashcard 
Jednobodové: náhodně vybereme pozici uvnitř binárního vektoru
* hodnoty před hranicí zdědí z jednoho rodiče, hodnoty za hranicí z druhého
Dvoubodové: obdobně jako u Jednobodového křížení, ale vybereme dvě pozice
Uniformní: každý bit binárního vektoru vybereme náhodně z jednoho nebo druhého rodiče
<!--ID: 1691578042123-->



Co je to mutace u genetického algoritmu a k čemu je dobrá? #flashcard 
Zvyšuje diverzitu, vnáší šum, vyrovnává ztrátu informace způsobenou selekcí
Náhodně překlápí bity a tím prohledává blízké okolí jedinců.
Pomáhá se dostat z lokálního minima, zabraňuje předčasné konvergenci.
Snadno degraduje, pravděpodobnost mutace je třeba procento.
<!--ID: 1691578042124-->



Jak genetické algoritmy postaví novou populaci? #flashcard 
Aplikací operátorů: křížení, mutace nahradíme částečně/úplně starou generaci
Elitismus: ponecháme nejlepší jedince a pak nějak pošmelíme zbytek. Je potřeba si dát pozor na degeneraci.
<!--ID: 1691578042125-->
