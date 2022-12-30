# 标题： 多模态对话生成任务

Title：Multimodal Dialogue Response Generation

## 摘要

使用图像进行回复是智能对话代理的重要能力；然而过去的工作都是着重于基于检索的方法，而基于生成的方法没有太多工作。为了填补这个空白，本文提出了多模态对话响应生成任务（MDRG）——在给定对话背景下，一个模型需要生成一个多模态（文本或者图像）对话响应。

在低资源的情况下，本文设计了一个新的对话代理，Divter，以便于从生成模型中分离出依赖于多模态对话的参数。模型的主要部分可以分别从大量的纯文本对话和文本-图像对中学习，然后只需要少量的训练数据，就可以拟合整个参数。

## 介绍

贡献介绍：

+ 第一个多模态对话生成
+ 提出Divter，一个全新的对话代理，能够有效率的理解对话文本并且生成相关的文本和高解析度的图片回复
+ 对PhotoChat语料库的广泛实验，表明了Divter的有效性

## 问题定义

dataset : $D_S = {(U_i, R_i)}^n_{i=1}$

dialog context : $U_i = {u_{i,1}, u_{i, 2}, \cdots, u_{i, n_i}}$

response : $R = P(R|U;\theta), \theta:模型参数$

## 方法

### Divter：多模态生成模型

#### tokenization

goal：对齐文本和图片模态
text tokenizer：BPE-encoded
image tokenizer：VQGAN

#### 低资源学习模型

存在大规模开源文本对话模型$D_C$和大规模的<图像描述，图像>对模型$D_P$，用下面的方法对齐：

1. 如果多模态文本包含图片，替换图片为图片描述，并且把图片描述输入$D_C$
2. 如果我们需要产生图片，我们首先生成图片描述，然后用$D_P$去翻译描述为图片。

#### 文本对话生成器

一个基于transformer的seq-2-seq模型，包含24层Transformer，隐藏层维度1024，16个多头注意力。

[SEP]分割句子，[DST]表示后面跟着的是图片的描述

#### 文本-图像翻译器

文本-图像翻译器同样是seq-2-seq模型，基于transformer，24层，1024维，16头。

给定一个图像和他的文本描述，把图片表示成向量s，文本描述表示成向量c，连接c和s，然后训练一个自回归的transformer模型来模拟文本和图像的联合分布

## 实验

dataset：photochat（包含10917个图片和12286个对话）

### 评价指标

#### 自动评价

1. 图片意图预测
   1. 这个任务的目标是预测是否在下一个回合中是否应该产生一个图像
   2. 二分类问题，acc和f1
2. 图片描述生成
   1. ppl，bleu，rouge，f1
3. 图片产生质量
   1. Frechet Inception Distance
   2. Inception Score
      1. Zero-shot text-to-image generation(Ramesh,2021)
4. 文本回复生成
   1. ppl，bleu，rouge，f1

#### 人工评价

选出200个对话文本和回复，对比divter和baseline，三个人工标注员

指标：

1. 文本一致性
2. 本文流畅度
3. 图像质量
4. 图像背景一致性

### 实现细节

文本生成器：DialoGPT

<图像描述，图像> ImageNet，在PhotoChat下fine-tune

图像生成器：DALL-E

### baseline

bert-base，T5-3B，SCAB，S2S-TF
