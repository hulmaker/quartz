In our setup, we often need to switch between multiple coordinate spaces. A good explanation of how the pinhole camera works is in the [Kornia documentation](https://kornia.readthedocs.io/en/latest/geometry.camera.pinhole.html)

![[coordinate_transformer.svg]]
Figure depicts the transformation between coordinate systems, with each arrow representing one method in our CoordinateTransformer. The Image-space corresponds to video stream images. With camera calibration, it is possible to correct the distortion and transition to the Camera frame. The inverse distortion for the Camera and World is done using a reference rectify map. A perspective transformation describes the transition between cameras. An inverse perspective transformation is feasible with the knowledge of scene depth, which is crucial for generating synthetic data in shared world space.


---


All described transformations can be done using the [GlobalCoordinateTransformer](https://gitlab.com/icsystemsai/tools/camera-geometry-utils/-/blob/main/camera_geometry_utils/global_coordinate_transformer.py?ref_type=heads). If you don't need to use homography and projection into a floor plan, you can use the [RectilinearCoordinateTransformer](https://gitlab.com/icsystemsai/tools/camera-geometry-utils/-/blob/main/camera_geometry_utils/camera/transformer_rectilinear.py) How to register cameras, remove distortion and obtain all necessary configs is described in the [[image registration]] page.


### Image
Distorted image captured by the camera.

### Camera
Undistorted image where straight lines in the scene appear straight in the image. Can be corrected using the [[lens distortion]]


### World
Projected 2d camera coordinates to the world frame. You can do this with an inverse pinhole camera projection locked at certain depth. The coordinates are then projected onto a plain that is orthogonal to the camera optical axis. The units are in meters. You can read about it more here: https://kornia.readthedocs.io/en/latest/geometry.camera.pinhole.html


### Plan
Shared coordinate space with multiple registered cameras. Can be done with the [[image registration]] tool. This space is not yet part of the coordinate transformer.


> [!info]
> The names does not have to correspond to names in the image registration tool


Responsible person: Erik
