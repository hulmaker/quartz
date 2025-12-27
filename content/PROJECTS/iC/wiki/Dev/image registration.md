**Image registration** is the process of transforming different sets of data into one coordinate system. Data may be multiple photographs, data from different sensors, times, depths, or viewpoints.

The [image registration tool](https://gitlab.com/icsystemsai/tools/image-registration) uses two methods. The first one allows user to stitch two images and provides a high quality homography. The second "by vočko" method is for those who like pain and should be used only if the first one fails. The main page is going to ask you for the camera lens and camera height. If you provide these for all registrations, you can load the global coordinate transformer form a single file. I strongly recommend filling both.

> [!danger]
> You might want to remove the [[lens distortion]] first. In the future, we can implement automatic undistort when you submit the camera lens and camera height.

To generate a config, do:
```bash
git clone git@gitlab.com:icsystemsai/tools/image-registration.git

# (for someone) docker-compose up (otherwise)
docker compose up
```

> Make sure the camera image is **SOURCE** and the plan image is **DESTINATION**!! Otherwise you just made an inverse homography and you would have to invert the matrix.

The app will then run at [localhost:8000](localhost:8000)

> [!warning]
> The app is still unfinished. Both methods work, but the export is still too bulky and a script that can combine multiple registrations into one will definetly be available soon.
> Also the pop-up warning about unsaved changes is hardcoded. Read about things that need to be done in the repository [README.md](https://gitlab.com/icsystemsai/tools/image-registration)


# Homography Config

This config can be created using: `script/merge_exports.py` - this script merges multiple exports into a single homography config.
```bash
python -m merge_exports --dir="/export/dir" --outfile="name_YYYY-MM-DD.json" --filename "extra_export.json" "other_export.json"
```

Each homography config groups sensors that share the same plan coordinate space. If you read two configs, they are seen as covering different coordinate spaces. If a camera changes, create a new config and update only the registration for the changed camera. Sensors that are registered are stored in homography configurations in the following format: 
```json
{
    "plan": "/Users/erik/code/image-registration/temp/big_plan.jpg",
    "note": "Krakov - ground floor",
    "created": "2023-09-15",
	"camera": {
		"kra-151": {
			"homography": [[1, 0, 0], [0, 1, 0], [0, 0, 1]],
			"manual_adjustment": None,
			"camera_height": 4.0,
			"camera_lens": "MR_F0155IRST_12MP",
		},
		"kra-107": {
			"homography": None,
	        "manual_adjustment": [
	            [1.0091583728790283, 0.02790956012904644, 1754.171142578125],
	            [-0.02790956012904644, 1.0091583728790283, 834.4577026367188 ],
	            [0.0, 0.0, 1.0]
	        ],
			"camera_height": 6.4,
			"camera_lens": "MR_F0155IRST_12MP",
		},
	}
}
```


These configs are then stored in [footfall_datasets/homography](https://gitlab.com/icsystemsai/research/footfall-datasets)
