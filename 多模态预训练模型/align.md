# 笔记

## 标题与小结

title：Scaling Up Visual and Vision-Language Representation Learning With Noisy Text Supervision
标题: 通过嘈杂的文本监督来扩大视觉和视觉语言表示学习

小结

## 摘要

nlp领域内很多学习已经过度到对原始文本的训练，不需要人工注释。vision和vision-language仍然严重依赖精心标注的数据集。

ALIGN利用了一个超过10亿个图像和文本的视觉和语言表示，没有经过昂贵的过滤或后处理步骤就获得。使用对比学习来对齐图像和文本的视觉和语言表示。

## 介绍和相关工作

1. 迁移学习很重要，但是对数据集质量要求很高
2. vision-language数据集比nlp数据集小很多
3. 本文使用双流结构对齐了视觉和语言表示（visual-semantic embeddings，vse）
4. 过去的vse方法以及跨模态注意力都太慢了，无法用于现实都学习
5. align和clip的不同，align不对数据去噪，clip是专家系统收集的数据集

## 模型和方法

### 数据集

工作重点：扩大视觉和视觉语言表示学习，所以用了比当前最大的数据集还要大的数据集，数据集有明显噪声。

**image-based 过滤**

删除色情图像，保留像素大于200，色度小于3的图像；超过1000个关联词的图像被丢掉

**text-based 过滤**

排除超过10个图像共享的备选文本，丢弃太短（小于3）和太长的（大于20）

### 模型

#### 双流模型

image encoder  efficientNet

text encoder  带有cls标记的bert 在bert的顶部添加了一个fc层，匹配图像的尺寸

通过loss来匹配，图文匹配是正数，图文不匹配是负数；

最小化两个loss：（1）图像到文本的分类；（2）文本到图像的分类（跟clip很像），图像和文本嵌入都采取L2归一化

任务：图文匹配，检索，视觉分类

#### 消融研究

1. 更改图像编码器和文本编码器
   扩大图像编码器的效果非常好
   越大的模型对大数据集的表现越好

## 实验和结果

efficientNet ：图像289*289，图像大小346*346，随机裁剪（反转）

bert-large：最多64个标记的wordpiece序列

align有多语言版本

## 图表

### figure 1

![](https://secure2.wostatic.cn/static/fjYXLp5cNhvuBCyENhuM3k/image.png?auth_key=1666654238-9x1Z61WgbeDS44odBciDpS-0-1df438199afc2b2d81753b718931cfe6)

Figure 1.A summary of our method， ALIGN. Visual and language representations are jointly learned from noisy image alt-text data. The representations can be used for vision-only or vision-language task transfer.Without any fine-tuning， ALIGN powers zero-shot visual classification and cross-modal search including image-to-text search， text-to-image search and even search with joint image+text queries.
图1.我们方法的概要，ALIGN。视觉和语言表示是从嘈杂的图像中共同学习的，alt-textdata。表示可以用于仅视觉或视觉语言任务转移。没有任何微调，对齐功能零镜头视觉分类和跨模式搜索，包括图像到文本搜索，文本到图像搜索，甚至与联合图像文本查询一起搜索。

### figure 2

![](https://secure2.wostatic.cn/static/gezF83Gn6fKKbXWmDybH5N/image.png?auth_key=1666654238-iqMoFXz3guipX9UyrzvfHt-0-9a2c30a8a48f1ac4ceba130a332c331f)

Figure 2.Example image-text pairs randomly sampled from the training dataset of ALIGN. One clearly noisy text annotation is marked in italics.
图2.从ALIGN的训练数据集中随机采样的示例图像-文本对。一个明显有噪声的文本注释用斜体标记。
