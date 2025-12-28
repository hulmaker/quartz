
```python
"""  
for each folder in directory, check subfolder /detections/ for file name filter and print version form pickle file  
must be run in footfall conda environment and footfall repository due to the use of pickle on detections cache  


Example:
cd ~/dev/footfall
conda activate footfall
export PYTHONPATH=./src

python this_script.py flo-203

----- output ----
python ls_vts.py flo-203
 /epsilon/VTs//1.22.15/detections/flo-203_2023-03-21_12h.pkl: 5837273ca5506be78e5aa22d0503a1b7a8a723e9
 /epsilon/VTs//martin-testing_visu_fp_fn/detections/flo-203_2023-07-06_12h.pkl: 3f7a2ee06ae979bf3d516d24d9c29f4df935cc2e
 /epsilon/VTs//2.0.0_beta/detections/flo-203_2023-05-13_15h.pkl: UNKNOWN
 /epsilon/VTs//2.0.0_beta/detections/flo-203_2023-03-21_12h.pkl: UNKNOWN
........
"""  
  
import pickle  
import glob  
import os  
import sys 
import tqdm
  
if __name__ == '__main__':  
	dataset_name = sys.argv[1]  
	  
	vts_dir = "/epsilon/VTs/"  
	if len(sys.argv) > 2:  
		vts_dir = sys.argv[2]  

	results_str = ""
	for vt_dir in tqdm.tqdm(os.listdir(vts_dir)):  
		for path in glob.glob(f"{vts_dir}/{vt_dir}/detections/*.pkl"):  
			if dataset_name in path:  
				version = ""  
				with open(path, "rb") as f:  
					commit = pickle.load(f)["commit"]  
				tmp_str = f" {path}: {commit}"
				results_str += tmp_str + "\n"
				print(tmp_str)
				
	print("\n\n\n---- results -----")
	print(results_str)
```


If you run it with only .pkl as an argument, it will print all detections cache in given folder and commits it was created with.