TARGET DECK: NI-ZI-2023::NI-SCR
FILE TAGS: NI-ZI-2023 NI-ZI-22 NI-SCR

prev::[[NI-ZI-21]]
next::[[NI-ZI-22]]

Smíšené modely ARIMA: základní vlastnosti modelů/procesů, integrování a diferencování. Zápis ARIMA, včetně zápisu pomocí operátorů zpoždění a diference, speciální případy podle hodnot p, d, q. Problém redundance parametrů.


Za jakých podmínek je lepší použít model ARIMA oproti ARMA? #flashcard 
Základní předpoklad ARMA modelu je slabá stacionarita časové řady. Pokud je tento předpoklad porušen, máme několik  řešení:
1. Odstranit trend, tj. rozložit časovou řadu na trend + zbytek a trend odečíst. Trend můžeme hledat interpolací řady polynomem odpovídajícího řádu.
3. Použít metodu diferencí, tj. vytvořit z řady $\{X_t; t=1,2,\ldots\}$ řadu $\{X_{t}'; t=1,2,\ldots\}$ následovně:
$$
X_{t}' = X_{t} - X_{t-1}, \qquad t = 1,2,\ldots
$$
Diferencování za nás právě obstará ARIMA.
<!--ID: 1692886189362-->



Definice modelu ARIMA(p, d, q) #flashcard 
$$
X_{t}=c+\phi_{1} X_{t-1}'+\ldots+\phi_{p} X_{t-p}'+\theta_1 \varepsilon_{t-1}+\cdots+\theta_q \varepsilon_{t-q}+\varepsilon_t
$$
Kde $\phi_i$ jsou parametry AR části, $\theta_j$ jsou parametry MA části a $X_{t-i}'$ je prvek příslušející d-krát diferencované časové řadě.
<!--ID: 1692886189367-->



Definice modelu ARIMA(p, d, q) za pomoci operátoru zpoždění #flashcard 
$$
{\Phi}(1-B)^d X_t = \Theta \varepsilon_t, \qquad\text{kde}\qquad
\Phi=1-\sum_{i=1}^p \phi_i B^i \quad\text{a}\quad
\Theta = 1+\sum_{i=1}^q \theta_i B^i,
$$
popřípadě s konstantou $c$
$$
\Phi (1-B)^d X_t = c + \Theta \varepsilon_t.
$$
<!--ID: 1692886189372-->



Dejte příklady nějakých běžných ARIMA modelů #flashcard 
- ARIMA(0,0,0)+c - konstantní model
- ARIMA(0,1,0) - model náhodné procházky
- ARIMA(0,1,0)+c - náhodná procházka s driftem
- ARIMA(1,0,0)+c - AR(1) model
- ARIMA(2,0,0)+c - AR(2) model
- ARIMA(1,1,0)+c - AR(1) model na jednou diferencovaných datech
- ARIMA(2,1,0)+c - AR(2) model na jednou diferencovaných datech
- ARIMA(0,1,1) - jednoduché exponenciální vyhlazování - MA(1) model na diferencovaných datech
- ARIMA(0,1,1)+c - jednoduché exponenciální vyhlazování - MA(1) na diferencovaných datech - s konst. lin. trendem
- ARIMA(1,1,2) - lineární exponenciální vyhlazování s tlumeným trendem
- ARIMA(0,2,2) - zobecněné lineární exponenciální vyhlazování
<!--ID: 1692886189376-->



Problém redundance parametrů v kontextu modelování časových řad #flashcard 
AR a MA části modelu pracují i proti sobě - zvýšíme-li řády u obou, mohou se navzájem vyrušit. Příklad: model ARMA(1,2) ve tvaru: $X_t = \phi X_{t-1} + \varepsilon_t + \theta_1\varepsilon_{t-1} + \theta_2\varepsilon_{t-2}$
minulá hodnota: $X_{t-1} = \phi X_{t-2} + \varepsilon_{t-1} + \theta_1\varepsilon_{t-2} + \theta_2\varepsilon_{t-3}$
Vynásobme $X_{t-1}$ konstantou $c \neq 0$: $cX_{t-1} = c\phi X_{t-2} + c\varepsilon_{t-1} + c\theta_1\varepsilon_{t-2} + c\theta_2\varepsilon_{t-3}$
odečtěme od $X_t$: 
$$
X_t = (\phi+c) X_{t-1} -c\phi X_{t-2} + \varepsilon_t + (\theta_1-c)\varepsilon_{t-1} + (\theta_2 -c\theta_1)\varepsilon_{t-2} - c\theta_2\varepsilon_{t-3}
$$
což je ARMA(2,3)! A zjevně nejsou parametry jednoznačně určené, neboť $c$ je libovolné. V "backshift" notaci uvedené níže to znamená, že je-li $\phi B X_t = \theta B \varepsilon_t$ odpovídající model procesu, potom je jím i $(1-cB)\phi B X_t = (1-cB) \theta B \varepsilon_t$ pro libovolnou konstantu $c$. Jednoznačnou parametrizaci dostaneme pokrácením všech společných faktorů v AR a MA charakteristických rovnicích - to už jsme ale za hranicí MI-SCR.
<!--ID: 1692886189380-->



Příklad redundance parametrů u ARMA(1, 1), kdy je proces ve skutečnosti bílý šum #flashcard 
Uvažujme bílý šum pro všechna $t$, tj. pro dva konsekutivní libovolné časové okamžiky
$$
\begin{aligned}
X_t &= \varepsilon_t \\
X_{t-1} &= \varepsilon_{t-1}.
\end{aligned}
$$
Vynásobme druhou rovnici 0.5 a převeďme na jednu stranu $0 = -0.5 X_{t-1} + 0.5 \varepsilon_{t-1}$
a jelikož jde o nulu (aspoň ve střední hodnotě), sečtěme to s první rovnicí:
$$
X_t = -0.5 X_{t-1} + \varepsilon_t + 0.5 \varepsilon_{t-1}.
$$
Vidíme, že bílý šum je ekvivalentní k nějakému ARMA(1,1). Přesto, pokud bychom se podívali na ACF a PACF, nic by nenasvědčovalo tomu, že by mělo jít o takto složitější model. Pokud bychom si vynutili fitování ARMA(1,1), potom budou odhady koeficientů symetrické a budou pusobit proti sobě (viz ono $c$ v teorii výše). Toto je jeden z důvodů, proč tolik preferujeme jednodušší modely a proč je vždy rozumné zkoumat grafy ACF a PACF.
<!--ID: 1692886189385-->



Obecný postup pro modelování časových řad pomocí ARIMA modelů #flashcard 
![[ARIMA.png]]
<!--ID: 1692886189391-->
