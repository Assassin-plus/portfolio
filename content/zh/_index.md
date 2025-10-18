---
# Leave the homepage title empty to use the site title
title: ''
date: 2025-10-14
type: landing

design:
  # Default section spacing
  spacing: '6rem'

sections:
  - block: resume-biography-3
    content:
      # Choose a user profile to display (a folder name within `content/authors/`)
      username: admin
      text: ''
      # Show a call-to-action button under your biography? (optional)
      button:
        text: 下载简历
        url: uploads/resume-zh.pdf
      headings:
        about: ''
        education: ''
        interests: ''
    design:
      # Apply a gradient background
      css_class: hbx-bg-gradient
      # Avatar customization
      avatar:
        size: medium # Options: small (150px), medium (200px, default), large (320px), xl (400px), xxl (500px)
        shape: circle # Options: circle (default), square, rounded
  - block: experience
    id: experience
    content:
      username: admin
    design:
      # Hugo date format
      date_format: 'January 2006'
      # Education or Experience section first?
      is_education_first: false
  - block: skills
    content:
      title: 技能与兴趣
      username: admin
    design:
      columns: '1'
  - block: collection
    id: papers
    content:
      title: 论文
      filters:
        folders:
          - publication
        featured_only: true
    design:
      view: article-grid
      columns: '1'
  - block: collection
    content:
      title: 最近发表
      text: ''
      filters:
        folders:
          - publication
        exclude_featured: false
    design:
      view: citation
  - block: collection
    id: project
    content:
      title: 个人项目
      subtitle: ''
      count: 5
      # Display content from the `content/post/` folder
      filters:
        folders:
          - project
        featured_only: true
    design:
      # Choose how many columns the section has. Valid values: '1' or '2'.
      columns: '2'
      # Choose your content listing view - here we use the `showcase` view
      view: showcase
      # For the Showcase view, do you want to flip alternate rows?
      flip_alt_rows: true
  - block: languages
    content:
      title: 语言
      username: admin
---
