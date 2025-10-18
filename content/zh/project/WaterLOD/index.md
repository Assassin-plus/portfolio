---
title: WaterLOD
summary: 一种用于十亿级流体粒子渲染的连续细节层次（LOD）方法。清华大学的学士论文项目。
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
# WaterLOD摘要
随着计算机辅助模拟研究的进展，岩土工程和水力领域对大规模三维流体模拟的需求越来越大。这些领域需要处理大规模、高精度的流体模拟数据。然而，传统的可视化技术存在效率低、真实性差、缺乏直观性等局限性。同时，虚拟现实和增强现实等当前流行技术的广阔应用前景要求开发照片级逼真的场景流体可视化。 

因此，本研究专注于大规模流体粒子数据的照片级逼真场景可视化，旨在快速、交互式地可视化数亿级左右的粒子数据。本研究首先通过对输入数据特征的深入观察，将连续细节技术引入流体颗粒数据领域，以减少性能浪费；同时，通过监控硬件性能，智能预加载未来的流体动画帧可以提高视频渲染的平滑度。本研究的核心是在VTK的OpenGL扩展中开发vtkOpenGLFluidMapper类。通过应用连续细节层次技术和未来帧预加载和传输优化技术，建立了一种高效的流体粒子数据场景可视化方法，并实现了一个原型系统，以验证该算法的可行性和优越性。该研究在不显著影响视觉效果的情况下提高了真实性可视化的效率。
