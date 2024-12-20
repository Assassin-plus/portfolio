---
title: Contrast Adjustments
subtitle: 
# Summary for listings and search engines
summary: Basic Color Grading Tools in Davinci Resolve
# Link this post with a project
projects: []

# Date published
date: '2023-07-27T00:00:00Z'

# Date updated
lastmod: '2023-07-27T00:00:00Z'

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.

authors:
  - Zi-Qi Lu

tags:
  - Digital Arts
  - 开源

categories:
  - Tutorial
  - 教程
---
# 调整反差的工具

LIFT GAMMA GAIN

* Lift: 调整趾部
* Gamma：更改中间调的分布
* Gain：调整高光

Contrast & Pivot

Contrast：线性地改变图像的黑白位
Pivot：分配Contrast在黑位白位之间区域的权重

## Y'CbCr/RGB下的LUMA调整

> 大多数调色系统的一级反差控制使用RGB图像处理方式，即调整图像亮度时，是对所有三个色彩分量进行等量且同步调整的。由此产生的调整，会对图像饱和度产生明显影响。
> 单独操控Y'CbCr的Y通道，对图像的饱和度没有可测量的效果（即矢量波形保持不变）。然而，图像的感知饱和度确实有改变。

# 用LOG调色控件微调反差

## 使用OFFSET、EXPOSURE和CONTARST微调反差

在套用LUT之前使用这些控件！
这样可以控制图像反差并找回一些图像细节，因为可能在套用LUT时会被裁切

## 使用SHADOW、MIDTONE和HIGHLIGHT微调反差

他们被设计为用于log素材正常化之前的调整

这些控件对图像的影响完全取决于图像本身有多少反差。
Shadow：影响影调的底部三分之一
Midtone：影响范围广泛的中间调
Highlight：影响高光的顶部三分之一

# 设置适当的高光和暗部

> 对高光的感知与阴影的深度有关。某些时候压低阴影而高光保留不动比提高高光更好。

## 保持中间调的同时将白位合法化

压低Gain的同时将中间调提高以补偿影响，也可以通过降低一点暗部来保持反差。

## 尝试用降低中间调替代压低暗部的操作

不是每个图像都要求把暗部压到0%，有时候降低中间调可以达到相同的效果。

# 反差和视觉感知

## 利用环境效应

提高高光令阴影看起来更暗，同时尽量避免平均中间调看起来比原来更亮。

* 提高Gain
* 为了减少图像的感知亮度，降低Gamma。这导致高光减少了一点，但是上步中提起高光幅度很大，不会有太大影响
* 降低中间调的同时阴影降低的有点太多，提高Lift作为补偿

## 增加图像感知锐度

调整反差的另一个效应：增加对比度可以让画面细节变得更锐。

# 如何处理曝光问题素材

## 曝光不足

试图增加亮度和中间调时，通常：

* 会增加噪点
* 饱和度过高/欠饱和
* 暗部细节不足

> 提高中间调比调整白位更好

使用曲线控制器，将中间调偏低区域伸展，同时保持中间调偏上的区域不变以获得扎实的阴影。

## 过曝

先做取舍：是否需要压过曝部分

如果过曝面积不太大：

### 为过曝区域添加颜色

* 降低Gain，将高光合法化
* 如果有需要，用Gamma提高中间调
* 使用HSL选色的Luma控件
* 将Gain推向某种颜色，即补色

### 为过曝区域添加辉光

若夸张的过曝不能避免，光晕和溢出可以软化过渡区域的边缘，也能让画面更加舒服

* 降低Gain，将高光合法化，同时提高Gamma补偿
* 使用HSL选色的Luma控件分离出过曝区域
* 使用HSL选色中的Blur或Soften，模糊键控蒙版，最终要令蒙版比曝光过度的区域更大，边缘更柔软
* 用Lift或Gamma来提亮选中的键控区域，类似晕染和溢出会逐渐出现。

### 使用通道混合器重建被裁切的通道

由于显著过曝而造成的某个通道分配不均，导致难看的图像高光。检查RGB分量示波器，如果某个通道远高于110%，但是其他通道都没有，那么可以使用这类方法。

> 这是最后的方法，目的是找回更多图像数据而不是让图像更漂亮。

* 调整色彩和反差，达到色彩平衡（一级校色），先别担心裁切位置，只需要进行整体校正。在这种情况下，offset来重新编排三个色彩通道的位置，先降低红色通道，再使用“Master Offset”来降低整体图像信号，使图像阴影密度更多
* 创建新节点进行通道修复。这次调整所作的校正将要放在之前的校正上。也即使用Layer Mixer
* 选择新节点，检查哪个通道在被裁切的区域内有更多的细节。
* 使用 RGB Mixer / Channel Blending / Channel isolation / Blend mode来混和绿色与蓝色通道给红色通道。
* 使用Luma限定控件分离出过曝高光区域，然后柔化边缘并使用该键控蒙版来限制通道混合的影响范围。
* 最后添加额外的校色操作，整体图像进行调色
