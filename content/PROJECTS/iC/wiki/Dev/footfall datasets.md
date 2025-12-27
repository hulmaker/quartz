This repository is for dataset management. Each recording has a camera config and a dataset config. Both are stored in [this repo](https://gitlab.com/icsystemsai/research/footfall-datasets) (among other things)

# Create a Dataset Config
Let's say you just recorded a video and you want to run the evaluation with [[footfall evaluation repository]]. You have to first create dataset config.
1. Check if the current [camera config](https://gitlab.com/icsystemsai/research/footfall-datasets/-/tree/main/footfall_datasets/datasets/camera_configs?ref_type=heads) exists, otherwise you have to create it. The camera config defines basic information along with camera mask, entrances, etc... `footfall_datasets/datasets/camera_configs`
2. create a file in `footfall_datasets/datasets/datasets_configs` and make a record for each recorded video
3. Create a VT config in the `footfall_datasets/datasets/test_configurations`
4. Continue here [[footfall evaluation repository]]  (**tip**: use --output_dir and -e flags)


# Example of Dataset Config
```yaml
datasets:
  - name: "kra-210_2023-03-13_15h"
    description: ""
    camera_id: 210
    data_type: "imgs"
    path: "videos/Krakov/2023-03-13/kra-210/15h/"
    camera_config_path: "Krakov_2021-11/kra-210.yaml"
    fps: 5
```
