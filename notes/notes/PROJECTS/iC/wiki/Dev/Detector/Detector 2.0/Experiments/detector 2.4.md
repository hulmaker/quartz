
# no quantization, custom_yolo_s_age_gender_latest_1_3_19M_256_320_full_arch_256_320.onnx
```json
#TP: 343, #FP: 54, #FN: 16
#LOW TP: 119, #FP: 19, #FN: 2
#HIGH TP: 224, #FP: 35, #FN: 14
#TP_mean: 0.00, #FP_mean: 0.00, #FN_mean: 0.00
recall: (95.54%) precision: (86.40%)
f1: 0.9074
f1_low: 0.9189
f1_high: 0.9014
```


# no quantization, custom_yolo_s_age_gender_latest_1_3_19M_256_320_full_arch_160_224.onnx
```json
#TP: 328, #FP: 56, #FN: 25
#LOW TP: 117, #FP: 12, #FN: 4
#HIGH TP: 211, #FP: 44, #FN: 21
#TP_mean: 0.00, #FP_mean: 0.00, #FN_mean: 0.00
recall: (92.92%) precision: (85.42%)
f1: 0.8901
f1_low: 0.936
f1_high: 0.8665

```




# no quantization, strollers, custom_yolo_s_age_gender_latest_1_5_19M_256_320_full_arch_160_224.onnx
```JSON
#TP: 348, #FP: 78, #FN: 90
#LOW TP: 67, #FP: 21, #FN: 29
#HIGH TP: 281, #FP: 57, #FN: 61
recall: (79.45%) precision: (81.69%)
f1: 0.8056
f1_low: 0.7283
f1_high: 0.8265
```




# no quantization, pedestrians, 1_6_age_gender_pruned_256_320_500ep_exp_160x224.onnx
```json
#TP: 329, #FP: 54, #FN: 24
#LOW TP: 114, #FP: 17, #FN: 6
#HIGH TP: 215, #FP: 37, #FN: 18
recall: (93.20%) precision: (85.90%)
f1: 0.894
f1_low: 0.9084
f1_high: 0.8866
```






# 1_8_age_gender_pruned_256_320_finetuned_lowres_300ep_160_224.onnx
### pedestrians
```json
#TP: 337, #FP: 42, #FN: 19
#LOW TP: 114, #FP: 10, #FN: 5
#HIGH TP: 223, #FP: 32, #FN: 14
recall: (94.66%) precision: (88.92%)
f1: 0.917
f1_low: 0.9383
f1_high: 0.9065
```

### strollers
```json
#TP: 389, #FP: 59, #FN: 61
#LOW TP: 82, #FP: 13, #FN: 14
#HIGH TP: 307, #FP: 46, #FN: 47
recall: (86.44%) precision: (86.83%)
f1: 0.8664
f1_low: 0.8586
f1_high: 0.8685
```


## Q_picked3
### pedestrians
```json
#TP: 333, #FP: 43, #FN: 21
#LOW TP: 115, #FP: 13, #FN: 4
#HIGH TP: 218, #FP: 30, #FN: 17
recall: (94.07%) precision: (88.56%)
f1: 0.9123
f1_low: 0.9312
f1_high: 0.9027
```

### strollers
```json
#TP: 365, #FP: 81, #FN: 84
#LOW TP: 77, #FP: 12, #FN: 19
#HIGH TP: 288, #FP: 69, #FN: 65
recall: (81.29%) precision: (81.84%)
f1: 0.8156
f1_low: 0.8324
f1_high: 0.8113
```


## Q_picked4
### pedestrians
```json
#TP: 341, #FP: 70, #FN: 17
#LOW TP: 116, #FP: 26, #FN: 5
#HIGH TP: 225, #FP: 44, #FN: 12
recall: (95.25%) precision: (82.97%)
f1: 0.8869
f1_low: 0.8821
f1_high: 0.8893
```


## strollers
```json
#TP: 381, #FP: 81, #FN: 71
#LOW TP: 81, #FP: 13, #FN: 15
#HIGH TP: 300, #FP: 68, #FN: 56
recall: (84.29%) precision: (82.47%)
f1: 0.8337
f1_low: 0.8526
f1_high: 0.8287
```




# 1_8_age_gender_pruned_256_320_finetuned_lowres_300ep_160_224_genderFix.onnx

## pedestrians
```json
#TP: 343, #FP: 42, #FN: 14
#LOW TP: 116, #FP: 11, #FN: 4
#HIGH TP: 227, #FP: 31, #FN: 10
recall: (96.08%) precision: (89.09%)
f1: 0.9245
f1_low: 0.9393
f1_high: 0.9172
```
## strollers
```json
#TP: 369, #FP: 66, #FN: 80
#LOW TP: 75, #FP: 15, #FN: 21
#HIGH TP: 294, #FP: 51, #FN: 59
recall: (82.18%) precision: (84.83%)
f1: 0.8348
f1_low: 0.8065
f1_high: 0.8424
```



## 1_8_age_gender_pruned_256_320_finetuned_lowres_300ep_160_224_genderFix_Q5.onnx
```json
#TP: 322, #FP: 65, #FN: 29
#LOW TP: 115, #FP: 20, #FN: 4
#HIGH TP: 207, #FP: 45, #FN: 25
recall: (91.74%) precision: (83.20%)
f1: 0.8726
f1_low: 0.9055
f1_high: 0.8554
```


#  /tmp/1_8_age_gender_pruned_256_320_finetuned_lowres_300ep_160_224_genderFix_Q6_percentile_bigger_ds.onnx

## pedestrians
```json
#TP: 329, #FP: 64, #FN: 24
#LOW TP: 113, #FP: 25, #FN: 6
#HIGH TP: 216, #FP: 39, #FN: 18
recall: (93.20%) precision: (83.72%)
f1: 0.882
f1_low: 0.8794
f1_high: 0.8834
```

## strollers
```json
#TP: 295, #FP: 70, #FN: 152
#LOW TP: 34, #FP: 8, #FN: 62
#HIGH TP: 261, #FP: 62, #FN: 90
recall: (66.00%) precision: (80.82%)
f1: 0.7266
f1_low: 0.4928
f1_high: 0.7745
```