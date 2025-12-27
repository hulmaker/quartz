
You might want to export and quantize the model first - [[ONNX export and quantization]]

important:
1) set proper input size
2) set model path
3) `intra_op_num_threads = 1 ` switches off multiprocessing which is not a good idea on rpi

```python
"""
forcing onnxruntime to single core processing
"""
from onnxruntime.quantization import CalibrationDataReader
import onnxruntime as ort
import numpy as np
import time
import multiprocessing
from multiprocessing.pool import Pool


# set your own values, implement the DataReader
model_path = '/epsilon/docker/erik/efficientnet-infer.onnx'
threads = 5
repeat = 100    # for each thread, repeat this many times
decimals = 8   # print format option


class DataReader(CalibrationDataReader):
    """
        You can provide real data, or you can generate some dummy data.
        Something like this is necessary for quantization, so it shouldn't be a problem.
    """
    def get_next(self):
        return {
        'img': np.random.rand(*(1, 3, 64, 64)).astype("float32"),
        'location_xy': np.random.rand(*(1, 2)).astype("float32"),
        'bounding_box': np.random.rand(*(1, 4)).astype("float32"),
        'camera_height': np.random.rand(*(1, 1)).astype("float32"),
        'oaa': np.random.rand(*(1, 1)).astype("float32")
    }
    


def do_work(id_):  
    x = DataReader().get_next()
    sess_options = ort.SessionOptions()  
    sess_options.intra_op_num_threads = 1  
    sess_options.execution_mode = ort.ExecutionMode.ORT_SEQUENTIAL  
    sess_options.graph_optimization_level = ort.GraphOptimizationLevel.ORT_ENABLE_ALL  
    ort_sess = ort.InferenceSession(model_path, sess_options)  

    print(f"Job {id_} prepared...", flush=True)  

    times = []
    for i in range(repeat):
        t = time.time()
        outputs = ort_sess.run(None, x)
        times.append(time.time() - t)
    return id_, np.array(times)


p = Pool(threads)
result = p.map(do_work, range(threads))
p.close()

print("All runs finished.")
print(f"\nPrinting results (in seconds) for {repeat} repeats for {threads} threads: \n")

table = [["thread", "repeats", f"total time", "it/[s]", "mean", "std", "min", "max"]]

for id_, times in result:
    table.append([id_, repeat, times.sum(), 1/times.mean(), times.mean(), times.std(), times.min(), times.max()])
    
times = np.array([r[1] for r in result])
table.append(["all", repeat*threads, times.sum(), 1/times.mean(), times.mean(), times.std(), times.min(), times.max()])
    

def print_table(table, decimals):
    format = lambda x: str(np.around(x, decimals=decimals) if isinstance(x, float) else x)
    table = np.vectorize(format)(table)
    length = np.vectorize(len)(table).max()
    table = np.vectorize(lambda x: x.rjust(length))(table)
    print(*list(map(lambda x: " | ".join(x), table)), sep="\n")

    
print_table(table, decimals)
```