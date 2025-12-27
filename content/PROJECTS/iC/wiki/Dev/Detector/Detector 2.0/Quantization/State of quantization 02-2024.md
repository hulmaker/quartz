Ultimate goal - QAT & export to onnx in int8 ops in most layers
Currently (Feb-2024) only feasible option to export in int8 ops is onnx ptq

Tested:

## Super-gradients QAT / export to onnx
### Issues
- QAT in SG never fuses quant/conv+bn+relu/dequant ops, and they remain as 32bit layers
	- SG relies on pytorch-quantization proprietary library from nvidia/tensorrt
	- Only intended use-case for this library is export in 32bit unfused ops, tensorRT network compiler solves this for cuda-enabled devices (jetson etc.)
	- Happens in both old and new SG model export APIs
	- https://github.com/Deci-AI/super-gradients/blob/master/documentation/source/ptq_qat.md
	- Seems to be a limitation of current pytorch-quantization only supporting fake-quantization (as of version 2.2.0) - https://docs.nvidia.com/deeplearning/tensorrt/pytorch-quantization-toolkit/docs/index.html#post-training-quantization
		- "Currently, we only support exporting int8 and fp8 fake quantized modules. Additionally, quantized modules need to be calibrated before exporting to ONNX."
- Potential solution in future versions of SG / pytorch-quantization (nvidia lib) adding support
### Tested solution 1:
- Compiling the fake-quantized QAT or PTQ (both are in float32 in native onnx export) model using TensorRT compiler (trtexec) and using tensorflow wrapper to run on non-cuda hardware
	- Inspired by https://blog.rareschool.com/2019/07/benchmarking-tf-trt-on-raspberry-pi-and.html
		- Blog post author's repo - https://github.com/romilly/pi-nano-tf-benchmarks
	- TF-TRT guide - https://docs.nvidia.com/deeplearning/frameworks/tf-trt-user-guide/index.html
- Problem - TF-TRT must be compiled on cuda-enabled machine, and to be run on aarch64 without cuda most likely cross-compiled on cuda-machine
	- Potential solution: community-built wheels on https://github.com/PINTO0309/Tensorflow-bin/tree/main
	- All wheels report "not compiled with tensorRT support"
		- Potentially misleading error str, the source triggers this error also on library version mismatch
- Potential solution - cross compiling TF-TRT from source for aarch64 with tensorrt support
- Risk - we don't know what speedup could be expected on aarch64

### Tested solution 2:
- Abandoning SG/pytorch-quantization entirely, and writing custom quantization using pytorch native quantizers
- torch provides multiple APIs - eager mode, fx and pytorch 2.0 quant
	- Eager mode is in beta, quantized modules have to be defined manually
	- fx is prototype and abandoned?
	- pytorch 2.0 export quantizer is prototype feature and does not work well, but should be default option and fully automatic in future
		- Fails on tracing certain dynamic model architecture operations - unpack operators, for, else/ifs etc
- Tested eager mode quantization - minimal working example - custom-defined mobilenet v2 on cifar-10
	- Test mostly followed guide https://pytorch.org/tutorials/advanced/static_quantization_tutorial.html
	- Test source will be in detector repo
	- PTQ working in torch.qint8
	- QAT also working in torch.qint8
	- fake-quantized layers for QAT fuse well into all qint8 ops
- Issues
	- both PTQ/QAT models cannot be saved as torch models
		- Torch.save wont properly export modified architecture, and either won't pickle library
		- You have to export state dict, create new model instance, quantize layers and load weights
			- guide https://pytorch.org/docs/stable/quantization.html#frequently-asked-questions
	- Exporting qat model to onnx requires tracer
		- For eager mode in torch 2.2.0, we tested dynamo_tracer (beta)
			- https://pytorch.org/docs/stable/onnx_dynamo.html#
		- Could not trace model due to unsupported ops in tested model (which was way simpler than our custom-yolonas detector) - it has to be converted to fx graph which fails
		- We also tested torchscript exporter (older), also failed
	- Given troubles even with simple model and lack of automatic ptq/qat and tracer support, this is currently unfeasible for our model
- Potentially to be solved in future releases of pytorch


## Only currently feasible solution
- Currently only working way to quantize detector is exporting onnx version of unquantized model from super_gradients, and performing PTQ using onnx library to produce model for onnx runtime on the sensor
- Not automatic, and has to be tested well with every iteration of detector
- Decrease in accuracy for every layer, due to static calibration instead of QAT, has to be tested for biases etc

### Current best-yet settings for onnx ptq
```
params = dict(
                    quant_format=QuantFormat.QDQ,
                    per_channel=False,
                    calibrate_method=CalibrationMethod.MinMax,
                    # calibrate_method=CalibrationMethod.Percentile,
                    # calibrate_method=CalibrationMethod.Entropy,
                    activation_type=QuantType.QInt8,
                    weight_type=QuantType.QInt8, 
                    # reduce_range=True,
                    # extra_options={"MatMulConstBOnly":True},
                    extra_options={"ActivationSymmetric": False, "WeightSymmetric": True},
                    # extra_options={"QDQOpTypePerChannelSupportToAxis": {"MatMul": 1, "Add": 1, "Relu": 1}},
                    optimize_model=False,
                reduce_range=True,
)
```