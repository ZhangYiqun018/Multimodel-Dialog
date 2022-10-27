1. 原来的LM embedding
   1. feature - based
      利用语言模型的中间结果也就是LM embedding，将其作为额外的特征，引入到原任务的模型中
   2. fine-tuning
      在训练好的语言模型的基础上，加入少量的task-specific parameters（eg，对于分类问题在语言模型的基础上加一层softmax，然后在新的语料上重新训练来进行fine-tune）
2. BERT
   1. 两个预训练任务
      1. Masked language Model
         现在语言模型的问题在于没有利用到双向的信息
         单向语言模型的问题：前向RNN当前词的概率只依赖前面出现词的概率；后向RNN当前词的概率只依赖后面出现的词的概率
         mlm：随机去掉句子的部分token，然后模型预测被去掉的token是什么，p=0.15；mlm收敛的比lm慢
      2. Next Sentence Prediction
         训练语料是两句话，有label：{isnext，notnext}
   2. input
      token embedding 当前词的embedding
      segment embedding 当前词所在句子的index embedding
      position embedding 当前词所在句中位置的 index embedding
      多句子拼接作为单个句子，用segment embedding 和 [seg]作为区分
      句子的第一个token总有特殊含义，比如分类问题中是类别
      input是三个embedding加和
   3. fine-tuning
      ![](https://secure2.wostatic.cn/static/v5RH6oDp9ZKgAoQbJXN5WF/image.png?auth_key=1666830835-iv32QcnipTzLMoafuap197-0-8e0b29cb34aac1799f2d67371a3327c2)

![](https://secure2.wostatic.cn/static/ewyhUYe1rdWmACsHjNz5A8/image.png?auth_key=1666830835-6NVac1p7vLPBgTAg5FVtqG-0-cba67bddf947c32b104f290a800ce6d5)

![](https://secure2.wostatic.cn/static/thHxMbg6nVnMSiAMjuc54U/image.png?auth_key=1666830835-5MZoUmwg7TCdUiv2Fx35Q7-0-ae9e45f86942c69ee4a41bd96919030e)
