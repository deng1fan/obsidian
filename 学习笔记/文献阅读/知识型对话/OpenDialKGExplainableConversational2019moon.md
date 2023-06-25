---
Type: inproceedings
Authors: Seungwhan Moon, Pararth Shah, Anuj Kumar, Rajen Subba
Year: 2019
Title: OpenDialKG: Explainable Conversational Reasoning with Attention-based Walks over Knowledge Graphs
Journal: Proceedings of the 57th Annual Meeting of the Association for Computational Linguistics
DOI: 10.18653/v1/P19-1081
Publisher: Association for Computational Linguistics
---

#  (2019)OpenDialKG: Explainable Conversational Reasoning with Attention-based Walks over Knowledge Graphs
###                  ——Seungwhan Moon, Pararth Shah, Anuj Kumar, Rajen Subba
[*Read it now! See in Zotero*](zotero://select/items/@OpenDialKGExplainableConversational2019moon)
**Web:** [Open online](https://aclanthology.org/P19-1081)
**Citekey:** OpenDialKGExplainableConversational2019moon
**Tags:** #数据集, #知识图谱 #ACL #英文
**Code:** 暂无


## 摘要
We study a conversational reasoning model that strategically traverses through a large-scale common fact knowledge graph (KG) to introduce engaging and contextually diverse entities and attributes. For this study, we collect a new Open-ended Dialog \textless-\textgreater KG parallel corpus called OpenDialKG, where each utterance from 15K human-to-human role-playing dialogs is manually annotated with ground-truth reference to corresponding entities and paths from a large-scale KG with 1M+ facts. We then propose the DialKG Walker model that learns the symbolic transitions of dialog contexts as structured traversals over KG, and predicts natural entities to introduce given previous dialog contexts via a novel domain-agnostic, attention-based graph path decoder. Automatic and human evaluations show that our model can retrieve more natural and human-like responses than the state-of-the-art baselines or rule-based models, in both in-domain and cross-domain tasks. The proposed model also generates a KG walk path for each entity retrieved, providing a natural way to explain conversational reasoning.

## 总结
提出**基于知识图谱**的、开放域对话数据集：OpenDialKG；
数据集概况：
				*对话组数：15 K
				句子总数：91 K*
![[Pasted image 20220606195551.png]]
并基于此数据集提出*DialKG Walker* 模型用于建模对话过程中的知识转换
  
## 研究动机
开放域对话的关键要素就是对上下文的理解并引入相关的实体或属性，来增加对话的吸引力。本文旨在根据对话上文去筛选一个来自于知识图谱的实体集合，以方便将该实体放入到response中

## 研究背景/ 问题描述
现有的基于知识图谱的数据集通常有两个限制：实体数量少；缺少实体与实体之间的转移建模。
本文贡献：
![[Pasted image 20220606195430.png]]

## 方法的创新点
1、显式的模拟了对话实体的推理路径
> (1) explicitly modeling output reasoning paths in a structured KG, (2) by introducing an attentionbased multi-hop concept decoder to improve both recall and precision. ([pdf](zotero://open-pdf/library/items/DJ4V4H2H?page=8&annotation=U55RYCWU))
([Moon 等。, 2019, p. 852](zotero://select/library/items/TIJQ6JTK))

2、数据集包含了多个对话场景（推荐和闲聊），并且内容涵盖多个领域
> Our OpenDialKG corpus is unique in that it includes open-ended natural human conversations over multiple scenarios (e.g. chit-chat and recommendation on various domains), where reasoning paths from each dialog are annotated with their corresponding discrete KG operations. Our work can also be viewed as extending the conventional state-tracking approaches (Henderson et al., 2014) to more flexible KG path as states.
> (Moon 等。, 2019, p. 852)

3、不同于以往的对知识图谱的推理任务（e.g. edge prediction），本文旨在在现有的路径中找出符合人类认知的实体转移路径
> In contrast to the line of work on KG edge prediction, we aim to learn an optimal path within existing paths that resemble human reasoning in conversations.
> (Moon 等。, 2019, p. 852)

![[Pasted image 20220606195245.png]]

## 实验评测
**Baselines:** 
1、Seq2Seq：![[Pasted image 20220606195800.png]]
2、Tri-LSTM ![[Pasted image 20220606195938.png]]
3、Extended Enc-Dec ![[Pasted image 20220606200050.png]]
4、消融实验：![[Pasted image 20220606200201.png]]

## 实验结论
本文提出的*DialKG Walker* 模型可以有效地利用知识，带有注意力的图解码器能有效的去除不相关的路径，同时该模型可以实现跨域的迁移学习，即模型可以实现领域无关的性能提高
![[Pasted image 20220606195223.png]]

![[Pasted image 20220606195211.png]]

## 笔记
![[Pasted image 20220606191101.png]]