---
layout: post
title: XMP-Font：无监督跨域的few-shot字体生成
---

![image-20220512233100855](https://raw.githubusercontent.com/294coder/blog_img_bed/main/imgs/image-20220512233100855.png)

# 简介

作者设计了一个**自监督预训练方法**和一个跨域的**依赖于字符图像和对应笔画的表情的encoder**（transformer-based），可以在few-shot的情况下，生成质量很好的中文字体。



