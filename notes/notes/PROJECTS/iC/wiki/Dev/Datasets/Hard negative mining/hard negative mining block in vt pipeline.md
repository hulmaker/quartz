# Hard Negative Mining block in VT pipeline

Introduced in [GitLab commit link](https://gitlab.com/icsystemsai/products-evaluation/footfall-evaluation/-/commit/c242f753b70835693226a8184fcda21d66e6e65d).

## General idea:
- When running VT pipeline, adding this block (currently numbered 12) detects all FP (Detection object) and FN (Track / Annotation object), samples the current frame (in which the failure is detected) and extra frames around the failure point.
    - FP can happen at any time during the video, so we currently sample both before and after the FP was first detected.
    - FN on the other hand is currently Annotation when the person leaves the frame, so we sample before the frame, to capture when he is still in the frame.
- These frames are by default saved to the VT_folder/hard_negative_mining, together with db.json, containing info about all saved frames, including the Detection/Annotation data.
    - The structure of this db.json is further described in db_desc.txt for easy future reference.
- Symlinks to all hard_negative_mining folders are created by default in /epsilon/hard_negative_mining_all.

## Implementation
- class BlockHardNegativeMining - wrapper
- class NegativeMiningPipeline  - actually interesting part
    - Args:
        - output_path: Where to save the hard_negative_mining folder with outputs. By default set to the VT's output_path.
        - aggregation_path: For every VT with its own hard_negative_mining folder, create symlinks to these in a centralized folder (currently gauss:/epsilon/hard_negative_mining_all). This folder should have iClab group, so that all users can run the hard negative mining pipeline without issues. If the path is set to None, no aggregation is performed.
        - tracking_algorithm: By default, set to "rfc_prasator".
        - show_frame_ids: Will draw frame number into each saved frame. Useful for debugging purposes.

### Naming of the output frames
- `{current_video_name}_FN_{frame_id}.jpg` for FN frame where the FN was detected.
- `{current_video_name}_FN_{frame_id}_extra.jpg` for frames sampled around a detected FN.

### Sampling of extra frames
- Currently we sample based on frame rate, in half second intervals around the detected FP/FN.
- For FP, we sample 0.5/1 second both before and after the frame of detection.
- For FN, we sample 0.5/1 second before the frame of annotation.
- These can be modified - `sample_frames_around_FP()` and `sample_frames_around_FN()` functions.

### Future improvements
- Smarter sampling
    - Time intervals could be modified based on the height of camera and average speed of person in the scene.
- Sampling throughout entire track
    - Track would have to be returned from `extract_important_frames_from_vt()` instead of frame.
- Sharpness detection
    - Some of the sampled frames are blurry. We could implement a threshold at which we could check frames before/after for better sharpness.
    - Either gradient amplitudes or FFT high freq analysis as baseline?

## DB.json
```
The db.json file contains the following structure:
sensor/                                             # eg. "knb-002"
└── video_file/                                     # eg. "videos_knb-002_knb-002_2024-04-25-0600_14h.mp4"
    ├── input/                                      # dict
    │   ├── ds_path                                 # eg. "/data/footfall/datasets/videos_v1/Knorr_Bremse/knb-002/videos/knb-002_2024-04-25-0600_14h.mp4"    
    │   ├── cam_conf_pat                            # eg. "/epsilon/default_configs/knb-002.yaml"
    │   ├── annots_path                             # eg. "/epsilon/annotations/CVAT_with_areas_counts/videos_knb-002_knb-002_2024-04-25-0600_14h.mp4.json"
    │   ├── annots_type                             # eg. "DB"       
    │   └── name                                    # eg. "videos_knb-002_knb-002_2024-04-25-0600_14h.mp4"
    ├── tracking_cache_path                         # eg. "/epsilon//VTs/2.4.14__Knorr_Bremse__knb-002//tracking/rfc_prasator/videos_knb-002_knb-002_2024-04-25-0600_14h.mp4.pkl"
    └── output/                                     # dict    
        ├── FP_original_frame_ids                   # array of frame ids where false positives were detected
        ├── FN_original_frame_ids                   # array of frame ids where false negatives were detected        
        ├── FP_sampled_frame_ids                    # array of frame ids that were sampled from the video        
        ├── FN_sampled_frame_ids                    # -||-
        ├── FP_sampled_extra_frame_ids              # array of only the extra frame ids that were sampled from the video       
        ├── FN_sampled_extra_frame_ids              # -||-
        ├── FP_by_frame/                            # dict        
        │   └── frame_id/                           #         
        │       └── detection                       # detection object from detector            
        ├── FN_by_frame/                            # dict   
        │   └── frame_id/                           #    
        │       └── annotation                      # annotation object from VT   
        ├── FP_sampled_frame_filenames              # array of filenames of sampled frames               
        └── FN_sampled_frame_filenames              # array of filenames of sampled frames
```