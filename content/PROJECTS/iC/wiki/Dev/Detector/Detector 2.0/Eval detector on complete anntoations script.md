[[footfall repositor]] / `myutils/diagnostics/eval_detector_on_complete_annotations.py`

# Overview
It will run detector + postprocessing on all frames listed in [[Detector Postprocessing Benchmark]] and computes f1 and other metrics.
- it will ignore FPs/FNs which occurs outside of *current* camera config definition. 

# Output
```json
#TP: 318, #FP: 65, #FN: 32
#LOW TP: 113, #FP: 22, #FN: 6
#HIGH TP: 205, #FP: 43, #FN: 26
#TP_mean: 0.00, #FP_mean: 0.00, #FN_mean: 0.00
recall: (90.86%) precision: (83.03%)
f1: 0.8677
f1_low: 0.8898
f1_high: 0.8559
```

+ it might save some visualisations, more details in script's docopt