
# Investigation
 - [Last neptune run](https://app.neptune.ai/o/Eyen/org/placard-classifier/runs/details?viewId=standard-view&detailsTab=metadata&shortId=PLAC-18&type=run&path=.)
 - entrypoint:  training/car_classification/train.py
 parameters
```
batch_size 64
checkpoint placards_work_dir/epoch_99.pth
checkpoint_num_classes 59
data_folder ../hazmat_classifier/train/
data_workers 16
epochs 100
frozen_backbone False
learning_rate 0.001
learning_rate_gamma 0.4
learning_rate_step 20
model resnet50
no_class_weights False
plot_dataset True
pretrained False
split_seed 42
store_dir placards_work_dir
val_data_folder ../hazmat_classifier/val/
verbose True
weight_decay 0.00001
```