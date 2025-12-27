# description
pruning run by [[PROJECTS/iC/wiki/Personal/Martin Vadlejch]] from `batch_2-3_fixed_person_only_prunned_0p03_H_bellow_5p0_removed_empty_256x320_lre-4`, expecting ~22% improvement in FPS on 64bit to 10.5FPS using 3 cores. This should be enough to run on 32bit.
# benchmark performance without quantisation
```json
#TP: 328, #FP: 61, #FN: 23
#LOW TP: 116, #FP: 14, #FN: 3
#HIGH TP: 212, #FP: 47, #FN: 20
#TP_mean: 0.00, #FP_mean: 0.00, #FN_mean: 0.00
recall: (93.45%) precision: (84.32%)
f1: 0.8865
f1_low: 0.9317
f1_high: 0.8635
```


can be compared with ![[batch_2-3_fixed_person_only_prunned_0p03_H_bellow_5p0_removed_empty_256x320_lre-4_continued_ckpt_best_3x160x224_opv11_3.onnx#benchmark performance without quantisation]]
