---
tags:
  - log/event
  - on/ai
---

https://www.dny.ai/?city=Praha

21.10. https://www.dny.ai/event-2024/ai-startup-pitch-contest-2024

21.10 https://www.dny.ai/event-2024/data-mesh-24-by-dataddo

22.10 https://www.dny.ai/event-2024/tech-happy-hours-2024

https://www.dny.ai/event-2024/tech-happy-hours-2024


## AI TINKERERS
event: https://prague.aitinkerers.org/p/ai-tinkerers-prague-october-meetup-czech-ai-days

**Ondra**:
replicate.com/basta/tomas.flux
generuje obrazky - lora...

**Nik Logachev - hospitable**:
hospitable.com
ai generated suggestions: tech stack
php, Laravel, openai, anthropic - multistep AI pipelines
context + guidelines + XML structure = prompt -> gpt -> message
context = static db with user details + rag with similar responses, guidebook
to make money: ship value, use simple stack
postdoc - analytics 
they pay 10k/m to openai


**Ondřej Michalak+ Matouš Macak**
Gen AI Firewall Demo and test environment - ukazuji demo postavene na gradio
Dělají prostředníka mezi openai a uživatelem (firmou) a dělají "information firewall" - aby openai nevědělo citlivé věci o firmě atd
protective layer demo:
- Mají nějaký dokument kde jsou emaily, text atd
- promptuji ten dokument a chteji z neho dostat informaci o lidech.
- output: misto emailu tam maji nejaky token: PROTECTED-EMAIL
- limituji mnozstvi tokenu aby chranili firmu pred utracenim penez (pravnici pastnou cely zakonik xD)
- checking topic and intent = nekdy LLM odpovida divne, checkuj topic a intent na input a outpu a pokud matchuji, tak je to nejspis valid, jinak invalid a potrbujes to pregenerovat
- maji tam topic extractor, sentiment extractor a metriku k oboum - polarity


**Posledni typek**
research application for lawyers
Problem data:
- neni lehke ziskat law data, digitalizace, API vraci pdf, scraping, ...
- potrebujes case laws
- extraktuj informaci z promptu a z db ziskavej relevantni data
Typek popsal svuj projekt a timhle zpusobem hleda pomoc, radu - Frajer!
rada od cloveka: nepouzivej RAG - za jak dlouho si mam vymenit kombinezu co jsem si prodrel buldozerem - LLM extrahuje veci co nejsou relevantni k zakonu (buldozer, prodreni)

ai4all - o vikendu budou workshopy