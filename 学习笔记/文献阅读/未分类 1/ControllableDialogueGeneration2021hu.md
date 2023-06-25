---
Type: article
Authors: Zhe Hu, Zhiwei Cao, Hou Pong Chan, Jiachen Liu, Xinyan Xiao, Jinsong Su, Hua Wu
Year: 2021
Title: Controllable Dialogue Generation with Disentangled Multi-grained Style Speciﬁcation and Attribute Consistency Reward
Journal: 
DOI: 
Publisher: 
---

#  (2021)Controllable Dialogue Generation with Disentangled Multi-grained Style Speciﬁcation and Attribute Consistency Reward
###                  ——Zhe Hu, Zhiwei Cao, Hou Pong Chan, Jiachen Liu, Xinyan Xiao, Jinsong Su, Hua Wu
[*Read it now! See in Zotero*](zotero://select/items/@ControllableDialogueGeneration2021hu)
**Web:** [Open online]()
**Citekey:** ControllableDialogueGeneration2021hu
**Tags:** #多粒度控制 #未完
**Code:** [*Available Here*]()


## 摘要
Controllable text generation is an appealing but challenging task, which allows users to specify particular attributes of the generated outputs. In this paper, we propose a controllable dialogue generation model to steer response generation under multi-attribute constraints. Specifically, we define and categorize the commonly-used control attributes into global and local ones, which possess different granularities of effects on response generation. Then, we significantly extend the conventional seq2seq framework by introducing a novel twostage decoder, which first uses a multi-grained style specification layer to impose the stylistic constraints and determine word-level control states of responses based on the attributes, and then employs a response generation layer to generate final responses maintaining both semantic relevancy to the contexts and fidelity to the attributes. Furthermore, we train our model with an attribute consistency reward to promote response control with explicit supervision signals. Extensive experiments and in-depth analyses on two datasets indicate that our model can significantly outperform competitive baselines in terms of response quality, content diversity and controllability.

## 总结
提出**CRAYON**模型，
  
## 研究动机
可控文本生成是一项有吸引力但具有挑战性的任务，它允许用户指定生成输出的特定属性。在本文中，我们提出了一种可控的对话生成模型，用于指导多属性约束下的响应生成。具体来说，我们将常用的控制属性定义并分类为全局和局部属性，它们对响应生成具有不同的影响粒度。然后，我们通过引入一种新的两阶段译码器显著扩展了传统的seq2seq框架，该译码器首先使用多粒度样式规范层施加样式约束，并根据属性确定响应的字级控制状态，然后使用响应生成层生成最终响应，同时保持与上下文的语义相关性和对属性的保真度。此外，我们使用属性一致性奖励训练我们的模型，以通过显式监督信号促进响应控制。对两个数据集的大量实验和深入分析表明，我们的模型在响应质量、内容多样性和可控性方面明显优于竞争基线。

## 研究背景/ 问题描述


## 方法的创新点
![[Pasted image 20220801102548.png]]

> context encoder maps input contexts into hidden representations using a bi-directional GRU network     ([Hu 等。, 2021, p. 2](zotero://select/library/items/LS93FPAL)) ([pdf](zotero://open-pdf/library/items/35B44ZFB?page=2&annotation=CQX5ZTL3))  
> 笔记：使用GRU进行编码

在预测控制信号时
> we further incorporate the posterior distribution P ′(zj|x, y) to leverage both input context and response, and train the predictor by reducing the prediction divergence between its prior P (zj|x) and posterior distributions to improve the prediction performance.     ([Hu 等。, 2021, p. 2](zotero://select/library/items/LS93FPAL)) ([pdf](zotero://open-pdf/library/items/35B44ZFB?page=2&annotation=SU5499DH))  
> 笔记：使用了后验拉近先验

## Baselines
[]()       [*Code*]()
> 

## 实验评测


## 实验结论


## 笔记
