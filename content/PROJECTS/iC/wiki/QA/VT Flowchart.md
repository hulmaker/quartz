# VT automatizace
### Usecases
* Katka chce nahrat video a stahnout si ho sama z gausse - gauss filesystem
* doplnit offline data z VT na cloud pokud nesedí
* Po konfiguraci senzoru se spusti pipeline a na konci je report
* Automatice nahravani videa kdyz je malo pruchodu po spusteni VT
* Zakaznik zpochybnuje ze to funguje, spoustime validacni VT
* Vyjde ti spatny report, zjisti se ze Annotace jsou spatne, musime to preanotovat a dostat novy report
	* Preanotovat - musime resit penize annotatoru, lidsky problem, ne nutne automatizace
	* udelat to uplne znova a zahodit stare - musi se vytvorit znovu job a ten stary se prejmenuje
* uprava configu, annotace ok, znovu vyhodnoceni VT - nemame zpusob jak zjistit config a ten porovnat
	* Zmeni se trochu config ale nemelo by to mit vliv na vysledek annotaci
	* Zmeni se config kriticky a tim padem by se melo znovu annotovat
* Pridani entrance do senzoru ktery uz prosel VT - nova VT na senzor
* celodenni VT - occupancy
* vyhozeni datasetu z VT - vsechno muze byt ok, ale z nejakeho duvodu ho nechceme mit ve vyslednem reportu (zavrene dvere)
* update systemu:
	* mame napocitane annotace, config lze pouzit i na nove verzi - jen se to prepocita
	* mame annotace, ale config se vyrazne zmeni. Annotace pak jdou pouzit jen v nejakych pripadech
* hard negative mining - dat tam nejaky hook, ktery dovoli pridat do trenovaciho datasetu potencialni chyby. - jde to automaticky diky false negatives - pridam frame a nejake framy kolem nej (popsat proces, kdy se tohle spusti)
* vysledkem maji byt i videa na sharepoint-
* experiment kdy chceme zmenit camconf a znovu s nim to vyhodnotit. Nezavazne. bez toho abychom to museli uploadovat do kamery


```json
[
{
	"ds_path": "/data/footfall/datasets/videos_v1/.../.mp4",
	"cam_conf_path": "/data/footfall/datasets/videos_v1/.../.yaml",
	"annots_path": "/epsilon/annotations/CVAT_with_areas_counts/.../.mp4.json",
	"annots_type": "DB"
}
]
``` 

Our goal is to design an automation pipeline that has multiple blocks. Some blocks are parallel, and some are sequential. Each block can be run only if all predecessors are completed. Parallel blocks can run at the same time. But the block following the two parallel blocks must wait for both. Each block has defined inputs and outputs with data types and conditions. There is also a supervisor that reports on what stage the pipeline is and it sends logs. The pipeline can be run from any point. This means that the results have to be stored and a user can decide to skip the first few stages and run the pipeline from the middle. Draw a class diagram that describes this concept.

To design an automation pipeline with multiple blocks, parallel and sequential execution, and a supervisor, you can create a class diagram with the following classes:

1. **PipelineManager**: Manages the execution of the pipeline.
2. **Block**: Represents a single block in the pipeline.
3. **SequentialBlock**: Represents a block that executes sequentially after its predecessor blocks are completed.
4. **ParallelBlock**: Represents a block that can execute in parallel with other parallel blocks.
5. **PipelineSupervisor**: Supervises the pipeline execution and reports on its progress.
6. **Data**: Represents the data passed between blocks.
7. **Logger**: Handles logging for the pipeline.

Below is a class diagram illustrating these concepts:

```
+----------------+             +---------------------+
|  PipelineManager|-------------| PipelineSupervisor  |
+----------------+             +---------------------+
| - blocks: List<Block>         | - log(message)      |
| - executePipeline()           | - reportProgress()  |
| - skipToBlock(blockName)      |                     |
+----------------+             +---------------------+
        |                               ^
        |                               |
        |                               |
        v                               |
+----------------+             +-------------------+
|      Block     |<---------- |      Logger       |
+----------------+             +-------------------+
| - name: string |             | - log(message)    |
| - inputs: List<Data>          +-------------------+
| - outputs: List<Data>         /                 \
| - isCompleted(): boolean     /                   \
| - execute(): void           /                     \
+----------------+           /                       \
         |                  /                         \
         |                 /                           \
         |                /                             \
         |               /                               \
         |              /                                 \
         |             /                                   \
         |            /                                     \
         v           v                                       v
+----------------+ +----------------+                   +-------------------+
| SequentialBlock| |  ParallelBlock |                   |       Data        |
+----------------+ +----------------+                   +-------------------+
|                | |                |                   | - type: DataType  |
+----------------+ +----------------+                   | - condition: Condition |
                                                      +-------------------+

```

Explanation:

- **PipelineManager**: Manages the execution of the pipeline. It contains a list of blocks and methods to execute the pipeline and skip to a specific block.
- **PipelineSupervisor**: Supervises the pipeline execution and reports its progress. It has methods to log messages and report progress.
- **Block**: Represents a single block in the pipeline. It contains information such as name, inputs, outputs, and methods to execute and check completion.
- **SequentialBlock**: Inherits from Block class, represents a block that executes sequentially after its predecessor blocks are completed.
- **ParallelBlock**: Inherits from Block class, represents a block that can execute in parallel with other parallel blocks.
- **Logger**: Handles logging for the pipeline.
- **Data**: Represents the data passed between blocks, including its type and conditions.


experimenty s VT configem - na dataset delat verze, kazda ma nejaky popis



Prozkoumam nastroje, zjistim jestli to umi co potrebujem

na konci export dat souvisejic s vt zachycujici vsechny promenne - config atd. to pak jde vzit, upravit a spustit to znova

nejznamejsi: apache airflow, jenkins, luigi