---
Type: unpublished
Authors: Hannah Rashkin, David Reitter, Gaurav Singh Tomar, Dipanjan Das
Year: 2021
Title: Increasing Faithfulness in Knowledge-Grounded Dialogue with Controllable Features
Journal: arxiv:2107.06963 [cs]
DOI: 
Publisher: arXiv
---

#  (2021)Increasing Faithfulness in Knowledge-Grounded Dialogue with Controllable Features
###                  ——Hannah Rashkin, David Reitter, Gaurav Singh Tomar, Dipanjan Das
[*Read it now! See in Zotero*](zotero://select/items/@IncreasingFaithfulnessKnowledgeGrounded2021rashkin)
**Web:** [Open online](http://arxiv.org/abs/2107.06963)
**Citekey:** IncreasingFaithfulnessKnowledgeGrounded2021rashkin
**Tags:** #ACL #可控生成
**Code:**  暂无


## 摘要
Knowledge-grounded dialogue systems are intended to convey information that is based on evidence provided in a given source text. We discuss the challenges of training a generative neural dialogue model for such systems that is controlled to stay faithful to the evidence. Existing datasets contain a mix of conversational responses that are faithful to selected evidence as well as more subjective or chit-chat style responses. We propose different evaluation measures to disentangle these different styles of responses by quantifying the informativeness and objectivity. At training time, additional inputs based on these evaluation measures are given to the dialogue model. At generation time, these additional inputs act as stylistic controls that encourage the model to generate responses that are faithful to the provided evidence. We also investigate the usage of additional controls at decoding time using resampling techniques. In addition to automatic metrics, we perform a human evaluation study where raters judge the output of these controlled generation models to be generally more objective and faithful to the evidence compared to baseline dialogue systems.

## 总结
提出**CTRL-Dial**模型，通过将数据分类作为控制信号实现可控对话生成
![[Pasted image 20220706195636.png]]

一些关于模型实现的具体细节可以在 [[CTRL实现计划]]查看
  
## 研究动机
观察到基于知识的对话数据集通常包含具有不同对话风格和意图的话语，包括一些信息量更大的话语和一些闲聊话语或主观评论。

由于这种对话风格的混合，我们无法确保在这些数据上直接进行训练的模型将学会仅生成可靠的、信息丰富的话语。

采用可控文本生成技术来训练对话模型，学习在数据中分开这些对话风格，并且可以在生成时进行控制以产生更充实的回复。

## 研究背景/ 问题描述


## 方法的创新点
通过添加控制信号的方式实现一种Prompt的风格控制生成
![[Pasted image 20220706195718.png]]

控制信号：
**Objective Voice**
> \<first-person>\<no-first-person>     ([Rashkin 等。, 2021, p. 5](zotero://select/library/items/DWRRENIU)) ([pdf](zotero://open-pdf/library/items/8WZ3JGIY?page=5&annotation=8YMD6YWT))  
> 笔记：人称控制

**Lexical Precision**
> \<high-prec>,\<med-prec>, and \<low-prec>)     ([Rashkin 等。, 2021, p. 5](zotero://select/library/items/DWRRENIU)) ([pdf](zotero://open-pdf/library/items/8WZ3JGIY?page=5&annotation=5DIKUPPU))  
> 笔记：与知识的词汇重叠度

**Entailment**
> \<entailed>,\<non-entailed>     ([Rashkin 等。, 2021, p. 5](zotero://select/library/items/DWRRENIU)) ([pdf](zotero://open-pdf/library/items/8WZ3JGIY?page=5&annotation=9XFBXEFT))  
> 笔记：与知识的一致性

## Baselines
[E2E model](https://openreview.net/forum?id=r1l73iRqKm)   
[dodecaDialogue](https://aclanthology.org/2020.acl-main.222/)       [*Code（Parl Model）*](https://parl.ai/projects/dodecadialogue/)


## 实验评测
![[Pasted image 20220706200137.png]]
![[Pasted image 20220706200144.png]]
![[Pasted image 20220706200152.png]]
![[Pasted image 20220706200205.png]]

## 实验结论


## 笔记
