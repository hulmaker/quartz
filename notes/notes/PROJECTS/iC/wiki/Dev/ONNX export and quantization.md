
Make sure you export the model with a correct [opset number](https://onnx.ai/onnx/intro/concepts.html#what-is-an-opset-version). On [[testing rpi 64 bit, iCLab]] you can use max. opset number 17!!

```python
import io
import numpy as np
from torch import nn
import torch.onnx
import torch

checkpoint = "2023-06-02T14:25:53_real_desc_noori_distinct/RealDesc_checkpoint_0000001800_109800.pt"

torch_model = ... # load your model from checkpoint
torch_model.eval()


float_model_path = "efficientnet.onnx"           # just the export
prep_model_path = "efficientnet-infer.onnx"      # optimised for inference
quantized_model_path = "efficientnet-quant.onnx" # quantized

class DataReader(CalibrationDataReader):
    def __init__(self, path, ...):
        # prepare your data. Using real data is recommended
        data = torch.load(path)
        data = torch.utils.data.default_collate(data)
        self.iterator = iter(self.data)
    
	 def get_next(self):  # MANDTORY TO IMPLEMENT
        return next(self.iterator, None)


# Export the model
dr = DataReader("/epsilon/docker/erik/dataset_preview.pt", batch_size=1)
x = {k: torch.from_numpy(v) for k, v in dr.get_next().items()}
torch_out = torch_model(**x)

torch.onnx.export(
    torch_model,               # model being run
    x,                         # model input (or a tuple for multiple inputs)
    float_model_path,   # where to save the model (can be a file or file-like object)
    export_params=True,        # store the trained parameter weights inside the model file
    opset_version=16,          # the ONNX version to export the model to
    do_constant_folding=True,  # whether to execute constant folding for optimization
    input_names = ['img', 'location_xy', 'bounding_box', 'camera_height', 'oaa'],   # the model's input names
    output_names = ['descriptor_logits', 'descriptor', 'oyox_logits', 'oyox'], # the model's output names
)
```

The dynamic axis argument  in `torch.onnx.export` always returns this warning: UserWarning: No names were found for specified dynamic axes of provided input. Automatically generated names will be applied to each dynamic axes of input oyox_logits.
[here](https://github.com/pytorch/pytorch/issues/27695), and [here](https://github.com/pytorch/pytorch/issues/25681) are some links regarding this issue. But you won't most likely want to use dynamic axis. It is slower than static batch size.

---

Your model is now successfully exported as an onnx model. If you want to do the quantization, continue below.


# Quantization

https://onnxruntime.ai/docs/performance/model-optimizations/quantization.html

In the preparation below, I had to use skip_symbolic_shape (some errors). Preparation is recommended by onnx because there are some optimisations. The following code should be run after you setup and run your ONNX export

```python
from onnxruntime.quantization.shape_inference import quant_pre_process
from onnxruntime.quantization import quantize_static, CalibrationDataReader, QuantType, CalibrationMethod, QuantFormat


quant_pre_process(
    float_model_path,
    prep_model_path,
    skip_symbolic_shape=True,
)

dr = DataReader("/epsilon/docker/erik/dataset_preview.pt", batch_size=1)

quantize_static(
    prep_model_path,
    quantized_model_path,
    dr, 
    # nodes_to_quantize=layers_to_quantize,
    quant_format=QuantFormat.QOperator,
    per_channel=False,
    calibrate_method=CalibrationMethod.MinMax,
    activation_type=QuantType.QUInt8, 
    weight_type=QuantType.QUInt8, 
    # reduce_range=True,
    # extra_options={"MatMulConstBOnly":True},
    extra_options={"ActivationSymmetric": True, "WeightSymmetric": True},
    # extra_options={"QDQOpTypePerChannelSupportToAxis": {"MatMul": 1, "Add": 1, "Relu": 1}},
    optimize_model=True
)

print("The quantized model saved as:", quantized_model_path)
```


Responsible person: [[PROJECTS/iC/wiki/Personal/Filip Naiser]], Erik