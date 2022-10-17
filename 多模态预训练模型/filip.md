## 精读笔记

### 标题和小结

title：FILIP: FINE-GRAINED INTERACTIVE LANGUAGE-IMAGE PRE-TRAINING
FILIP: 细粒度的交互式语言-图像预训练

小结

### 摘要

* 跨模态后期交互机制实现更精细的对齐
  * 视觉和文本标记之间的最大相似性来指导对比目标
  * 修改对比损失
* 大规模图像-文本对数据集FILIP300M，图像分类和图像检索都有好性能

### 介绍

* clip的align的成功之处
  * 大规模的数据集
  * 通过双流模型进行全局对比对齐
  * 两个编码器解耦，离线分别计算图像和文本的表示
* clip和align的不足之处
  * 只对齐全局特征，缺乏捕捉精细信息的能力

### 相关工作

单流：visual-bert，vilt

双流：vilbert，clip，align，filip

### 模型与方法

* text encoder 基于transformer的模型
* image encoder vision transformer
* 与clip和align不同，考虑了粒度更细的特征
* 如何实现跨模态后期交互？
  * 对于第k个视觉标记，我们计算它与其他所有文本标记的相似度，并使用最大的
    对于每个图像patch，都找到其最相似的文本特征；对于每个文本token，都找到最相似的图像patch
  * 对于每个图像块和文本token，找到最大相似度，求平均然后作为该图像-文本对的相似程度s
* 训练效率
  * embedding dim 256
  * 还有一些操作目前不明白
* **提示学习**
  * 这里的处理方式与clip相似
    * a photo of {label}
  * 提示模板
    * [prefix] {label}, [category description]. [suffix]
    * prefix → 一个上下文描述 如 a photo of a
    * label → 类标签
    * category description → 类别描述，对某些细粒度图像分类数据集有用的类别（比如宠物）
    * suffix → 包含参考词it的后缀，比如 i like it，提高了zero-shot性能
      * 推测是it加强了细粒度的跨模态对齐，可以与图像块进行对齐
* **数据增强**
  * 为了获得更好的模型泛化性和数据效率，在预训练阶段对于图像和文本进行了数据增强，构建更多的图像-文本对
    AutoAugment
  * 图像增强：采用sota的识别方法
  * 文本增强：反向翻译：文本先被翻译为目标语言，然后再翻译成源语言（目标语言是德语和俄语）

### dataset

clip：400M

align：1800M

filip：300M

3亿个图像-文本对

从互联网上收集，过滤规则：小于200像素，纵横比大于3的；文本：保留英文，删掉无意义的；丢弃重复超过10次的

cc3M，cc12M，YFCC100，采用相同的过滤规则

虽然数据集小，但是模型更优秀

### 实验结果

* 实验采用的模型结构
  * filip-base：vit-b/32
  * filip-large：vit-L/14
* 刷榜
  * zero-shot 分类
    * 在12个数据集上，只跟clip相比，比clip好
    * align没开源比不了
  * zero-shot图像-文本检索任务
    * flickr 30K
    * mscoco
