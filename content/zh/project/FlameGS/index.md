---
title: FlameGS
summary: 一个完整的面部重建流程，用于从单目或多目视频中重建逼真的面部网格、纹理和动画,增强了Avatar在各种应用中的真实感和多样性。
tags:
  - Computer Graphics
  - Reconstruction
  - Simulation
featured: true
date: '2024-09-08T00:00:00Z'

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
# Reconstructing Detailed Facial Mesh from Monocular or Multicam Videos

July 2024 - Sept. 2024

在犹他大学杨垠教授指导下的实习.

* 开发了一套全面的推理流程，从单目或多摄像机视频源重建照片级逼真的面部网格、纹理和动画，增强了虚拟角色在各种应用中的真实感和实用性
* 将FLAME可微分参数化人脸模型与高斯溅射法相结合，以高效捕捉极端数据分布下的面部特征
* 针对网格和高斯混合的Avatar表示，制定了一种传输算法，以便进一步模拟人脸运动。在表情、姿势和视角方面完全可控且用户友好
* 与最先进的方法相比，实现了相当的图像相似性和多视图一致性，同时生成了时间上更平滑的姿势和表情动画

## Copyright

Header image copyright: [GaussianAvatars](https://shenhanqian.github.io/gaussian-avatars) by Technical University of Munich
