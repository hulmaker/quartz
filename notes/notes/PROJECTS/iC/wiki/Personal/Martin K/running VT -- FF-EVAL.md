
example simple run
-----------------

python -m run_group_of_visual_tests --test_names=VT_Atrium_Flora.yaml --footfall_version="refactor_future_for_erik" --footfall_datasets_version=fixing_merge_from_main_2__23 --name="flora_2.1.4_beta_m" --tracking_algorithm=rfc_prasator --num_processes=3 

filter_dnames
-------------------
python -m run_group_of_visual_tests --test_names=VT_Atrium_Flora.yaml --footfall_version="refactor_future_for_erik" --footfall_datasets_version=fixing_merge_from_main_2__23 --name="flora_2.1.4_beta_m" --tracking_algorithm=rfc_prasator --num_processes=3 --dname_filter=flo-203_2023-07


NEW WAY (paths)
------------------------
https://app.clickup.com/t/861nafa8k

`python -m run_all_basic --ds_paths="/data/footfall/datasets/videos/Cestlice/2020-09-01/ics-801/11h/" --cam_conf_paths="/home/stdmartin/footfall-datasets/footfall_datasets/datasets/camera_configs/Cestlice_2020-12/ics-801.yaml" --footfall_version="rework_for_automatization" --footfall_datasets_version="reworking_for_automatization" --name="martin_testing_paths" --dont_update`


python -m run_all_basic --ds_paths="/data/footfall/datasets/videos/Cestlice/2020-09-01/ics-801/11h/" --cam_conf_paths="/home/stdmartin/footfall-datasets/footfall_datasets/datasets/camera_configs/Cestlice_2020-12/ics-801.yaml" --footfall_version="rework_for_automatization" --footfall_datasets_version="reworking_for_automatization" --name="martin_testing_paths" --dont_update



/data/footfall/datasets/videos/BoryMallSK/bma-001/data/2023-10-10-1100/videos/bma-001_2023-10-10-1100_0.mp4,/data/footfall/datasets/videos/BoryMallSK/bma-001/data/2023-10-10-1100/videos/bma-001_2023-10-10-1100_1.mp4,/data/footfall/datasets/videos/BoryMallSK/bma-001/data/2023-10-09-1700/videos/bma-001_2023-10-09-1700_0.mp4,/data/footfall/datasets/videos/BoryMallSK/bma-001/data/2023-10-09-1700/videos/bma-001_2023-10-09-1700_1.mp4,/data/footfall/datasets/videos/BoryMallSK/bma-002/data/2023-10-10-1100/videos/bma-002_2023-10-10-1100_0.mp4,/data/footfall/datasets/videos/BoryMallSK/bma-002/data/2023-10-10-1100/videos/bma-002_2023-10-10-1100_1.mp4,/data/footfall/datasets/videos/BoryMallSK/bma-002/data/2023-10-09-1700/videos/bma-002_2023-10-09-1700_0.mp4,/data/footfall/datasets/videos/BoryMallSK/bma-002/data/2023-10-09-1700/videos/bma-002_2023-10-09-1700_1.mp4





/data/footfall/datasets/videos/BoryMallSK/bma-001/config/2023-10-10-1100.yaml,/data/footfall/datasets/videos/BoryMallSK/bma-001/config/2023-10-10-1100.yaml,/data/footfall/datasets/videos/BoryMallSK/bma-001/config/2023-10-09-1700.yaml,/data/footfall/datasets/videos/BoryMallSK/bma-001/config/2023-10-09-1700.yaml,/data/footfall/datasets/videos/BoryMallSK/bma-002/config/2023-10-10-1100.yaml,/data/footfall/datasets/videos/BoryMallSK/bma-002/config/2023-10-10-1100.yaml,/data/footfall/datasets/videos/BoryMallSK/bma-002/config/2023-10-09-1700.yaml,/data/footfall/datasets/videos/BoryMallSK/bma-002/config/2023-10-09-1700.yaml


additional options
-------------------

`--dont_update`

==> does not update relevant entrances / other various info from cloud -- use this only if running for the second time (as the info is stored in json files)

TODO
options explanation
-------------------
TODO