# 说明

此仓库记录阅读/寻找**多模态对话**相关的论文

- [多模态数据集](#多模态数据集)
- [多模态预训练模型](#多模态预训练模型)
- [多模态生成](#多模态生成)
- [共情对话](#共情对话)
- [经典论文](#经典论文)

# 多模态数据集

| 论文名称(简称)                                                                              | 笔记状态 | 年份 | 会议/期刊 | CCF级别 | 研究机构          | 概述                                        |
| ------------------------------------------------------------------------------------------- | -------- | ---- | --------- | ------- | ----------------- | ------------------------------------------- |
| [Openvidial](https://arxiv.org/abs/2012.15015), [OpenVidial2.0](https://arxiv.org/abs/2109.12761) | ✅       | 2021 | arXiv     | --      | ShannonAI         | 多模态对话数据集；电视剧抽帧；提供图片特征  |
| [SER30K](https://dl.acm.org/doi/abs/10.1145/3503161.3548407)                                   | ❌       | 2022 | ACM MM    | A       | Nankai University | meme梗图和sticker的数据集，表情包情感分类器 |
| [MMChat](https://arxiv.org/abs/2108.07154)                                                     | ❌       | 2021 | arXiv     | --      | Alibaba           |                                             |
| [MMDialog](https://arxiv.org/abs/2211.05719)                                                   | ✅       | 2022 | arXiv     | --      | microsoft         | 超大规模多轮对话图文多模态数据集            |
| [PhotoChat](https://arxiv.org/abs/2108.01453)                                                  | ✅       | 2021 | arXiv     | --      | Google research   | 真实照片-对话多模态数据集（小规模）         |

# 多模态预训练模型

| 论文名称(简称)                                                                                                                    | 笔记状态 | 年份 | 会议/期刊 | CCF级别 | 研究机构                        | 概述                                             |
| --------------------------------------------------------------------------------------------------------------------------------- | -------- | ---- | --------- | ------- | ------------------------------- | ------------------------------------------------ |
| [CLIP](http://proceedings.mlr.press/v139/radford21a)                                                                                 | ✅       | 2021 | ICML      | A       | OpenAI                          | 基于对比学习的图文检索预训练模；双流             |
| [ViLT](https://proceedings.mlr.press/v139/kim21k.html)                                                                               | ✅       | 2021 | ICML      | A       | NAVER AI                        |                                                  |
| [Visual-Bert](https://arxiv.org/abs/1908.03557)                                                                                      | ✅       | 2019 | arXiv     | --      | University of California        | 基于transformer的多模态预训练模型；单流          |
| [FILIP]()                                                                                                                            | ✅       | 2021 | arXiv     | --      | Huawei Noah’s Ark Lab          | 比CLIP更细粒度；双流                             |
| [ALIGN](http://proceedings.mlr.press/v139/jia21b.html)                                                                               | ✅       | 2021 | PMLR      | A       | Google Research                 | 相比于CLIP运用了更大规模、噪声更多的数据集；双流 |
| [VilBert（visual-and-language Bert）](https://proceedings.neurips.cc/paper/2019/hash/c74d97b01eae257e44aa9d5bade97baf-Abstract.html) | ❌       | 2019 | NeurlPS   | A       | Georgia Institute of Technology | 早期的视觉-语言跨模态预训练模型；双流            |

# 多模态生成

| 论文名称(简称)                                                                   | 笔记状态 | 年份 | 会议/期刊 | CCF级别 | 研究机构                 | 概述                                                                                           |
| -------------------------------------------------------------------------------- | -------- | ---- | --------- | ------- | ------------------------ | ---------------------------------------------------------------------------------------------- |
| [memeBot](https://arxiv.org/abs/2004.14571)                                         | ✅       | 2020 | arXiv     | --      | Arizona State University | 以文字生成+图片检索（梗图被表示为ocr+title）的方式进行meme梗图回复，本文是DSTC-10MOD任务的报告 |
| [(Divter)Multimodal Dialogue Response Generation](https://arxiv.org/abs/2110.08515) | ✅       | 2022 | ACL       | A       | Microsoft STC Asia       | Divter，sota的多模态（文本+图像）对话生成                                                      |
| Zero-Shot Text-to-Image Generation                                               | ❌       | 2021 | ICML      | A       |                          |                                                                                                |

# 共情对话

因为近期的工作涉及共情对话，所以阅读了一些共情对话的文章。

| 论文名称(简称)                                                                              | 笔记状态 | 年份 | 会议/期刊 | CCF级别 | 研究机构             | 概述 |
| ------------------------------------------------------------------------------------------- | -------- | ---- | --------- | ------- | -------------------- | ---- |
| [CEM](https://ojs.aaai.org/index.php/AAAI/article/view/21373)                                  | ✅       | 2022 | AAAI      | A       | Tsinghua University  |      |
| [Empathetic Dialogue Dataset](https://arxiv.org/abs/1811.00207 "empathetic conversation dataset") | ❌       | 2019 | ACL       | A       | Facebook AI Research |      |
|                                                                                             |          |      |           |         |                      |      |

# 提示学习

| 论文名称(简称)                       | 笔记状态 | 年份 | 会议/期刊 | CCF级别 | 研究机构 | 概述                                                          |
| ------------------------------------ | -------- | ---- | --------- | ------- | -------- | ------------------------------------------------------------- |
| [UPT](https://arxiv.org/abs/2205.05313) | ✅       | 2022 | EMNLP     | B       | Alibaba  | upt：从non-target任务中学习提示知识来提升few-shot文本分类效果 |
|                                      |          |      |           |         |          |                                                               |
|                                      |          |      |           |         |          |                                                               |

# 经典论文

| 论文名称(简称)                                                                                                          | 笔记状态 | 年份 | 会议/期刊 | CCF级别 | 研究机构           | 概述                                        |
| ----------------------------------------------------------------------------------------------------------------------- | -------- | ---- | --------- | ------- | ------------------ | ------------------------------------------- |
| [Attention is all you need](https://proceedings.neurips.cc/paper/2017/hash/3f5ee243547dee91fbd053c1c4a845aa-Abstract.html) | ❌       | 2017 | NIPS      | A       | Google             | Transformer开山之作，提出了多头自注意力机制 |
| [BERT](https://arxiv.org/abs/1810.04805)                                                                                   | ✅       |      | arXiv     | --      | Google AI Language | BERT开山之作，多层transformer               |
|                                                                                                                         |          |      |           |         |                    |                                             |
