umler - 4 pismena se doplnuji mezerami a 10 cisla nulami

event 303099 mame


PGPASSWORD=$(gcloud secrets versions access latest --secret=psql_eyen_ro_password) psql -h localhost -p 5432 -U eyen_ro -d train_observation_dev 


ideal ABC, CBA - ale jsou tam repeaty
udelat hezci logovaci vypis
logika kdy uz si myslim ze je dalsi vlak

debug UI - download - detection_event_archive - z toho jde neco mozna vykoukat

namapovat sekvenci tagu a namapovat na sekvenci obrazku
checknout jestli tam jsou nejake tam a zpatky sightingy, nebo jsou cele rozbite

zapisuje s nejakou frekvenci

chyta lidar mezery mezi vagonama?

`grep Deco log.txt | sed "s/.*'equipment initial': '\([A-Z]\+\)', 'car number': \([0-9]\+\).*/\1\2/" |uniq`


Tohle tam vyskakuje za chybu
```
Traceback (most recent call last):
  File "/home/rs-ops/cv_pipeline/bin/tag_reader.py", line 113, in <module>
    loop.run_until_complete(_main())
  File "/usr/lib/python3.10/asyncio/base_events.py", line 649, in run_until_complete
    return future.result()
  File "/home/rs-ops/cv_pipeline/bin/tag_reader.py", line 99, in _main
    tags = reader.read(timeout=int(TIME_STEP * 1000))
RuntimeError: LLRP error
```

Grep na vypsani raw tagu a car_id
```
grep "Raw tag:" logs/tag_reader.log  | awk '{print $1, $2, $7}'
grep "car_id:" logs/tag_reader.log | awk '{print $1, $2, $8}'
```
