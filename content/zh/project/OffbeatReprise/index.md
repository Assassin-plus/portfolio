---
title: 错节复奏
summary: 结合了节奏游戏的2.5D子弹时间射击游戏，米哈游策划大赛参赛作品
tags:
  - Video Games
featured: true
date: '2025-11-13T00:00:00Z'

# Optional external URL for project (replaces project detail page).
external_link: 'https://assassin-plus.itch.io/offbeat-reprise'

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
# 错节复奏

我作为开发承担了除了游戏策划和关卡设计以外的所有部分，包括程序开发、资产和音效制作。

值得一提的是，在策划提出了“子弹时间配合玻璃破碎的物理模拟”这一需求之后，我尝试实现的原型版本遭遇了严重的性能问题。我深入unity的调用栈分析，最终找到了性能瓶颈在于物理模拟模块的创建和销毁，并在房间地形的移动中参与了模拟过程，而这是不需要的。因此我将玻璃碎片于游戏启动时预先创建，并在地形改变时暂时冻结碎片参与物理模拟的“权限”，从而解决了性能问题。