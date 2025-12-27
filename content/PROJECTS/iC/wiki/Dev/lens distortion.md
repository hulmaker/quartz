It is a form of optical aberration, that causes a deviation. Straight lines in a scene are not straight in the image. This can be corrected using the [camera calibration](https://docs.opencv.org/4.x/dc/dbb/tutorial_py_calibration.html) 

You, a fortunate reader may shout a loud hooray and throw the nearest person in air thrice as a means of celebration. It is because we already calibrated the cameras. You only have to check which lens does your camera use.

Currently, you can check your lens [here](https://icfootfall.sharepoint.com/:x:/s/Customers/EYcVh-VLXDhBuUrL0b-N8zgBz3747tsZU_VH-oDExYAHKg?e=aFwsov&clickparams=eyJBcHBOYW1lIjoiVGVhbXMtRGVza3RvcCIsIkFwcFZlcnNpb24iOiIxNDE1LzIzMDEwMTAwOTEzIiwiSGFzRmVkZXJhdGVkVXNlciI6ZmFsc2V9). 

Currently, the calibrations can be found in the [footfall camera calibration](https://gitlab.com/icsystemsai/footfall/-/tree/master/camera/calibration?ref_type=heads) folder, but I think they should be moved into the [camera geometry utils](https://gitlab.com/icsystemsai/tools/camera-geometry-utils) repository.

Using the [RectilinearCoordinateTransformer](https://gitlab.com/icsystemsai/tools/camera-geometry-utils/-/blob/main/camera_geometry_utils/camera/transformer_rectilinear.py?ref_type=heads) you can transition between all convert between all [[coordinate spaces]]


In this example we initialize the rectilinear coordinate transformer and undistort an image
```python
import camera_geometry_utils as cgu

# create a pinhole camera representation (may be usefull)
cam = cgu.camera.PinholeCamera.from_json("footfall/camera/calibration", camera_lens, camera_height)

# coordinate transformer from the cam object
tr = cgu.camera.RectilinearCoordinateTransformer(cam, None)

# or in one line:
 tr = cgu.camera.RectilinearCoordinateTransformer.from_calibration("footfall/camera/calibration", camera_lens, camera_height)

img = tr.undistort_img(np.array(Image.open("path").convert("RGBA")), crop=False)
```


Responsible person: Erik

