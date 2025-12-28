## Prerequisities
- you need to have [[ssh-key in gitlab]], so you don't have to add credentials every time you try to pull something


1) Main repo for Visual Tests as well as for footfall version evaluation is in [footfall-evaluation](https://gitlab.com/icsystemsai/products-evaluation/footfall-evaluation) repository.
2) `cd ./footfall-evaluation/scripts`
3) `bash init_other_repositories.sh {absolute path to footfall-evaluation} master main`, this should initialize footfall, footfall-datasets and submodules etc...

4) It works as follows:
- it clones locally [footfall-datasets](https://gitlab.com/icsystemsai/research/footfall-datasets) (version/branch defined as an argument of the script) (to prevent any issues, this shouldn't be installed in your python envirnoment),
- clones [footfall](https://gitlab.com/icsystemsai/footfall) (defined by tag, branch or commit name).
- And provided by either path (e.g. `/tmp/my_vt.yaml`) or VT_config_name (from `footfall-datasets/footfall_datasets/datasets/test_configurations/*.yaml`) it will compute all detections, checks cache integrity, compute tracking, evaluate using annotations it can also do tracking visualisations and error visualisations and it generates reports.
* For new recordings, you might want to register recordings with [[footfall datasets]]
- it will by default use `/data/footfall/datasets` as a source for images/videos.œ
- it will by default save all data to `/epsilon/VTs/{name}` (can be specified using the `--output_dir=""` flag)

5) Main control is from [run_group_of_visual_tests.py](https://gitlab.com/icsystemsai/products-evaluation/footfall-evaluation/-/blob/main/footfall_evaluation/run_group_of_visual_tests.py?ref_type=heads). Typical usage is (on gauss or other server where data are present):
```bash
git clone --recurse-submodules -j8 git@gitlab.com:icsystemsai/products-evaluation/footfall-evaluation.git

cd footfall-evaluation/footfall_evaluation

# you might want to run this in screen
screen -SU footfall_evaluation

conda activate ffeval; python -m run_group_of_visual_tests --test_names="VT_Benchmark_2023-08_small.yaml" --footfall_version=dev_2.0 --footfall_datasets_version=VT_Benchmark2 --name="2.0.0_beta" --dont_skip_irrelevant_entr --ignore_source
```


**For more details on how to use this script, visit docstring in [run_group_of_visual_tests.py](https://gitlab.com/icsystemsai/products-evaluation/footfall-evaluation/-/blob/main/footfall_evaluation/run_group_of_visual_tests.py?ref_type=heads) script.**


## Example of custom VT.yaml file
```yaml
datasets:
- name: let-001_2021-05-10_12h
  dataset_version: 1
  annotations_type: DB

- name: ics-231_2020-12-03_16h
  dataset_version: 1
  annotations_type: DB

- name: krp-106_2023-04-11_16h
  dataset_version: 1
  annotations_type: DB

- name: "gcs-108_2023-08-11_15h"
  dataset_version: 1
  annotations_type: "config"
```

config means - it was counted only from video and only final sum is saved in footfall-datasets


*Responsible person*: [[Martin Koucky]], [[PROJECTS/iC/wiki/Personal/Filip Naiser]]
