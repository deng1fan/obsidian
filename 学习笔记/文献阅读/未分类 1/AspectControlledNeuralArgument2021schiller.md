---
Type: inproceedings
Authors: Benjamin Schiller, Johannes Daxenberger, Iryna Gurevych
Year: 2021
Title: Aspect-Controlled Neural Argument Generation
Journal: Proceedings of the 2021 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies
DOI: 10.18653/v1/2021.naacl-main.34
Publisher: Association for Computational Linguistics
---

#  (2021)Aspect-Controlled Neural Argument Generation
###                  ——Benjamin Schiller, Johannes Daxenberger, Iryna Gurevych
[*Read it now! See in Zotero*](zotero://select/items/@AspectControlledNeuralArgument2021schiller)
**Web:** [Open online](https://aclanthology.org/2021.naacl-main.34)
**Citekey:** AspectControlledNeuralArgument2021schiller
**Tags:** #话题控制 #粗读 
**Code:** [*Available Here*](https://github.com/UKPLab/controlled-argument-generation)


## 摘要
We rely on arguments in our daily lives to deliver our opinions and base them on evidence, making them more convincing in turn. However, finding and formulating arguments can be challenging. In this work, we present the Arg-CTRL - a language model for argument generation that can be controlled to generate sentence-level arguments for a given topic, stance, and aspect. We define argument aspect detection as a necessary method to allow this fine-granular control and crowdsource a dataset with 5,032 arguments annotated with aspects. Our evaluation shows that the Arg-CTRL is able to generate high-quality, aspect-specific arguments, applicable to automatic counter-argument generation. We publish the model weights and all datasets and code to train the Arg-CTRL.

## 总结
基于CTRL模型换了个数据集，提出**Arg-CTRL**模型，使用控制信号并配合关键字用来控制辩论的态度（支持或反对），本文关键其实就是**Aspect（关键字）挖掘**
  
## 研究动机
我们依靠日常生活中的论据来表达我们的观点，并将其建立在证据的基础上，从而使其更具说服力。然而，发现和阐述论点可能具有挑战性。在这项工作中，我们提出了Arg-CTRL——一种用于参数生成的语言模型，可以控制它为给定的主题、立场和方面生成句子级参数。

## 研究背景/ 问题描述


## 方法的创新点
使用BERT在数据集上训练一个分类器，
![[Pasted image 20220725102657.png]]

## Baselines

## 实验评测
![[Pasted image 20220725130934.png]]
![[Pasted image 20220725130949.png]]

## 实验结论


## 笔记
> two experts (a post-doctoral researcher and an undergraduate student with NLP background) independently annotate 800 random samples (from four topics, 200 per topic) taken from the UKP-Corpus.     ([Schiller 等。, 2021, p. 382](zotero://select/library/items/ZTWVXC6H)) ([pdf](zotero://open-pdf/library/items/SV6SRDKY?page=3&annotation=CNXHU5Q4))  
> 笔记：两个人 800样本 好拼