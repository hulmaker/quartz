

just one dataset
-----------
use this for re-export -- annots export fixing -- as it rewrites annots

1) connect to gauss
2) `conda activate ffeval`
3) 
`python footfall_datasets/annotations/annotations_export_automation.py --user="martin" --save_path="/home/stdmartin/tmp/testing_annots" --export_exact=flo-101_2023-05-13_17h`
4) pick results from `footfall_datasets/datasets/db_annotations/[dataset name here].json`
5) git commit, push, run...
# known issues

**Important** - you need cvat-cli installed in your environment...
`pip install cvat-cli`

you should also be on the same machine as CVAT is hosted, in our case [[Gauss]]

- it works in `ffeval` conda environment, use others on your own peril.








z clickupu v ramci restructure
--------------

task kde to je v commentech: https://app.clickup.com/t/861nbrm89


**ohledne anotaci**

kdyz je vytahneme z CVATu, tak nemame jak je priradit do spravne slozky, takze to od ted bude fungovat takhle:

- anotace po exportu pujdou VSECHNY do jedne slozky -- `/epsilon/annotations/`
    
    - rozlisovat se budou jmenem datasetu -- to tedy musi byt unikatni
        
- argumenty:
    
    - bude to fungovat, neni potreba moc zmen
        
    - nevidim proc by to melo prestat fungovat do budoucna
        
    - zadne info navic se minimalne neztrati -- protoze ze CVATu ani zadne nemame
        
- nevyhody:
    
    - vse je v jedne slozce -- takze trochu neprehlednost
        
    - neni to idealni reseni, protoze je pak trochu obtiznejsi s anotacemi manipulovat, napr kdybsme chteli vice ruznych anotaci pro stejny dataset, ale tohle je nestandartni problem a navic, jak uz jsem psal, problem ktery tohle minimalne nezhorsi, ze CVATu stejne nejde zadne info, takze se tohle musi delat manualne a to porad pujde
        

  

kdyz se bude vytvaret VT/json tak se proste pro kazdy dataset prohleda tahle slozka

do budoucna v tehle slozce (`/epsilon/annotations/` ) muzeme udelat podslozky:

`/epsilon/annotations/counting`

`/epsilon/annotations/cvat`

na rozliseni rucnich anotaci ktere maji jiny format nez ten ze CVATu


----------------------------------

**doplnujici info**
---------------

doted byla pri exportu anotaci feature:

  

**entrance areas** -- ty fungovaly tak ze se z configu nacetly areas a z CVATu vyexportovane areas se na ne namatchovali

**counts** -- rovnou se pak spocetly counts k jednotlivym entrancum a ulozili se do anotaci (pod jiny key nez annotations)

  

➝ tyhle dve veci ted nemuzou fungovat protoze pri exportu nemame info o ceste ke configu, takze tohle se bude delat separatne za pomoci VT.json a takto "plne hotove" anotace se budou ukladat do:

`/epsilon/annotations/CVAT_with_areas_counts`

  

-------------------

nova struktura tedy bude:

`/epsilon/annotations/CVAT_with_areas_counts` -- plne hotove anotace se vsemi "features"

`/epsilon/annotations/CVAT` -- prvotne vyexportovane anotace, lze pouzit, ale nemusi byt spravne namatchovane entrancy

`/epsilon/annotations/counting` -- rucni pocitani

prikaz co funguje ted (14.11.2023)
-------------------

dobra zprava, cast tohohle uz funguje:

`python footfall_datasets/annotations/annotations_export_automation.py --user="martin" --save_path="/home/stdmartin/tmp/testing_annots" --annotations_save_p=/epsilon/annotations/CVAT --json_config="/home/stdmartin/tmp//OCNovoPlaza_small.json" --export_everything`

je prikaz ktery exportuje vse (nezavisle na annot_DB) ale jen z vt.json, zaroven z toho vt bere cesty ke configum, takze takhle to muzeme pouzivat uz ted, jen jsem zapomnel ze uz jsem tohle delal
