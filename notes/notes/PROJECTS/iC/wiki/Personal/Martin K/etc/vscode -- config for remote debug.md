
**ff-eval example**
--------------------------




{

    "version": "0.2.0",

    "configurations": [        

        {

            "name": "Python: Module",

            "type": "python",

            "request": "launch",

            "python": "/home/icsadmin/miniconda3/envs/ffeval/bin/python3",

            // "module": "pipelines.compute_detections_for_some_datasets",

            "module": "vt_pipeline_class_based",

            "cwd": "${workspaceFolder}/footfall_evaluation",

            "justMyCode": true,

            "env": {

                "VIDEO": "0",

                "commit": "martin_mp4_experiments_images",

                "DATASETS_PATH":"/data/footfall/datasets/",

                "CACHE_PATH":"/epsilon/TRACKING_CHECKPOINTS/martin_mp4_experiments_images/",

                "PROPOSER_CACHE_PATH":"/epsilon/TRACKING_CHECKPOINTS/martin_mp4_experiments_images/proposer",

                "PYTHONPATH":"src"

              },

              // "args": ["--dataset_names_path=\/epsilon\/data\/datasets_mp4"]

              "args": ["--json_config=\/epsilon\/vt_configs\/OCSestka_2024-04-15-1600_fixed_camc.json", "--name=2.4.14__OCSestka__2024-04-15-1600", "--footfall_version=2.4.14", "--footfall_datasets_version=more_rework_to_new_struct_changes_2", "--user=martin", "--project_id=13", "--stages=10", "--dont_update", "--dont_fix_stages"]

        }

    ]

}


