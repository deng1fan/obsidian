---
Type: unpublished
Authors: Prakhar Gupta, Harsh Jhamtani, Jeffrey P. Bigham
Year: 2022
Title: Target-Guided Dialogue Response Generation Using Commonsense and Data Augmentation
Journal: arxiv:2205.09314 [cs]
DOI: 
Publisher: arXiv
---

#  (2022)Target-Guided Dialogue Response Generation Using Commonsense and Data Augmentation
###                  ——Prakhar Gupta, Harsh Jhamtani, Jeffrey P. Bigham
[*Read it now! See in Zotero*](zotero://select/items/@TargetGuidedDialogueResponse2022gupta)
**Web:** [Open online](http://arxiv.org/abs/2205.09314)
**Citekey:** TargetGuidedDialogueResponse2022gupta
**Tags:**  #ConceptNet, #关键字 #话题转移模拟 #未完 
**Code:** [Available Here](https://github.com/prakharguptaz/target-guided-dialogue-coda)


## 摘要
Target-guided response generation enables dialogue systems to smoothly transition a conversation from a dialogue context toward a target sentence. Such control is useful for designing dialogue systems that direct a conversation toward specific goals, such as creating non-obtrusive recommendations or introducing new topics in the conversation. In this paper, we introduce a new technique for target-guided response generation, which first finds a bridging path of commonsense knowledge concepts between the source and the target, and then uses the identified bridging path to generate transition responses. Additionally, we propose techniques to re-purpose existing dialogue datasets for target-guided generation. Experiments reveal that the proposed techniques outperform various baselines on this task. Finally, we observe that the existing automated metrics for this task correlate poorly with human judgement ratings. We propose a novel evaluation metric that we demonstrate is more reliable for target-guided response evaluation. Our work generally enables dialogue system designers to exercise more control over the conversations that their systems produce.

## 总结
使用ConceptNet中的常识知识构建目标引导的转移路径，然后给模型提供引导![[Pasted image 20220624160008.png]]

本文还提出一种新的评价方法

## 研究动机


## 研究背景/ 问题描述
不同于以往的关键字或话题引导的模型（基于给定的关键字或话题去生成回复），本文的目标是实现从上文到目标语句的平滑过渡

## 方法的创新点
![[Pasted image 20220625141920.png]]

## 实验评测


## 实验结论


## 笔记
1、使用的知识路径生成器是一个在ConceptNet上训练的语言生成器
> Knowledge Path Generator (KPG), a language model trained on paths sampled from ConceptNet.     (Gupta 等。, 2022, p. 3)