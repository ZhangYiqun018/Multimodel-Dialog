## 精读笔记

* clip是一个预训练模型，数据集很大
* 如何实现zero-shot（imagenet分类任务）？
  * 用图片特征跟文本特征计算相似度，相似度最高的就是分类，图-文匹配
  * 对于其他数据集表现也非常好
* 整体架构
  * 大部分篇幅留给实验和分析
  * 1页引言，2页方法，6-18做实验，1页局限性，5页未来发展

### 摘要

* 过去的模型都是固定好分类头
  * 好处：简化问题
  * 坏处：泛化能力低
  * 改进方法：直接从自然语言中获得监督信号
    SOTA：state of the art
* 迁移学习效果强，不需要数据集微调表现比以前更好
* 开源了模型和推理的代码，没有开源预训练的代码

### 介绍和相关工作

* GPT-3，过去的大模型，只需要针对下游任务做微调，文本进文本出
* 过去的东西很好，但都有分类头，导致做zero-shot能力差
* 与clip相似的方法：VirTex，ICMLM，ConVIRT
  * 过去的效果不好不是方法不行，是规模不够大
  * 本文收集了400百万对数据
  * **作者发现迁移学习的效果跟模型大小呈正相关**
* 结果
  * 在30个数据集上做zero-shot跟有监督训练模型打成平手
  * 如果训练下游的分类头，比有监督模型要好很多

### 预训练方法

* 用自然语言的信号去做训练（无监督，自监督，弱监督，有监督）
  * 好处
    * 不需要额外标注。只需要下载图片和文本的配对
    * 输入输出的自由度高了
    * 学习到的特征不再是视觉特征而是多模态特征
  * 坏处
    * 需要足够大的数据集，原有的高质量数据集小而少，低质量数据集大
* 自己做了一个数据集
  * 4亿规模的数据集，与训练GPT-2数据集相当
  * WIT
  * 数据集足够大，不会出现过拟合；
  * 不需要数据增强（除了裁剪）
* 预训练
  * 第一次 - VirTex
    * 图像 - cnn，文本-transformer，预测图像的标题
  * 第二次 - 对比学习
    * 训练效率提高了四倍
    * 视觉
      * 五个resnet和3个vit

### 实验

* zero-shot迁移

  * 迁移学习的过程
* PROMPT ENGINEERING AND ENSEMBLING

  * 提示：文本的引导作用
  * polysemy ：多义性
    * 加提示
  * distribution gap：
    * 制作标签模板，a photo of a {label} 限定词性
    * a photo of a label, a type of a pet.
* 实验结果

  * zeroshot
    * 简单的任务zero-shot很好
    * 困难的任务需要few-shot
      * 因为困难的任务就算是人类也需要训练才能完成
  * 特征训练
    * linear probe - 冻结预训练模型，只加一个分类头
    * fine-tune - 微调

### clip接口

```Python
import clip
# 查看clip可用模型
clip.available_models()
# load model 
# preprocess是什么我不知道
model, preprocess = clip.load(name, device=..., jit=False)

# 给text变成张量
clip.tokenize(text: Union[str, List[str]], context_length=77)
# 给image变成张量
image = preprocess(Image.open("/home/zyq/modelTest/clip/image/test2.jpg")).unsqueeze(0).to(device)

# image encode
iamge = model.encode_image(image: Tensor)
# text encode
text = model.encode_text(text: Tensor)
# model train
model(text, image)
```
