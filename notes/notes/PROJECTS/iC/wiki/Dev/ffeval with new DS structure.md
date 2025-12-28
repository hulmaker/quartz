
ff-datasets on branch:
`more_rework_to_new_struct_changes`

`python footfall_datasets/handling_new_structure/create_json_from_folder.py --oc_path="/data/footfall/datasets/videos/Europa" --output_folder_path="/tmp/"`

will generate `/tmp/Europa.json` with paths...



**branch**: `rework_for_automatization`

`python -m run_all_basic --json_config="/home/stdmartin/ff-eval_second/footfall-evaluation/footfall_evaluation/eval_utils/absolute_VTs_DELETE_LATER/test_config_europa.json" --footfall_version="ea40c617105bed78e5229c364ab1b195f0d4aec6" --footfall_datasets_version="more_rework_to_new_struct_changes" --name="europa_all" --dont_update --preview_length=50 -dit`