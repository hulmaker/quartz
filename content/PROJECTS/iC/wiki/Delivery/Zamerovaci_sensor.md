# Zaměřovací sensory ( koště )

- [koste2-824](https://monitoring.ic-systems.ai:4001/app/ui/device/c125ce35-3760-4541-9c35-d0fc9056dc44)
- [koste2-155](https://monitoring.ic-systems.ai:4001/app/ui/device/0eb828c1-a1cc-4e01-8d59-4e3ae82c1740)
- [koste1-155](https://monitoring.ic-systems.ai:4001/app/ui/device/7d81e5ef-c7f2-4a62-a849-0146d96dd226)


# Pomocné vizualizace:
Task: https://app.clickup.com/t/86byrt89u

Camera config lze využít k zobrazování zajímavých oblastí.
Zaměřovač si může na širokoúhlém objektivu vizualizovat co by viděl objektiv s užší čočkou.
Pokud je na koštěti užší čočka, pak logicky nelze zobrazit oblast širší.

J02824 vidí oproti F0155 ( wide ) pouze toto
```
poly_pts_xy = np.array([
    [150, 118], [145, 240], [150, 355], 
    [310, 363], [470, 355], [475, 240],
    [470, 118], [310, 110]
])
```

### Konfig pro F0155 s vizualizovanou oblasí J02824

```
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

### Konfig pro F0155 s vizualizovanou oblasí J02824 + J02828


```
camera:
  id: 0
  height: 3
  lens: MR_F0155IRST_12MP
camera_mask:
  - type: 1
    id: 0
    points: [{x: 90, y: 75}, {x: 70, y: 250}, {x: 90, y: 400}, {x: 200, y: 430}, {x: 320, y: 440}, {x: 440, y: 430}, {x: 540, y: 400}, {x: 560, y: 250}, {x: 530, y: 70}, {x: 440, y: 50}, {x: 320, y: 35}, {x: 200, y: 50}]
  - type: 2
    id: 1
    points: [{x: 150, y: 118}, {x: 145, y: 240}, {x: 150, y: 355}, {x: 310, y: 363}, {x: 470, y: 355}, {x: 475, y: 240}, {x: 470, y: 118}, {x: 310, y: 110}]
    accept_nearby: false
video:
  from_camera: true
  frame_step: 1
  subsample: 1
  camera_fps: 5
```
