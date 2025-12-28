Dominik Matula
- Transactional network - nakupuješ v Albertu pravidelně, máš nejspíš něco společného s lidmi co tam nakupují taky pravidelně.
- 2023 assistant - obohacený search v db s kontextem
- 2024 agent - dělá rozhodnutí, je to síť uzlů, kde každý uzel je LLM, udělají stavový diagram a rozhodují a vykonávají. Switchboard principle
- code coverage, regression tests
- LLM testování je hard AF. Nejde to jednodušše porovnat. Lidská slepota, kvanta textu. Je to polovina nákladů na vývoj.
- Bert score = F1 = harmonický průměr. Moc nefunguje, problém když záleží na detailech

### AI as a judge
Použiju got jako arbitra pravdy. Je to prý extrémně těžký a zrádný.
Mají nějaký produkt evalmy.ai


3C: Correctness, completeness, contradiction 
C1: nechci any ai halucinovalo
C2: aby nic nezapomela
C3: aby nekecala

Když dostanu vysoké skóre za všechny C, tak jsou si věty podobný

**Jak na to**:
- 1: vyextrahuj a udělej seznam tvrzení v obou textech. Na úrovni tvrzení ohodnoť 3C
- 2: změř severity of each flaw. (Critical-complete change of meaning, large-significant, small-minor discrepancy vlastně to nevadí, negligible - insignificant detail)
- 3: combine 

Každé jednotlivé C je prý něco jako vážený průměr závažností nad tvrzeními. Kdy každá závažnost má různou váhu.

Kontext je důležitý: soustred se na počty, tohle když je špatně tak mi nevadí atd atd

Ten vzorec jsem si omylem smazal ale je to nejspíš tohle:
2x(1-contradiction)/(Correctness^-1 + completeness^-1)


AI teacher - hodnocení open odpovědi, vysvětlení co je špatně. Fact checking
