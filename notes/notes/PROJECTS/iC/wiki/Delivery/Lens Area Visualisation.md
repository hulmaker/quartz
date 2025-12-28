You can simulate different lenses field of view on sensors with wide lens.
Detailed information in ClickUp: https://app.clickup.com/t/86byrt89u

To simulate 828 on F155, update config to:
```YAML
camera:
  id: 0
  height: 2.6
  lens: MR_F0155IRST_12MP
camera_mask:
  - type: 1
    id: 0
    points: [{x: 150, y: 118}, {x: 145, y: 240}, {x: 150, y: 355}, {x: 310, y: 363}, {x: 470, y: 355}, {x: 475, y: 240}, {x: 470, y: 118}, {x: 310, y: 110}]
video:
  from_camera: true
  frame_step: 1
  subsample: 1
  camera_fps: 5
```


To simulate 824 on F155, update config to
```YAML
camera:
  id: 0
  height: 2.6
  lens: MR_F0155IRST_12MP
camera_mask:
  - type: 1
    id: 0
    points: [{x: 150, y: 118}, {x: 145, y: 240}, {x: 150, y: 355}, {x: 310, y: 363}, {x: 470, y: 355}, {x: 475, y: 240}, {x: 470, y: 118}, {x: 310, y: 110}]
video:
  from_camera: true
  frame_step: 1
  subsample: 1
  camera_fps: 5
```

! Don't forget to update the height!!