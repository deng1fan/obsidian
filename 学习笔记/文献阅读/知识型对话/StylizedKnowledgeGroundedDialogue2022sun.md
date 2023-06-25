---
Type: unpublished
Authors: Qingfeng Sun, Can Xu, Huang Hu, Yujing Wang, Jian Miao, Xiubo Geng, Yining Chen, Fei Xu, Daxin Jiang
Year: 2022
Title: Stylized Knowledge-Grounded Dialogue Generation via Disentangled Template Rewriting
Journal: arxiv:2204.05610 [cs]
DOI: 
Publisher: arXiv
---

#  (2022)Stylized Knowledge-Grounded Dialogue Generation via Disentangled Template Rewriting
###                  ——Qingfeng Sun, Can Xu, Huang Hu, Yujing Wang, Jian Miao, Xiubo Geng, Yining Chen, Fei Xu, Daxin Jiang
[*Read it now! See in Zotero*](zotero://select/items/@StylizedKnowledgeGroundedDialogue2022sun)
**Web:** [Open online](http://arxiv.org/abs/2204.05610)
**Citekey:** StylizedKnowledgeGroundedDialogue2022sun
**Tags:**  #可控生成 #未完 
**Code:** [Available Here（目前为空仓库）](https://github.com/victorsungo/SKDG-DTR)


## 摘要
Current Knowledge-Grounded Dialogue Generation (KDG) models specialize in producing rational and factual responses. However, to establish long-term relationships with users, the KDG model needs the capability to generate responses in a desired style or attribute. Thus, we study a new problem: Stylized Knowledge-Grounded Dialogue Generation (SKDG). It presents two challenges: (1) How to train a SKDG model where no <context, knowledge, stylized response> triples are available. (2) How to cohere with context and preserve the knowledge when generating a stylized response. In this paper, we propose a novel disentangled template rewriting (DTR) method which generates responses via combing disentangled style templates (from monolingual stylized corpus) and content templates (from KDG corpus). The entire framework is end-to-end differentiable and learned without supervision. Extensive experiments on two benchmarks indicate that DTR achieves a significant improvement on all evaluation metrics compared with previous state-of-the-art stylized dialogue generation methods. Besides, DTR achieves comparable performance with the state-of-the-art KDG methods in standard KDG evaluation setting.

## 总结
提出新问题：风格化知识对话，也就是要求模型在生成回复时，不仅要和上文连贯、和知识一致，还要和给定的风格或情感一致
针对新问题提出新模型：*DTR ：Disentangled Template Rewriting*
  
## 研究动机
风格化知识对话目前存在两个难点：1、**缺少<context, knowledge, stylized response>这样的标注数据的情况下如何训练模型**；2、**如何在保证对话风格和情感一致性的情况下保证知识的客观正确性（这里有一个很大的问题就是现有的风格对话模型，很容易把知识里边的某些词认为是风格信号，为了保持回复风格，模型会改变原知识的描述）**

> Especially when the given knowledge contains style-related content, existing stylized dialogue generation (SDG) models (Zheng et al., 2020; Ze et al., 2020) may undermine the correctness of knowledge section. ([pdf](zotero://open-pdf/library/items/4B7WBIMB?page=2&annotation=UGFYB2C4))
> ([Sun 等。, 2022, p. 2](zotero://select/library/items/CJBQKUDV))

为了解决上述的问题，本文提出一个解耦的模板去连接知识和风格之间的正确关系，并使用强化学习去要求模型保证知识的正确运用

## 研究背景/ 问题描述
*知识对话* ：以往的研究往往集中于根据Benchmark提出一个新的网络结构，本文则专注于如何将基于知识的回复转换成我们想要的风格
*文本风格和情感转换*：不同于传统的文本风格转换问题，风格化对话生成在要求风格转换的同时还要保证与上文的连贯性
*风格化对话生成*：本文首次提出在没有对应的训练数据（context-knowledge-response）的情况下如何去训练一个基于知识的风格化对话模型


## 方法的创新点
![[Pasted image 20220619155316.png]]

风格替换
![[Pasted image 20220619155344.png]]

在风格转化数据集上进行自编码器训练（这样重构带风格化的文本会比重构带内容的文本更加容易）


## 实验评测
![[Pasted image 20220619160514.png]]

![[Pasted image 20220619160533.png]]

消融实验![[Pasted image 20220619160643.png]]
注：WSL代表弱监督
## 实验结论


## 笔记
在强化学习阶段，使用batch平均奖励作为奖励
