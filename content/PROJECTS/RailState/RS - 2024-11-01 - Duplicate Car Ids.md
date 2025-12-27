
### Zadani RS
[task](https://app.shortcut.com/railstate/epic/18941?group_by=none&vc_group_by=day&ct_workflow=all&cf_workflow=500000005)

V jednom vlaku přečteme 2 čísla car id
ocr si to nějak vymyslí
důvody: missread, vlak se před senzorem otočí, jede zpátky a my to nepoznáme
v jednom vlaku nejde mit dva stejne vagony, kazdy vagon je unikatni

Drop duplicated car number on the same train
najdi duplicitu a nastav to na nulu
- remove duplicate cars in cv-pipeline
- resolve car id duplicates after auto-correction

1 panorama = 1 vlak (muze se stat chyba)

skonci sighting
- train id server - snazi se najit posledni pozorovani vlaku
- po pozorovani dela autokorekci - doplni z posledniho pozorovani

Najít si v DB nějaké příklady kdy je alespoň jeden carid duplikátní

Jak zjistim ze mi to funguje, testing pipeline?
- udelam test, dam tam data co jsem nasel z db a poustet jen tu funkcionalitu

OCR - detekujeme vsechny boxy, precteme boxy, skladame to cislo

na panorama lvl se musi nechat alespon prvni carid

prometheus router, zalogovat si kdyz neco zahazuju

**Otázky**:
- validovat jak se připojuji k db - gcloud sql connect vs. proxy, jake zpusoby pouzivame
- je [railstate-dev-9](https://console.cloud.google.com/sql/instances/railstate-dev-9/overview?cloudshell=true&project=railstate-development) správná instance? - ano je
- testing - unit test, end-to-end test
- deploy on one cloud panorama instance
- devices - jméno heslo 
- tunel v cloud jak se tam dostanu

**install proxy using gcloud components** - [bug](gcloud sql connect railstate-dev-9 --database=train_observation_dev --user=eyen_ro)
```bash
brew install --cask google-cloud-sdk

# nefunguje, viz: github.com/GoogleCloudPlatform/cloud-sql-proxy/issues/938
gcloud components install cloud-sql-proxy
gcloud sql databases list --instance=railstate-dev-9 # train_observation_dev
```

**Try gcloud sql connect from localhost**:
```bash
# permission error
gcloud sql connect railstate-dev-9 --database=train_observation_dev --user=eyen_ro

# works only with V1 cloud-sql-proxy
gcloud beta sql connect railstate-dev-9 --database=train_observation_dev

# ERROR: (gcloud.sql.connect) HTTPError 403: The client is not authorized to make this request. This command is authenticated as erik.hulmak@eyen.se which is the active account specified by the [core/account] property.
```

**Try gcloud sql connect from cloud shell**
```bash
gcloud sql connect railstate-dev-9 --database=train_observation_dev --user=eyen_ro
# same error result
```

links: [password for eyen_ro](https://docs.google.com/spreadsheets/d/1ALBaxQemTQq_Bgdetszrr4PJV642Xwtx0JFUCa16l3U/edit?gid=0#gid=0), [cloud-sql-proxy releases](https://github.com/GoogleCloudPlatform/cloud-sql-proxy/releases)

**Branch**: feature/sc-18941/duplicate-car-number

### Plan
- Try to run unit tests, e.g. [test](https://github.com/RailState/cv_pipeline/blob/dev/cv_pipeline/auto_correction/test/stack_car_autocorrect_test.py)
- Create your own test cases, figure out how to use the data from db
- Create a class similar to [this](https://github.com/RailState/cv_pipeline/blob/dev/cv_pipeline/auto_correction/stack_car_id_correction.py)
- Integrate the class into the autocorrection pipeline like [here](https://github.com/RailState/cv_pipeline/blob/dev/cv_pipeline/auto_correction/stack_car_id_correction.py)

## Otazky
- access to google storage
- Jak zajistím pořadí cars v sighting? Podle car_sighting.id?
- platformy u stack car sdílí car id. Kde vezmu car id? V db, sloupec trains.car_sightings.id je pk, hodnoty jsou tudíž unikátní.
- jak se dostanu k obrazku (pres gcloud bucket mi to reklo ze objekt neexistuje): 'gs://cv-pipeline-uploads/locations/na/ca/bc/mann/cn/2020/12/1/detected_events/event_22_2020_12_01_14:08:39.497720/separated_cars/panorama_0000_sequence_0_car_0.jpg'

# Udelej extenzi na 
kriterium pro zachovani id, delete - oritinal_id, longest sequence id
V tom druhem story - moznost vypinat rules (mapping)
misto greedy udelej graph structure a vybyrej z komponent co nechat