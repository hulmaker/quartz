

with paths
-----------------
GUIDE:

  
not optional:

`conda activate ffeval`  

optional:

`git checkout adding_cript_to_create_videos_in_new_struct`

`git pull`

`python setup.py install --user`

not optional:

`export DATASETS_PATH=/data/footfall/datasets/`
`python -m footfall_datasets.video.create_videos_and_timestamps_from_images --recording_folder="/data/footfall/datasets/videos/PetCentrum/pet-588/data/2023-09-12-1421/" --create_timestamps --n=1 --crf="15"`

before (without paths / with datasets or VT configs):
----------------------

`python footfall_datasets/annotations/tasks_upload_automation.py --user="martin" --VT_configs="VT_testing_upload_delete_later.yaml"`


`python footfall_datasets/annotations/tasks_upload_automation.py --user="martin" --VT_configs="VT_testing_upload_delete_later.yaml" --dataset="str-001_2023-08-30_13h" --save_path="/home/stdmartin/tmp/upload_annots/"`



new with project id
----------------------------


`python footfall_datasets/annotations/tasks_upload_automation.py --user="martin" --VT_configs="VT_OC_Stromovka.yaml" --dataset="str-001_2023-08-30_13h" --save_path="/home/stdmartin/tmp/upload_annots/" --project_id=16`


