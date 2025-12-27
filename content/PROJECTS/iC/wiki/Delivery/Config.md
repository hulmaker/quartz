Update iC Client, update footfall (App version) - to musi byt pred tim nez se zacnou nastavovat

Ty senzory co zacnou byt online se musi automaticky updatovat iC Client i app version - takze pokud je senzor novy, tak by se mel automaticky SAM updatnout po tom co se pripoji

V kazdou chvili musi byt jasne co se dela, priletel mi pozadavek a musim se pidit co se ma udelat: https://app.clickup.com/t/86bw6mmep 

[recording s tomasem](https://icfootfall-my.sharepoint.com/:v:/g/personal/erik_icsystems_ai/EakKvhoKseVJoYViDyDdK7cBbotmV7b9pB5XrXrF3Z9ilg) - todo, vytahej z toho poznamky

Kazdy pozdavek stejny, Bez toho abych to musel zjistovat z kontextu musi byt jasne kdo to ma delat, co ma delat a musi tam mit vsechny informace.

Michal kulkovsky ma připsat senzor do cloudu - proč to není automaticky?

## Out of bounds:
09-Nov-23 16:12:47-1207 ERROR run_footfall_on_sensor.py:93 index 643 is out of bounds for axis 1 with size 640

Kdyz entrance nakreslim mimo obrazek, tak ff failuje - bud to nesmi monitoring dovolit, nebo se s tim musi ff vyporadat, clovek by to memel resit

## Configure at iC Cloud - chybna hlaska, je to na monitoringu
09-Nov-23 16:06:38-904 ERROR configs.py:26 Using a default camera config. Please configure the sensor at iC Cloud

## Form validation
* pomlcky misto podtrzitek u cocky - cocka by mela byt drop down menu
* Vyska - vyhodit defaultni vysku a nutit cloveka aby ji nastavil
* Senzory by. mely mit stavy - new (potrebuje kalibrovat), running (bezi ff, vse ok), defect, artefact, dead, nevim....


## Otazky:
* Kde zjistim lens? 
* Filip Bucek commented: Sensory mají nastavený přepínač default - který by měl být podle mě vypnutý. Nesmí to svítit červeně. === Proč tam teda je? Proč byl zapnutý a proč by se o to měl někdo při configu starat?
* Accept nerby je by default on, ale kdyz pridam novy entrance tak je off. Musite si vybrat a defaultne nastavit to co tam bude ve vetsine pripadu
* kdyz menim search na monitoringu tak musim dat refresh

## Camera Config
Typical structure is as follows:

```
camera:
  id: 0
  height: 2.63
  lens: MR_F0155IRST_12MP
camera_mask:
  - type: 1
    id: 0
    points: [{x: 98, y: 213}, {x: 108, y: 324}, {x: 260, y: 280}, {x: 273, y: 444}, {x: 500, y: 459}, {x: 482, y: 125}, {x: 268, y: 109}, {x: 265, y: 184}, {x: 121, y: 113}]
  - type: 2
    id: 0
    points: [{x: 107, y: 334}, {x: 94, y: 214}, {x: 122, y: 106}, {x: 258, y: 178}, {x: 271, y: 105}, {x: 331, y: 108}, {x: 342, y: 342}, {x: 259, y: 341}, {x: 254, y: 286}]
  - type: 2
    id: 1
    points: [{x: 261, y: 354}, {x: 353, y: 352}, {x: 343, y: 109}, {x: 487, y: 122}, {x: 508, y: 462}, {x: 266, y: 447}]
video:
  from_camera: true
  frame_step: 1
  subsample: 1
  camera_fps: 5
  exposure_value: -0.5
```

- Default lenses are MR_F0155IRST_12MP #TODO: ste a process to get info when a given sensor has different lens. Camera height is a distance from lenses to the ground.
- camera_mask is set using drawing tool. For each item of type: 2 there can be also corrections set. 
    - female_prior: 0.92 # range 0 1
    - age_priors: [0.13, 0.25, 0.45, 0.17]
    - gender_bias:  # range -0.5, 0.5

- video - only value to modify here is exposure_value which can go from -8 to 8. Default is 0. When set to +1 the image will be brighter.