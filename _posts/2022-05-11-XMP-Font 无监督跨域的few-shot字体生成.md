---
layout: post
title: XMP-Font：无监督跨域的few-shot字体生成
---

![image-20220512233100855](https://raw.githubusercontent.com/294coder/blog_img_bed/main/imgs/image-20220512233100855.png)

介绍视频：[CVPR2022 XMP-Font 哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1qY4y1b7Mh?spm_id_from=333.1007.top_right_bar_window_view_later.content.click)

paper：[https://arxiv.org/abs/2204.05084](https://arxiv.org/abs/2204.05084)

> 学那么多理论，还是需要看下在工业界是咋用的，以及对应的task有什么trick。

# 简介

作者设计了一个**自监督预训练方法**和一个跨域的**依赖于字符图像和对应笔画的表情的encoder**（transformer-based），可以在few-shot的情况下，生成质量很好的中文字体。

# 方法

## 阶段一 跨域的encoder

输入分别是两个模态，一个是字形，一个是随机mask的笔画。字形被embed成三部分，分别是feature、position和一个指示模态的indicator(文中写为modality)；笔画也被embed成三部分，分别为stoke、order index和modality。

对于笔画来说，28个笔画就足以构成常用的中文字体，所以每个笔画会对应有一个label，这样经过embedding layer之后就成为512维的stroke label embedding。在构成一个字的时候，每个笔画是有顺序的（从上到下，从左到右），所以对应笔画的顺序会有一个position embedding。剩下的modality embedding为了指示是哪一个模态。

对于字形来说，输入为$256\times 256\times 3$的图像，经过5层卷积层之后成为$8\times8\times 512$的feature map。



