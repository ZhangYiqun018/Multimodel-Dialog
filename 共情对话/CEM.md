# CEM

- [CEM](#cem)
  - [粗读](#粗读)
    - [标题](#标题)
    - [摘要](#摘要)
    - [结论](#结论)
  - [精读](#精读)
    - [motivation](#motivation)
    - [预备工作](#预备工作)
    - [模型](#模型)
      - [Training objectives](#training-objectives)
    - [实验](#实验)
      - [baseline](#baseline)
      - [实现细节](#实现细节)
      - [自动评价](#自动评价)
      - [众包评价](#众包评价)
      - [消融实验](#消融实验)

## 粗读

### 标题

CEM: Commonsense-Aware Empathetic Response Generation

CEM：共识意识的共情回复生成

### 摘要

对话的重要性：表达感情和实现共情。

过去的方法：

    检测和利用用户的情绪，产生共情回复。

    缺点：除了识别情绪之外，还应该考虑对用户情况的认知和理解。

本文的方法：

    利用常识来获取更多用户情况，使用额外的信息来加强共情回复

数据集：

    facebook: EmpatheticDialogues

[开源地址](https://github.com/Sahandfer/CEM)

### 结论

主要贡献：

+ 提出了CEM模型
+ 证明常识知识有利于理解用户的情况和感受

## 精读

### motivation

共情回复可以改善多个领域的用户体验和满意度。

    共情包括感情和认知的各个方面，感情关注的是对用户经历的反应的情感模拟；认知的目的是理解用户的情况和隐含的感受。人类依赖于知识和常识性的推理来得出这些含义。

    如果为对话系统外部知识，可以让对话系统更了解用户的感受和处境，生成更好的共情回复。

### 预备工作

共情对话生成

常识和共情

任务制定

### 模型

context encoding

    input C = {cls, u1, u2, u3, ...}，使用对话状态嵌入来区分双方

knowledege acquisition

    对于输入C，分别使用五个特殊标记([xReact], [xWant], [xNeed], [xIntent], [xEffect])，加到对话历史的最后一句话，使用comet生成五个常识推理[csr1, csr2, ..., csr5]。将生成的常识推理串联起来，获得常识序列CSr = {csr1, csr2, ..., csr3}

    xReact显示了情感状态（用户的情绪）的知识，另一个关系代表了用户的情况，将这些关系分为：情感的和认知的。在序列前加上[cls]，分别获得情感和认知的特征，最后用情感关系的平均隐藏表征和认知关系的[CLS]隐藏表征来分别表示这些序列。

context refinement

    将句子特征与情感特征和认知特征分别拼接在一起，分别用两个编码器来进行混合编码，获得句子+情感的特征以及句子+认知的特征

emotion classification

    使用cls来进行情感分类，softmax(Haff[0])

knowledge selection

    通过sigmoid获得重要性分数，过一个mlp

response generation

    Y=[y1, ..., yt]

#### Training objectives

response diversity

    有些回复不需要用到上下文，回被频繁使用，比如i am sorry，good，ok之类的

    使用FACE来惩罚高频率的token，在训练期间，接收新的样本之前，首先计算出token的相对频率rf

### 实验

#### baseline

transformer，Multi-task Transformer，MoEL，MIME，EmpDG

#### 实现细节

#### 自动评价

PPl（评估总体质量），Dist-n（评估多样性），Acc（评价情感分类）

#### 众包评价

流畅性、相关性、同情心，1-5分

#### 消融实验

不含情感组件，不含认知，不含多样性
