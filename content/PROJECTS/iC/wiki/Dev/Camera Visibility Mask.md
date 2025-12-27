Using the [GlobalCoordinateTransformer](https://gitlab.com/icsystemsai/tools/camera-geometry-utils/-/blob/main/camera_geometry_utils/global_coordinate_transformer.py?ref_type=heads) it is possible to create a camera visibility mask. It is an area of the plan that is covered by a specific sensor. Using this, you can obtain camera intersections, unions, etc...

This can be useful during the [[image registration]] phase. 

Potentially, we can create a tool that can visualise sensor installation plan. Given a set of camera lenses, heights and positions, it is possible to roughly estimate the space coverage.

# Examples

### Get an intersection of two visibility masks. Project them into plan
```python
mask1 = gtf.visibility_mask('rel-101', plan.shape[:2])
mask2 = gtf.visibility_mask('rel-103', plan.shape[:2])

intersection = mask1 & mask2

visu = gtf.project_visibility_mask_into_plan(intersection, plan, color=(100, 100, 0, 100))
plt.imshow(visu)
```
### Project two visibility masks into plan, use different color
```python
visu = gtf.project_visibility_mask_into_plan("rel-101", plan, color=(0, 100, 0, 100))
visu = gtf.project_visibility_mask_into_plan("rel-103", visu, color=(100, 0, 0, 100))
plt.imshow(visu)
```

### estimate how many cameras can see each pixel
```python
masks = [gtf.visibility_mask(cam, plan.shape[:2]) for cam in gtf.homography.camera]
# value on ij corresponds to the number of cameras that can see the pixel ij in the plan
pixel_occupancy = np.sum(masks, axis=0)
plt.imshow(pixel_occupancy/pixel_occupancy.max())
```