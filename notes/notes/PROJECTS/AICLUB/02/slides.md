%%
Sources:
[Lex friedman slides on MIT](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbDFTOGR4b3RaZkhxNlFMd0FmVVVyX0dnbmoxQXxBQ3Jtc0ttLXcwTnNDRFY1S3l3aVRxSDh1TWVXMncxUXUwdU40ZUd6b25rLW9GN2ZKV0VMUjFGZjh1ZVk5QmFzemJWaG5CWkZxa2thaHhXMnFIcUh1eW5GMW43cUVjam9tRHpROGJNYnpfUUFRcmhoUDctd25QOA&q=http%3A%2F%2Fbit.ly%2F2HdjksA&v=CLOAswsxudo)
[MIT intro to dep learning](http://introtodeeplearning.com/)
%%
## AIClub 02
uvodni slide, titulek
Představení, email atd... Nepotřebuješ svůj slide

---

# Concept
60 min talk + discussion
next session in 2 months

### Goals
proc to je takovouhle formou, co musi delat v prubehu te lekce atd...

---

# Computer Vision is Deep Learning
Basically every field of computer vision has been overtaken by convolutional neural networks, vision transformers etc...

---
# Images are Numbers
Fotka s yllem, to co jsem si sepisoval v planning, tim se dostanu k dalsimu slidu

---

# Computer Vision is Hard
Člověk: kouknu a vidim, mám model a porozumění světa a silnou intuici
Počítač toto nemá.
Lightning changes, position changes...
Illumination variability: Fotka s panem co je osviceny
Intra-class variability: Fotka s chlupatym psem a čivavou
Occlusion
Blurr

---

# CNN's are Inspired by human brain
Visual cortex inspiration for cnn
[brain diagram](https://www.frontiersin.org/articles/10.3389/fncom.2014.00135/full)
[Levels of features](https://res.cloudinary.com/dry8rzbyx/image/fetch/s--5KJraWhB--/f_auto/q_auto/c_scale,w_1536/https://www.knime.com/sites/default/files/public/5-computer-vision-codeless-cnn.png)
(dej to do kontextu, je to stejne s mozkem a i CNN)

Hierarchical, feedforward visual processing. Stimuli are processed in a series of visual areas. V1 neurons are most sensitive to low-level features, such as edges and lines. In higher visual areas, like V4 and IT, receptive fields are larger, and neurons are sensitive to complex features, such as shapes and objects. Responses of high-level neurons are fully determined by the neural firing of lower-level neurons. For example, the neural firing to a square is determined by the neural firing for two vertical and two horizontal lines.


---

# Classification

[MNIST - NN 2D visu](https://adamharley.com/nn_vis/cnn/2d.html)
[classification demo - upload](https://huggingface.co/spaces/hasibzunair/image-recognition-demo)

---

# Detection
[demo](https://cloud.google.com/vision/docs/drag-and-drop)

---
# Segmentation
[segment anything](https://segment-anything.com/) - does not explain the segmentation
[COCO example in fiftyone](https://try.fiftyone.ai/datasets/try-coco/samples)

---

# Image stitching
[Image retrieval](https://ssl-demos.metademolab.com/retrieval/openimages/RetrievalResults?query_image=https%3A%2F%2Fc8.staticflickr.com%2F9%2F8160%2F7631552054_4437c13db1_z.jpg)
[3D reconstruction from 2D images](https://www.youtube.com/watch?v=DIv1aGKqSIk)

1. udelej ukazku
2. Ukaz obrazky bez niceho
3. spust detekci bodu
4. Any ideas how to find correspondences in a setting where there are so many noise detections?
5. Who knows the RANSAC algorighm?
```bash
cd /Users/erik/code/mpv-notebooks/RANSAC
source venv/bin/activate
jn
# then open ransac planar
```


---

Super resolution
Blur removal
Noise reduction
depth estimation: https://huggingface.co/spaces/LiheYoung/Depth-Anything

---

Similarity learning, deep metric learning

---

object tracking, SLAM?

---

# Image Generation
stable diffusion vs. GANs - usecasses, differences
[text to video synthesis](https://huggingface.co/spaces/ali-vilab/modelscope-text-to-video-synthesis)
[change hairstyle](https://huggingface.co/spaces/Gradio-Blocks/HairCLIP)
[understand and reason about images](https://build.nvidia.com/microsoft/microsoft-kosmos-2) - fotka s kriket players, otazka: What is the dog doing in the image?