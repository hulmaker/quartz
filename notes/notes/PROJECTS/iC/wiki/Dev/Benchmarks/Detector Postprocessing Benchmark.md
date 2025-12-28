# Purpose
this is used for detector + detector postprocessing tuning / evaluation. It is mainly used by [[Eval detector on complete anntoations script]]

# Format
```python
annotations = {
    'dataset name': {
	    frame: [annotation1, annotation2, ...]
    }
   'ics-101_2020-10-12_09h': {
		13: [{'y': 176, 'x': 94, 'height': 30, 'width': 75}],  
		1998: [
			{'y': 249, 'x': 397, 'height': 69, 'width': 53},  
			{'y': 348, 'x': 422, 'height': 66, 'width': 58},  
			{'y': 285, 'x': 80, 'height': 33, 'width': 48},  
			{'y': 432, 'x': 207, 'height': 45, 'width': 41}
		]
	},
```


in [[footfall datasets]] repo, there is a file `footfall_datasets/datasets/detector_evaluation/annotations_vol1.py`

which looks like 
https://gitlab.com/icsystemsai/research/footfall-datasets/-/blob/main/footfall_datasets/datasets/detector_evaluation/annotations_vol1.py?ref_type=heads






# Strollers
https://gitlab.com/icsystemsai/research/footfall-datasets/-/blob/main/footfall_datasets/datasets/detector_evaluation/strollers_annotations.py?ref_type=heads