requirements: https://github.com/Deci-AI/super-gradients/blob/master/requirements.txt
```bash
pip install super-gradients
```

# Detektor - loss investigation

[PPYoloELoss](https://github.com/Deci-AI/super-gradients/blob/master/src/super_gradients/training/losses/ppyolo_loss.py), [YoloNAS](https://github.com/Deci-AI/super-gradients/blob/master/documentation/source/YoloNASQuickstart.md)

**YOLOv6** upustilo od anchor points - stoji za to checknout - [paper](https://arxiv.org/abs/2209.02976)

**YOLOv7** si nejsem jisty jestli anchorless adoptovalo - [paper](https://openaccess.thecvf.com/content/CVPR2023/html/Wang_YOLOv7_Trainable_Bag-of-Freebies_Sets_New_State-of-the-Art_for_Real-Time_Object_Detectors_CVPR_2023_paper.html)

**YOLOv8** anchorless adoptovalo - [paper](https://openaccess.thecvf.com/content/CVPR2023W/AICity/html/Vats_Enhancing_Retail_Checkout_Through_Video_Inpainting_YOLOv8_Detection_and_DeepSort_CVPRW_2023_paper.html)

**YOLO-NAS** nema uverejneny paper a co se tyka anchorless designu, tak se tam nejspis nic nezmenilo


from super_gradients.training.losses import PPYoloELoss
from super_gradients.training.metrics import DetectionMetrics_050
from super_gradients.training.models.detection_models.pp_yolo_e import PPYoloEPostPredictionCallback

# PPYoloELoss
```python
loss = cls_weight * loss_cls + iou_weight * loss_iou + dfl_weight * loss_dfl
```
 * **CLS loss**: classification loss -  varifocal_loss/focal_loss (prakticky cross entropy)
 * **IoU, dfl loss**: bbox loss

[jupyterlab](http://212.47.16.33:6008)

Prijde mi, ze to ze to nefungovalo nesouvisi s tim ze je to anchor less, ale ze tam bude spis nejaky bug. 