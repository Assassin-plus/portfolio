---
title: WaterLOD
summary: A continuous Level of Detail (LOD) method for billion-scale fluid particle rendering. The bachelor thesis project at the Tsinghua University.
tags:
  - Computer Graphics
  - Rendering
featured: true
date: '2025-06-09T00:00:00Z'

# Optional external URL for project (replaces project detail page).
external_link: ''

url_code: ''
url_pdf: ''
url_slides: ''
url_video: ''

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---
With the progress of computer-aided simulation research, there's an increasing demand for large-scale 3D fluid simulation in geotechnical and hydraulic fields. These fields require processing large-scale, high-precision fluid simulation data. However, traditional visualization technologies have limitations including low efficiency, poor reality and lack of intuitiveness. At the same time, the promising application prospect of currently popping technologies such as Virtual Reality and Augmented Reality require development of photo-realistic scene fluid visualization.

Therefore, this study concentrates on the photo-realistic scene visualization of large-scale fluid particle data, aiming to rapidly and interactively visualize particle data at around hundred-million level. This study first introduces the continuous level of detail technique into the field of fluid particle data through in-depth observation of input data characteristics to reduce performance waste; At the same time, by monitoring hardware performance, intelligent preloading of future frames of fluid animation can improve the smoothness of video rendering. The core of this study is to develop on the vtkOpenGLFluidMapper class in VTK's OpenGL extension. By applying the continuous level-of-detail technology and the future frame pre-loading and transmission optimization technique, it establishes an efficient fluid particle data scene visualization method, and implemented a prototype system to validate the feasibility and superiority of the algorithm. The research improves the efficiency of authenticity visualization without significantly compromising visual effects.
