---
title: Offbeat Reprise
summary: Side-scroller bullet-time shooter game developed in Unity. Worked as everything except game and level design
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
# Offbeat Reprise
As a developer, I was responsible for all aspects of the project except for game design and level design, including programming, asset creation, and sound design.

Notably, after the designers proposed the feature of “bullet time combined with physically simulated glass shattering,” the initial prototype I implemented suffered from severe performance issues. By analyzing Unity’s call stack in depth, I identified the performance bottleneck as the repeated creation and destruction of physics simulation objects, as well as the unnecessary participation of glass fragments in the simulation during room geometry movement. To address this, I pre-created the glass fragments at game startup and temporarily disabled their participation in the physics simulation when the environment changed. This optimization successfully resolved the performance problem.