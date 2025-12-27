trained with 6a14e377ca2bdc5dcb512f643767450581b26a72
https://gitlab.com/icsystemsai/research/detector-using-super-gradients/-/blob/main/detector_training/trn_sandbox3.py

[[Euler]] : `/epsilon/nn_training/nn_checkpoints/batch_2-3_fixed_person_only_prunned_0p03_H_bellow_5p0_removed_empty_256x320_lre-4_continued_ckpt_best_3x160x224_opv11_3.pth`


`batch_2-3_fixed_person_only_prunned_0p03_H_bellow_5p0_removed_empty_256x320_lre-4_continued_ckpt_best_3x160x224_opv11_3.onnx`

Map@50: 0.8085

```json
#TP: 333, #FP: 44, #FN: 21
#LOW TP: 115, #FP: 16, #FN: 4
#HIGH TP: 218, #FP: 28, #FN: 17
#TP_mean: 0.00, #FP_mean: 0.00, #FN_mean: 0.00
recall: (94.07%) precision: (88.33%)
f1: 0.9111
f1_low: 0.92
f1_high: 0.9064
```

# Quantized
`batch_2-3_fixed_person_only_prunned_0p03_H_bellow_5p0_removed_empty_256x320_lre-4_continued_ckpt_best_3x160x224_opv11_3_v1_picked1.onnx`
HxW: 160x224
```json
picked_idxs_hand = [0, 1, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 22, 24, 26, 28, 29, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 98, 99, 100]

#TP: 318, #FP: 65, #FN: 32
#LOW TP: 113, #FP: 22, #FN: 6
#HIGH TP: 205, #FP: 43, #FN: 26
#TP_mean: 0.00, #FP_mean: 0.00, #FN_mean: 0.00
recall: (90.86%) precision: (83.03%)
f1: 0.8677
f1_low: 0.8898
f1_high: 0.8559
```



# 2.2
### /batch_2-3_fixed_person_only_prunned_0p03_H_bellow_5p0_removed_empty_256x320_lre-4_continued_ckpt_best_3x160x224_opv11_3_pruned_backbone_11M_finetuned_50ep_on_256x320_160x224_picked1.onnx
```JSON
#TP: 293, #FP: 45, #FN: 50
#LOW TP: 105, #FP: 16, #FN: 12
#HIGH TP: 188, #FP: 29, #FN: 38
#TP_mean: 0.00, #FP_mean: 0.00, #FN_mean: 0.00
recall: (85.42%) precision: (86.69%)
f1: 0.8605
f1_low: 0.8824
f1_high: 0.8488

FPS: 5.39

picked_idxs = [0, 1, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 22, 24, 26, 28, 29, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 98, 99, 100]
```

### batch_2-3_fixed_person_only_prunned_0p03_H_bellow_5p0_removed_empty_256x320_lre-4_continued_ckpt_best_3x160x224_opv11_3_pruned_backbone_11M_finetuned_50ep_on_256x320_160x224_picked2.onnx
```JSON
#TP: 298, #FP: 38, #FN: 45
#LOW TP: 106, #FP: 12, #FN: 10
#HIGH TP: 192, #FP: 26, #FN: 35
#TP_mean: 0.00, #FP_mean: 0.00, #FN_mean: 0.00
recall: (86.88%) precision: (88.69%)
f1: 0.8778
f1_low: 0.906
f1_high: 0.8629

FPS: 5.41

picked_idxs = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 22, 24, 26, 28, 29, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 98, 99, 100]
```