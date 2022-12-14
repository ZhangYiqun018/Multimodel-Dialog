* 本文主要工作
  * 提出一个重在融合的视觉文本转化器
* title
  * vlit 视觉和语言转换器，无需卷积或区域监督
* abstrack
  * 视觉和语言预训练提高了联合视觉和语言下游任务的表现
  * 当前存在的问题：
    * 1、严重依赖图像的特征提取过程
      * 区域监控（目标检测、卷积结构）
      * 效率和速度存在问题
    * 2、表达能力有问题
      * 视觉限制了表达能力的上限
  * 改进方向
    * 视觉处理的方式被简化为与处理文本输入相同的五卷机方式
    * 速度变快了，性能提升了
* 介绍
  * 由于卷积网络在视觉领域的成功，所以人们一般认为融合视觉和文本的时候，处理视觉也不应该离开卷积神经网络
  * 四类视觉-语言模型
  * 学界的趋势是强化视觉嵌入层，但是这篇论文的重点是轻量级的视觉嵌入，使用transformer，而不是卷积
    * 用统一的方式处理文本和语言，提升学习速度
      * 速度比具备区域特征的vlp模型快10倍
      * 比具有网格特征的模型快四倍
      * 性能相似甚至更好
  * 主要贡献
    * 1、简单 轻便
    * 2、不使用区域特征识别和深度卷积结构
* 背景
  * figure2图解
    * vse和scan 视觉大于文本 图2a
    * clip属于图2b 每种模态单独处理，但是很深，交互方案很浅，视觉 = 文本
    * 深层交互，但是文本小于视觉，视觉用深模型
    * vilt是文本=视觉 都是浅层的，深层是交互方面
  * 相关工作
    * 视觉嵌入结构
      * 区域检测，目标探测，落后，很深，很重
      * 补丁投影
        * 32 * 32补丁投影
    * 文本嵌入结构
* vilt
  * 模型概述
    * 多个transform和1个多层感知机，层归一化
    * text 输入是词嵌入矩阵和位置矩阵
    * image的输入是分割成块并且展平，
      * N=HW/P2 N = HW / P^2
        **N**=**H**W**/**P**2******
    * 文本和图像的嵌入矩阵与对应的模态响亮想家，然后连接成组合序列z
  * 预训练
    * ITM - 图像文本匹配
      * 用概率为0.5的不同图像随机替换对齐的图像，一个线性层ITM头将合并输出特征
    * MLM - 掩码语言建模
      * 像bert cloze
  * 全局掩码
    * bert-base-uncased tokenizer
      * giraffe标记为三个单词标记
        * gi ##raf ##fe
        * gi 【mask】 ##fe - 如果不是所有的标记都屏蔽，则模型仅依赖两种语言标记预测##raf
        * 0.15的概率遮蔽整个单词
  * 图像增强
    * randaugemnt
      * 用了一些图片增强技术 除了颜色反转和剪切
* 实验
  * 数据集
    * mscoco vg sbu captions google cc
  * 任务目标
    * 两种下游任务
      * 分类 - VQAv2 NLVR2
        * 视觉问答 vqav2
        * 视觉推理的自然语言 vlvr2
          * 二元分类任务，给定两个图像的三元组和一个自然语言的问题
          * 三元组输入被重新表述为两对 问题 图像1 和 问题 图像2
      * 检索 - MSCOCO Flickr30
  * 实现细节
  * 复杂度分析（模型的规模）
  * 视觉化
    * 图4展示了跨模态对齐
* 结论和未来展望
  * 更像是证明了一些复杂任务不需要卷积操作也可以实现
