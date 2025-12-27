to create mp4 video the old way
----------------------

`python -m footfall_datasets.video.create_videos_and_timestamps_from_images --video_path="/data/footfall/datasets/videos_mp4_crf15" --imgs_path="/data/footfall/datasets" --create_timestamps --n=1 --mode="datasets" --datasets="str-001_2023-08-30_13h" --crf="15"`


the new way (paths)
---------------------

repo: `footfall-datasets`
branch: `reworking_export_to_new_struct_23` (should be merged in main soon)
`python -m footfall_datasets.video.create_videos_and_timestamps_from_images --recording_folder="/data/footfall/datasets/videos/PetCentrum/pet-588/data/2023-09-12-1421/" --create_timestamps --n=1 --crf="15"`

# Responsibilities
[[Martin Koucky]]




another_example -- multiple folders:
--------------


`python footfall_datasets/video/create_videos_from_images.py --recording_folder="/data/footfall/datasets/videos/BoryMallSK/bma-001/data/2023-10-09-1700/,/data/footfall/datasets/videos/BoryMallSK/bma-002/data/2023-10-09-1700/,/data/footfall/datasets/videos/BoryMallSK/bma-002/data/2023-10-10-1100/,/data/footfall/datasets/videos/BoryMallSK/bma-001/data/2023-10-10-1100/"`