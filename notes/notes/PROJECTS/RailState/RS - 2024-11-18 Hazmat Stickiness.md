---
link: https://app.shortcut.com/railstate/epic/5131/incorporate-a-hazmat-stickiness-approach-to-infer-the-un-from-prior-sightings?group_by=none&ct_workflow=all&cf_workflow=500000005
---
branch: 
feature/sc-5131/hazmat-stickiness


[Human labeled data](https://drive.google.com/drive/u/2/folders/1oFnZBH_gsoe-NsvrQ9QixxpXWTM0m8x2)
[List of relevant threads](https://railstate.slack.com/lists/TLJUZ2J8K/F086ZUUGNBZ)


mame databazi caru, doplnuje se car id mezi sightingami
hazmat se muze menit, ale nedeje se to casto
z databaze si vyjet historii vagonu a co se stalo s hazmatama
pak se doptat expertu co muzeme predpokladat
chceme zvysit hazmat acc tim, ze prijdeme na to co se s tim stane mezi sightingama - za jakych okolnosti tam muzeme doplnit, dat tam flag ze to bylo autocorrected
najit kdy je spatne identifikovany placard - casy? sensory? vagony? - ruzne distribuce v zavislosti na velicine - per car, per hazmat class atd
v excelu jsou human rated ground truth
v grafane jsou cv Pipeline - quality dashboard - 
hazmat detection:
- detekce boxu 
- klasifikator na box a zjisti se co je to za class
- ocr - nezvisle na clasifikatoru - ten muze i nekdy prepsat co rekl klasifikator
tady si to muzes projit: placard_detection/hazmat_detection_worker.py - find_placards, postprocess_detected_placards

statistika - vidim car, ale nebyl tam ten box vubec (to neni empty, ale ze tam vubec nebyl)

detekuje se to v klasifikatoru, ale statistika se vyhazuje v composeru - protoze az v composeru se vi co je to za car type

jak to chceme resit - na dev_cz
co si myslime ze plati o tom jak se chovaji vagony - dev

udelat hruby nastrel toho algoritmu, doplnit cisla z databaze a validovat si to na dev jestli je to tak jak to chceme implementovat

# Notes
* train profile = 1 trip
* hazmat je vázaný na tank car - technicky je ale v db na container
* Hazard class je třída (např. exploze, hořlavina...), UN number je ID hazmatu

Co chceme zjistit:
* stabilita hazardu
	* v rámci journey, mimo journey, v čase atd.
	* za předpokladu, že je car v train profile po celý týden a ne nikde jinde
- šance že se hazmat na car změní v nějakém čas. horizontu
	- když je car jen v jednom train id
	- když je car ve vícero train ids
- testnout, jestli existují nějaké typy hazmatu co nejsou stabilní
- Pokud hazmat nevidíme, tak jestli se stane, že to nevidíme ve všech sightingách

car sighting muze mit nekolik hazmat sightingu
To ze se hazmat zmeni beru ze unikatni vycet trid se zmeni?
# Plán
 1. random sample of cars
 2. get history for each of these cars
 3. concat the history into a large table
 4. get train sightings and profiles that are in the large table
 5. analyze the data distributions
 6. decide on what to do next based on the distribution

stabilita v ramci journey
breakdown zmeny - jestli je to z neceho na empty, z empty na neco, nebo zmena tridy

# Specific cases

## PROX0000071707
**DONE**: NO
 - UN: EMPTY, EMPTY, UN3082, UN3082
 - CAR: [1686536](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=PROX0000071707&car_type=Tank+Car&sighting_id=1686536&detection_time_min=&detection_time_max=), [1686519](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=PROX0000071707&car_type=Tank+Car&sighting_id=1686519&detection_time_min=&detection_time_max=), [1687204](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=PROX0000071707&car_type=Tank+Car&sighting_id=1687204&detection_time_min=&detection_time_max=), [1687383](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=PROX0000071707&car_type=Tank+Car&sighting_id=1687383&detection_time_min=&detection_time_max=)
 - SIGH: [1686536](https://development.railstate.com/debug_tools/sighting/1686536/), [1686519](https://development.railstate.com/debug_tools/sighting/1686519/), [1687204](https://development.railstate.com/debug_tools/sighting/1687204/), [1687383](https://development.railstate.com/debug_tools/sighting/1687383/)
 - PANO: [1686536](https://development.railstate.com/debug_tools/sighting/1686536/panorama/), [1686519](https://development.railstate.com/debug_tools/sighting/1686519/panorama/), [1687204](https://development.railstate.com/debug_tools/sighting/1687204/panorama/), [1687383](https://development.railstate.com/debug_tools/sighting/1687383/panorama/)

**NOTES:** YYYY
3 - hodne artefaktu (duch)


## GATX0000000604
**DONE**: NO
 - UN: EMPTY, EMPTY, UN1075, UN1075
 - CAR: [1813662](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=GATX0000000604&car_type=Tank+Car&sighting_id=1813662&detection_time_min=&detection_time_max=), [1813683](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=GATX0000000604&car_type=Tank+Car&sighting_id=1813683&detection_time_min=&detection_time_max=), [1815976](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=GATX0000000604&car_type=Tank+Car&sighting_id=1815976&detection_time_min=&detection_time_max=), [1816040](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=GATX0000000604&car_type=Tank+Car&sighting_id=1816040&detection_time_min=&detection_time_max=)
 - SIGH: [1813662](https://development.railstate.com/debug_tools/sighting/1813662/), [1813683](https://development.railstate.com/debug_tools/sighting/1813683/), [1815976](https://development.railstate.com/debug_tools/sighting/1815976/), [1816040](https://development.railstate.com/debug_tools/sighting/1816040/)
 - PANO: [1813662](https://development.railstate.com/debug_tools/sighting/1813662/panorama/), [1813683](https://development.railstate.com/debug_tools/sighting/1813683/panorama/), [1815976](https://development.railstate.com/debug_tools/sighting/1815976/panorama/), [1816040](https://development.railstate.com/debug_tools/sighting/1816040/panorama/)

**NOTES:**
1 - og umler je jinak


---

ulozim 10 poslednich hazmatu + sighting id + train id
lookup:
- je konzistejntni s historii ok
- neni konzistentni, pak rozlisujeme pripady
	- UN-UN
	- UN-EMPTY
	- EMPTY-UN

napsat alg, spustit to nad novymi daty, zalogovat si adresy obrazku a rucne to rychle overit
verze 2 sahat do historie
Ultimatne - snizit pocet nanu v historii, 

Je horsi tam nechat none nez tam vyplnit neco co si myslime ze tam chceme

konzistence v ramci journey? - checknout jestli ta zmena nastava kdyz se meni train id - jestli je tam zvysena koncentrace

napsat do epicu, napsat algoritmus do dev-cz

---

UN missread
data chybi

---
## AITX0000220346

UN: [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=AITX0000220346&car_type=Tank+Car&sighting_id=2065882&detection_time_min=&detection_time_max=), [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=AITX0000220346&car_type=Tank+Car&sighting_id=2066516&detection_time_min=&detection_time_max=), [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=AITX0000220346&car_type=Tank+Car&sighting_id=2066206&detection_time_min=&detection_time_max=), [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=AITX0000220346&car_type=Tank+Car&sighting_id=2069423&detection_time_min=&detection_time_max=), [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=AITX0000220346&car_type=Tank+Car&sighting_id=2069708&detection_time_min=&detection_time_max=) || [UN1202](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=AITX0000220346&car_type=Tank+Car&sighting_id=UN1202&detection_time_min=&detection_time_max=), [UN1202](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=AITX0000220346&car_type=Tank+Car&sighting_id=UN1202&detection_time_min=&detection_time_max=), [UN1202](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=AITX0000220346&car_type=Tank+Car&sighting_id=UN1202&detection_time_min=&detection_time_max=), [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=AITX0000220346&car_type=Tank+Car&sighting_id=EMPTY&detection_time_min=&detection_time_max=), [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=AITX0000220346&car_type=Tank+Car&sighting_id=EMPTY&detection_time_min=&detection_time_max=)

PANO: [2065882](https://development.railstate.com/debug_tools/sighting/2065882/panorama/), [2066516](https://development.railstate.com/debug_tools/sighting/2066516/panorama/), [2066206](https://development.railstate.com/debug_tools/sighting/2066206/panorama/), [2069423](https://development.railstate.com/debug_tools/sighting/2069423/panorama/), [2069708](https://development.railstate.com/debug_tools/sighting/2069708/panorama/) || [2074892](https://development.railstate.com/debug_tools/sighting/2074892/panorama/), [2076045](https://development.railstate.com/debug_tools/sighting/2076045/panorama/), [2076351](https://development.railstate.com/debug_tools/sighting/2076351/panorama/), [2088935](https://development.railstate.com/debug_tools/sighting/2088935/panorama/), [2095112](https://development.railstate.com/debug_tools/sighting/2095112/panorama/)

UMLER missread
AITX0000220346 je BRGX0000000310 pro vsechny 3 pripady kde je UN

## CBTX0000717353

UN: [UN1202](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000717353&car_type=Tank+Car&sighting_id=2146564&detection_time_min=&detection_time_max=), [UN1202](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000717353&car_type=Tank+Car&sighting_id=2147993&detection_time_min=&detection_time_max=), [UN1202](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000717353&car_type=Tank+Car&sighting_id=2150005&detection_time_min=&detection_time_max=), [UN1202](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000717353&car_type=Tank+Car&sighting_id=2150426&detection_time_min=&detection_time_max=), [UN1202](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000717353&car_type=Tank+Car&sighting_id=2169459&detection_time_min=&detection_time_max=) || [UN1075](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000717353&car_type=Tank+Car&sighting_id=UN1075&detection_time_min=&detection_time_max=), [UN1075](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000717353&car_type=Tank+Car&sighting_id=UN1075&detection_time_min=&detection_time_max=), [UN1202](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000717353&car_type=Tank+Car&sighting_id=UN1202&detection_time_min=&detection_time_max=), [UN1202](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000717353&car_type=Tank+Car&sighting_id=UN1202&detection_time_min=&detection_time_max=), [UN1202](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000717353&car_type=Tank+Car&sighting_id=UN1202&detection_time_min=&detection_time_max=)

PANO: [2146564](https://development.railstate.com/debug_tools/sighting/2146564/panorama/), [2147993](https://development.railstate.com/debug_tools/sighting/2147993/panorama/), [2150005](https://development.railstate.com/debug_tools/sighting/2150005/panorama/), [2150426](https://development.railstate.com/debug_tools/sighting/2150426/panorama/), [2169459](https://development.railstate.com/debug_tools/sighting/2169459/panorama/) || [2170512](https://development.railstate.com/debug_tools/sighting/2170512/panorama/), [2171026](https://development.railstate.com/debug_tools/sighting/2171026/panorama/), [2178275](https://development.railstate.com/debug_tools/sighting/2178275/panorama/), [2178764](https://development.railstate.com/debug_tools/sighting/2178764/panorama/), [2180846](https://development.railstate.com/debug_tools/sighting/2180846/panorama/)

L: OK, R: necitelne
R1, R2 necitelne, navic R2: spatne UN - kdyz si to stahnu, tak je to missread
R3, pak uz je to spravne
## CBTX0000726055

UN: [UN1301](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000726055&car_type=Tank+Car&sighting_id=2058401&detection_time_min=&detection_time_max=), [UN1301](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000726055&car_type=Tank+Car&sighting_id=2058412&detection_time_min=&detection_time_max=), [UN1301](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000726055&car_type=Tank+Car&sighting_id=2059633&detection_time_min=&detection_time_max=), [UN1987](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000726055&car_type=Tank+Car&sighting_id=2176880&detection_time_min=&detection_time_max=), [UN1987](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000726055&car_type=Tank+Car&sighting_id=2179761&detection_time_min=&detection_time_max=) || [UN1301](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000726055&car_type=Tank+Car&sighting_id=UN1301&detection_time_min=&detection_time_max=), [UN1301](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000726055&car_type=Tank+Car&sighting_id=UN1301&detection_time_min=&detection_time_max=), [UN1301](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000726055&car_type=Tank+Car&sighting_id=UN1301&detection_time_min=&detection_time_max=), [UN1301](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000726055&car_type=Tank+Car&sighting_id=UN1301&detection_time_min=&detection_time_max=), [UN1301](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000726055&car_type=Tank+Car&sighting_id=UN1301&detection_time_min=&detection_time_max=)

PANO: [2058401](https://development.railstate.com/debug_tools/sighting/2058401/panorama/), [2058412](https://development.railstate.com/debug_tools/sighting/2058412/panorama/), [2059633](https://development.railstate.com/debug_tools/sighting/2059633/panorama/), [2176880](https://development.railstate.com/debug_tools/sighting/2176880/panorama/), [2179761](https://development.railstate.com/debug_tools/sighting/2179761/panorama/) || [2179805](https://development.railstate.com/debug_tools/sighting/2179805/panorama/), [2180053](https://development.railstate.com/debug_tools/sighting/2180053/panorama/), [2184374](https://development.railstate.com/debug_tools/sighting/2184374/panorama/), [2187198](https://development.railstate.com/debug_tools/sighting/2187198/panorama/), [2190347](https://development.railstate.com/debug_tools/sighting/2190347/panorama/)

L1 zarostle, neni nic videt
L2, L3 ok
L4-R5 nejsou zaznamy
## CBTX0000727816

UN: [UN3082](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727816&car_type=Tank+Car&sighting_id=2087500&detection_time_min=&detection_time_max=), [UN3082](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727816&car_type=Tank+Car&sighting_id=2091801&detection_time_min=&detection_time_max=), [UN3082](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727816&car_type=Tank+Car&sighting_id=2091872&detection_time_min=&detection_time_max=), [UN3082](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727816&car_type=Tank+Car&sighting_id=2094970&detection_time_min=&detection_time_max=), [UN3082](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727816&car_type=Tank+Car&sighting_id=2092132&detection_time_min=&detection_time_max=) || [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727816&car_type=Tank+Car&sighting_id=EMPTY&detection_time_min=&detection_time_max=), [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727816&car_type=Tank+Car&sighting_id=EMPTY&detection_time_min=&detection_time_max=), [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727816&car_type=Tank+Car&sighting_id=EMPTY&detection_time_min=&detection_time_max=), [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727816&car_type=Tank+Car&sighting_id=EMPTY&detection_time_min=&detection_time_max=), [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727816&car_type=Tank+Car&sighting_id=EMPTY&detection_time_min=&detection_time_max=)

PANO: [2087500](https://development.railstate.com/debug_tools/sighting/2087500/panorama/), [2091801](https://development.railstate.com/debug_tools/sighting/2091801/panorama/), [2091872](https://development.railstate.com/debug_tools/sighting/2091872/panorama/), [2094970](https://development.railstate.com/debug_tools/sighting/2094970/panorama/), [2092132](https://development.railstate.com/debug_tools/sighting/2092132/panorama/) || [2144360](https://development.railstate.com/debug_tools/sighting/2144360/panorama/), [2144523](https://development.railstate.com/debug_tools/sighting/2144523/panorama/), [2149510](https://development.railstate.com/debug_tools/sighting/2149510/panorama/), [2150745](https://development.railstate.com/debug_tools/sighting/2150745/panorama/), [2165061](https://development.railstate.com/debug_tools/sighting/2165061/panorama/)

L: OK
R: OK
## CBTX0000727917

UN: [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727917&car_type=Tank+Car&sighting_id=2105579&detection_time_min=&detection_time_max=), [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727917&car_type=Tank+Car&sighting_id=2109484&detection_time_min=&detection_time_max=), [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727917&car_type=Tank+Car&sighting_id=2130708&detection_time_min=&detection_time_max=), [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727917&car_type=Tank+Car&sighting_id=2132114&detection_time_min=&detection_time_max=), [EMPTY](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727917&car_type=Tank+Car&sighting_id=2134249&detection_time_min=&detection_time_max=) || [UN1993](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727917&car_type=Tank+Car&sighting_id=UN1993&detection_time_min=&detection_time_max=), [UN1993](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727917&car_type=Tank+Car&sighting_id=UN1993&detection_time_min=&detection_time_max=), [UN1206](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727917&car_type=Tank+Car&sighting_id=UN1206&detection_time_min=&detection_time_max=), [UN1993](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727917&car_type=Tank+Car&sighting_id=UN1993&detection_time_min=&detection_time_max=), [UN1993](https://development.railstate.com/debug_tools/cars/?ocr_umler_number=CBTX0000727917&car_type=Tank+Car&sighting_id=UN1993&detection_time_min=&detection_time_max=)

PANO: [2105579](https://development.railstate.com/debug_tools/sighting/2105579/panorama/), [2109484](https://development.railstate.com/debug_tools/sighting/2109484/panorama/), [2130708](https://development.railstate.com/debug_tools/sighting/2130708/panorama/), [2132114](https://development.railstate.com/debug_tools/sighting/2132114/panorama/), [2134249](https://development.railstate.com/debug_tools/sighting/2134249/panorama/) || [2147509](https://development.railstate.com/debug_tools/sighting/2147509/panorama/), [2147745](https://development.railstate.com/debug_tools/sighting/2147745/panorama/), [2150056](https://development.railstate.com/debug_tools/sighting/2150056/panorama/), [2150765](https://development.railstate.com/debug_tools/sighting/2150765/panorama/), [2152866](https://development.railstate.com/debug_tools/sighting/2152866/panorama/)

L: OK, R: OK (jen R3 je necitelne)

---
nekdy tam jsou 2 protoze failnul car splitting: https://development.railstate.com/debug_tools/cars/?ocr_umler_number=PROX0000044908&car_type=Tank+Car&sighting_id=2231142&detection_time_min=&detection_time_max=

---

Mame aspon 8 z nich neco, tak to preplacnu

vymysli pravidlo co chces pouzit
* majoritni hlasovani
* vyzkousej to nasimulovat a kouknout se co to udela - kolik mame winu a kolik lossu

najit zajimavejsi pripady - test na sucho s datama co mam - ty co jsou nezmenene a zmenene a ty zmenene jsou kandidat na to to ratovat - a bud to posleme cele a nebo 

bylo by zajimave tam videt i zmeny nez jen z none na neco

udelat algoritmus tak aby se to mohlo menit a doplnit ten human

utilita v pythonu na stahovani storage

---

alg, co zmeni, annotace
finetuning na zaklade annotaci
druha faze - prepsani, 
cache je problematicka kdyz prijde autokorekce, muze to invalidovat hazmat korekci a i korekci okolnich
musi to byt bezestavovy alg.

UN to UN harder than UN to easy

---

**Pár vět na status call**

We took a closer look into the data around hazmat placards on tank cars. We confirmed our previous believes that the placards change very rarely on a single car. Since placards are very small, it is very challenging to identify them with high confidence. Meaning that it is much more likely that we misclassify the hazmat than someone actually switched it.

We send approx. 1000 cars for human labeling and designed an algorithm to automatically correct false changes. 

On the data, we were able to improve the accuracy by more than 5% and we still see some room for improvement.

Currently we are working on integrating the algorithm into the system which requires some database changes and designing a caching functionality to allow the algorithm to run in real time.

 ---

samle kde je to to same a alternuje to s NaN
pokud conf > threshold, tak se to prepise, jinak zustane stejny
vzit v uvahu casovy interval
preferuj aby to zustalo stejne v jednom train profile
human label - kdyz je none, tak je unreadable

---

`sim_input_data.pq` vychazi z `corrected_df.pq`, `corrected_df.pq` vychazi z `load_df(...)`, ale z nejakeho duvodu jsem to nejdriv prohnal autocorrectorem a pak k tomu pridal nejaka dalsi data z db. -- melo by to byt v pohode, jen jsou v `un_number` spatne hodnoty a spravne jsou v `original_un_number`

#### Context:
sance ze context ma stejny un_number je 0.6
kdyz bereme v potaz context, zlepsime se pul procenta (107 vs 106 chyb)
{
	'P(prev == curr)': 0.6,
	 'P(curr == next)': 0.6,
	 'P(prev == curr == next)': 0.6,
 }






### TODO: FIX - Test cases are failing on

**reading parquet files**:
 - add pyarrow as a dependency
 - use a different format - make sure that all the values loads correctly
 
**secretmanager access during build time**:
 - google.api_core.exceptions.PermissionDenied: 403 Permission 'secretmanager.versions.access' denied
 
 **Database connection**
 - download train sighting and save it as a json instead?
 - skip test if it is impossible to download secret or connect to a database?


### TODO: Default Parameters

- Create a dataclass json mixin with default algorithm parameters. The sequential retro-corrector should use them too.
- Don't forget to update tests and experiments.

# Log analysis on the train id server
grep "Hazmat correction" log.txt.2025-02-11 | awk '{print $1, $2, $9, $12, $14, $16}' | tr " " ";"
annotation job image name je:
`image_filename = f"{car.sighting_id}_{car.sequence}_{car.idx}_{Path(car.image_path).name}"  # type: ignore`
podle toho pujde poznat co je to za car.


---
0x7fff=32767

SHRT_MAX = 32767 # Maximum value for a variable of type short

			# in cv2.warpPerspective OpenCV uses short for efficient calculations
			# there is a limit on the image size set by SHRT_MAX.
			# If the image is too big, we have to skip it otherwise we will get an assertion error.
			# See the story on shortcut: sc-47337
			if full_image.shape[0] > SHRT_MAX or full_image.shape[1] > SHRT_MAX:
				logger.warning('Image is too big, skipping it.')
				continue


## 2025-02-18
- koukni jestli cteme eventy - v debug ui, najdi sensor s id co potrebujes
tunnel na izar
udelej si tunel a expose port 80, pak se pripoj na UI tag readeru a koukni jestli tam dochazi ke cteni.
RS+long+train


## daemon.log
```
Feb 15 17:22:33 IZAR-2025c2 tmmpd[1703]: TMR_startReading success..  
Feb 15 17:22:33 IZAR-2025c2 tmmpd[1703]: TMR_stopReading success... TotalTag Read count:0 Total Stats Count:5  
Feb 15 17:22:33 IZAR-2025c2 tmmpd[1703]: TMR_startReading success..  
Feb 15 17:22:33 IZAR-2025c2 tmmpd[1703]: TMR_stopReading success... TotalTag Read count:0 Total Stats Count:5  
Feb 15 18:19:55 IZAR-2025c2 dhclient: DHCPREQUEST on eth0 to 192.168.66.1 port 67  
Feb 15 18:19:55 IZAR-2025c2 dhclient: DHCPACK from 192.168.66.1  
Feb 15 18:19:55 IZAR-2025c2 dhclient: bound to 192.168.66.119 -- renewal in 15312 seconds.  
Feb 15 22:35:12 IZAR-2025c2 dhclient: DHCPREQUEST on eth0 to 192.168.66.1 port 67  
Feb 15 22:35:12 IZAR-2025c2 dhclient: DHCPACK from 192.168.66.1  
Feb 15 22:35:12 IZAR-2025c2 dhclient: bound to 192.168.66.119 -- renewal in 14893 seconds.  
Feb 16 01:12:59 IZAR-2025c2 ntpd verification[1701]: grep: /tmp/foo: No such file or directory  
Feb 16 01:30:12 IZAR-2025c2 ntpd verification[1701]: grep: /tmp/foo: No such file or directory  
Feb 16 01:47:24 IZAR-2025c2 ntpd verification[1701]: grep: /tmp/foo: No such file or directory  
Feb 16 02:02:47 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 16 02:19:38 IZAR-2025c2 ntpd verification[1701]: grep: /tmp/foo: No such file or directory  
Feb 16 02:43:30 IZAR-2025c2 dhclient: DHCPREQUEST on eth0 to 192.168.66.1 port 67  
Feb 16 02:43:30 IZAR-2025c2 dhclient: DHCPACK from 192.168.66.1  
Feb 16 02:43:30 IZAR-2025c2 dhclient: bound to 192.168.66.119 -- renewal in 17289 seconds.  
Feb 16 04:18:26 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 16 04:37:06 IZAR-2025c2 ntpd verification[1701]: grep: /tmp/foo: No such file or directory  
Feb 16 07:07:51 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 16 07:31:43 IZAR-2025c2 dhclient: DHCPREQUEST on eth0 to 192.168.66.1 port 67  
Feb 16 07:31:43 IZAR-2025c2 dhclient: DHCPACK from 192.168.66.1  
Feb 16 07:31:44 IZAR-2025c2 dhclient: bound to 192.168.66.119 -- renewal in 17365 seconds.  
Feb 16 10:01:01 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 16 10:07:29 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 16 12:21:13 IZAR-2025c2 dhclient: DHCPREQUEST on eth0 to 192.168.66.1 port 67  
Feb 16 12:21:13 IZAR-2025c2 dhclient: DHCPACK from 192.168.66.1  
Feb 16 12:21:13 IZAR-2025c2 dhclient: bound to 192.168.66.119 -- renewal in 15257 seconds.  
Feb 16 15:56:25 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 16 16:12:24 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 16 16:35:35 IZAR-2025c2 dhclient: DHCPREQUEST on eth0 to 192.168.66.1 port 67  
Feb 16 16:35:35 IZAR-2025c2 dhclient: DHCPACK from 192.168.66.1  
Feb 16 16:35:35 IZAR-2025c2 dhclient: bound to 192.168.66.119 -- renewal in 17670 seconds.  
Feb 16 18:29:42 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 16 18:35:31 IZAR-2025c2 ntpd verification[1701]: grep: /tmp/foo: No such file or directory  
Feb 16 21:30:09 IZAR-2025c2 dhclient: DHCPREQUEST on eth0 to 192.168.66.1 port 67  
Feb 16 21:30:09 IZAR-2025c2 dhclient: DHCPACK from 192.168.66.1  
Feb 16 21:30:10 IZAR-2025c2 dhclient: bound to 192.168.66.119 -- renewal in 18914 seconds.  
Feb 16 23:24:05 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 16 23:36:08 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 17 01:13:21 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 17 01:16:36 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 17 02:45:28 IZAR-2025c2 dhclient: DHCPREQUEST on eth0 to 192.168.66.1 port 67  
Feb 17 02:45:28 IZAR-2025c2 dhclient: DHCPACK from 192.168.66.1  
Feb 17 02:45:29 IZAR-2025c2 dhclient: bound to 192.168.66.119 -- renewal in 15264 seconds.  
Feb 17 04:09:27 IZAR-2025c2 ntpd verification[1701]: grep: /tmp/foo: No such file or directory  
Feb 17 06:59:58 IZAR-2025c2 dhclient: DHCPREQUEST on eth0 to 192.168.66.1 port 67  
Feb 17 06:59:58 IZAR-2025c2 dhclient: DHCPACK from 192.168.66.1  
Feb 17 06:59:58 IZAR-2025c2 dhclient: bound to 192.168.66.119 -- renewal in 15343 seconds.  
Feb 17 08:03:14 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 17 11:15:46 IZAR-2025c2 dhclient: DHCPREQUEST on eth0 to 192.168.66.1 port 67  
Feb 17 11:15:46 IZAR-2025c2 dhclient: DHCPACK from 192.168.66.1  
Feb 17 11:15:46 IZAR-2025c2 dhclient: bound to 192.168.66.119 -- renewal in 18556 seconds.  
Feb 17 15:07:38 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 17 15:37:34 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 17 16:25:06 IZAR-2025c2 dhclient: DHCPREQUEST on eth0 to 192.168.66.1 port 67  
Feb 17 16:25:06 IZAR-2025c2 dhclient: DHCPACK from 192.168.66.1  
Feb 17 16:25:07 IZAR-2025c2 dhclient: bound to 192.168.66.119 -- renewal in 15588 seconds.  
Feb 17 18:44:19 IZAR-2025c2 ntpd verification[1701]: grep: /tmp/foo: No such file or directory  
Feb 17 19:01:31 IZAR-2025c2 ntpd verification[1701]: grep: /tmp/foo: No such file or directory  
Feb 17 20:44:58 IZAR-2025c2 dhclient: DHCPREQUEST on eth0 to 192.168.66.1 port 67  
Feb 17 20:44:58 IZAR-2025c2 dhclient: DHCPACK from 192.168.66.1  
Feb 17 20:44:58 IZAR-2025c2 dhclient: bound to 192.168.66.119 -- renewal in 15843 seconds.  
Feb 17 22:50:32 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 18 01:09:05 IZAR-2025c2 dhclient: DHCPREQUEST on eth0 to 192.168.66.1 port 67  
Feb 18 01:09:05 IZAR-2025c2 dhclient: DHCPACK from 192.168.66.1  
Feb 18 01:09:06 IZAR-2025c2 dhclient: bound to 192.168.66.119 -- renewal in 17324 seconds.  
Feb 18 04:45:41 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory  
Feb 18 05:57:55 IZAR-2025c2 dhclient: DHCPREQUEST on eth0 to 192.168.66.1 port 67  
Feb 18 05:57:55 IZAR-2025c2 dhclient: DHCPACK from 192.168.66.1  
Feb 18 05:57:55 IZAR-2025c2 dhclient: bound to 192.168.66.119 -- renewal in 19435 seconds.  
Feb 18 07:23:17 IZAR-2025c2 timeupdation[1702]: grep: /tmp/foo: No such file or directory
```

ujasnit si ze muzeme verit lidaru
tag reading d sightingu
mas casy a tagy a jak z toho udelat jeden sighting - protoze tam ten vlak treba dlouho stoji
deduplikace - vyhazes to co je po sobe

Verze 1 - kdyz zacnu vlak a 10 min neprectu nic jineho, poslu to jako sighting. A kdyz jim tam jede vlak zpet a chvili tam stoji, tak jim prijde vic sightingu a oni si s tim poradi.
Verze 2 - odstraneni tam a zpet - koukat na sekvence tag readu a koukat kde je mirror