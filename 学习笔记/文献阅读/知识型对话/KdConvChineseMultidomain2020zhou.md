---
Type: unpublished
Authors: Hao Zhou, Chujie Zheng, Kaili Huang, Minlie Huang, Xiaoyan Zhu
Year: 2020
Title: KdConv: A Chinese Multi-domain Dialogue Dataset Towards Multi-turn Knowledge-driven Conversation
Journal: arxiv:2004.04100 [cs]
DOI: 
Publisher: arXiv
---

#  (2020)KdConv: A Chinese Multi-domain Dialogue Dataset Towards Multi-turn Knowledge-driven Conversation
###                  ——Hao Zhou, Chujie Zheng, Kaili Huang, Minlie Huang, Xiaoyan Zhu
[*Read it now! See in Zotero*](zotero://select/items/@KdConvChineseMultidomain2020zhou)
**Web:** [Open online](http://arxiv.org/abs/2004.04100)
**Citekey:** KdConvChineseMultidomain2020zhou
**Tags:** #数据集 #ACL #中文 #结构化知识 #话题转移模拟
**Code:** [Available Here](https://github.com/thu-coai/KdConv)


## 摘要
The research of knowledge-driven conversational systems is largely limited due to the lack of dialog data which consist of multi-turn conversations on multiple topics and with knowledge annotations. In this paper, we propose a Chinese multi-domain knowledge-driven conversation dataset, KdConv, which grounds the topics in multi-turn conversations to knowledge graphs. Our corpus contains 4.5K conversations from three domains (film, music, and travel), and 86K utterances with an average turn number of 19.0. These conversations contain in-depth discussions on related topics and natural transition between multiple topics. To facilitate the following research on this corpus, we provide several benchmark models. Comparative results show that the models can be enhanced by introducing background knowledge, yet there is still a large space for leveraging knowledge to model multi-turn conversations for further research. Results also show that there are obvious performance differences between different domains, indicating that it is worth to further explore transfer learning and domain adaptation. The corpus and benchmark models are publicly available.

## 总结
提出一个**中文**、**多轮**、**多领域**、**知识驱动**的开放域对话数据集：KdConv
数据集概况：
					*对话组数： 4.5 K （三个领域各1.5 K）
					句子数：86 K
					平均对话轮数： 19
					涉及的领域：3
					每组对话涉及的topic： 1到4*
详细数据： [[KdConvChineseMultidomain2020zhou#^2xlugy]]

## 研究动机
知识驱动的对话研究很大程度上受到了数据匮乏的制约，现有的数据集不能很好地去模拟多轮对话中的知识互动（knowledge interactions）或者对话的主题（topic）有限

## 研究背景/ 问题描述
为了让对话系统表现得更加类人，对话中用到的背景知识起到了关键性作用。在任务型对话系统中，背景知识被定义为槽值对（slot-value pairs），以此为对话生成提供关键信息；开放域对话系统中背景知识常被表示为*知识图谱*或者*非结构化文本*。
近年来，提出了许多知识驱动的对话语料。CMU DoG、India DoG以及Wizard of Wikipedia为对话提供了topic-related Wikipedia articles。
> However, these datasets are not suitable for modeling topic transition or knowledge planning through multi-turn dialogs based on the relations of topics. ([pdf](zotero://open-pdf/library/items/996N9AYJ?page=1&annotation=H6TIB4YH))
([Zhou 等。, 2020, p. 1](zotero://select/library/items/CL5PR6J8))

> **这里的 topic 的概念其实更像是对话中提到的关键词，在知识图谱中被表示为 Head Entity**
> ![[Pasted image 20220606123308.png]]

OpenDialKG、DuConv使用了知识图谱作为知识源。
> Nevertheless, the number of topics is limited to one (Moon et al., 2019) or two (Wu et al., 2019), which is not sufficient for diversified topic transition in humanlike conversations. ([pdf](zotero://open-pdf/library/items/996N9AYJ?page=1&annotation=VNF7HDKR))
([Zhou 等。, 2020, p. 1](zotero://select/library/items/CL5PR6J8))

这些数据集在知识间交互都存在着一定的限制
> knowledge planning, knowledge grounding, knowledge adaptations ([pdf](zotero://open-pdf/library/items/996N9AYJ?page=1&annotation=RC8YQLYD))
([Zhou 等。, 2020, p. 1](zotero://select/library/items/CL5PR6J8))

## 方法的创新点
1、提供了句子级的标注（knowledge grounding）
2、每组对话会涉及1到4个topic，topic都已经显示的定义在了知识图谱中（knowledge planning）
3、数据集涵盖了三个领域的对话（knowledge adaptations）

## 实验评测

**基于生成的模型：语言模型、Seq2Seq、HRED**
![[Pasted image 20220605225519.png]]

**基于检索的模型：Bert**
![[Pasted image 20220605225711.png]]
> 这里使用了 #关键字 提取来代表知识（[参考的论文](https://aclanthology.org/P17-1046.pdf)使用的 tf-idf 方法，并用关键字扩充了上下文）
> ![[Pasted image 20220606101919.png]]

**基于知识感知的模型：基于Bert**
![[Pasted image 20220606100851.png]]

**具体细节：**
![[Pasted image 20220606101330.png]]
> 使用了[Jieba分词](https://github.com/fxsjy/jieba)、初始化词向量

## 实验结论
**评测结果：**
![[Pasted image 20220605230051.png]]
**结论：** 
1、提出了中文的多轮知识对话数据集，包含具体的句子级标注，为知识驱动对话提供了一个基准；
2、同时数据集包含了电影、音乐和旅游三个领域，可用来研究领域转换或迁移学习；
3、提供了两大类模型Baseline：基于生成的和基于检索的。大量的实验证明这些模型可以通过引入知识而加强性能


## 笔记
![[Pasted image 20220605191756.png]]

![[Pasted image 20220605222906.png]] ^ed06c9

![[Pasted image 20220605224908.png]] ^2xlugy