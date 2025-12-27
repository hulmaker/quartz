http://212.47.16.33:4080/projects/10?page=1

# Dataset versions
# 2023-09-14
[[Euler]] : `/epsilon/nn_training/batch_2-3_fixed_person_only_prunned_0p03_H_bellow_5p0_removed_empty`


# Generation
## Prepare data for annotations
repo: *footfall*
branch: `dev_2.0`
script: `myutils/annotations/generate_trn_data_for_nn.py`

## Data generation for NN

1) from [[CVAT]] export as [[YOLO 1.1 format]].
2) get img data from [[Euler]]:`/epsilon/nn_training/training_data_source_images/`. In case of any issues, labels and images have name in format `{dname}_{frame}.jpg/txt` thus it is possible to reconstruct data
3) 
repo: detector-using-super-gradients, 
branch: `main` 
commit: ``
script: `dataset_management/cvat_yolo_2_sg_structure.py`,  `dataset_management/yolo_data_remove_some_labels.py` and `dataset_management/integrity_check.py`


# batch2 stats
```
kra: 679
pet: 1341
tst: 15
ics: 273
let: 280
mil: 213
mhd: 29
ros: 15
omb: 86
har: 39
ocn: 15
val: 15
```

# batch3 stats
num boxes
`{'0': 10143, '1': 103, '3': 2, '6': 11, '2': 7, '4': 1, '5': 7}`