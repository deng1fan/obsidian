---
Type: unpublished
Authors: Chujie Zheng, Yunbo Cao, Daxin Jiang, Minlie Huang
Year: 2020
Title: Difference-aware Knowledge Selection for Knowledge-grounded Conversation Generation
Journal: arxiv:2009.09378 [cs]
DOI: 
Publisher: arXiv
---

#  (2020)Difference-aware Knowledge Selection for Knowledge-grounded Conversation Generation
###                  ——Chujie Zheng, Yunbo Cao, Daxin Jiang, Minlie Huang
[*Read it now! See in Zotero*](zotero://select/items/@DifferenceawareKnowledgeSelection2020zheng)
**Web:** [Open online](http://arxiv.org/abs/2009.09378)
**Citekey:** DifferenceawareKnowledgeSelection2020zheng
**Tags:**  #DiffKS, #知识间的差异 #未完 
**Code:** [Available Here](https://github.com/chujiezheng/DiffKS)


## 摘要
In a multi-turn knowledge-grounded dialog, the difference between the knowledge selected at different turns usually provides potential clues to knowledge selection, which has been largely neglected in previous research. In this paper, we propose a difference-aware knowledge selection method. It first computes the difference between the candidate knowledge sentences provided at the current turn and those chosen in the previous turns. Then, the differential information is fused with or disentangled from the contextual information to facilitate final knowledge selection. Automatic, human observational, and interactive evaluation shows that our method is able to select knowledge more accurately and generate more informative responses, significantly outperforming the state-of-the-art baselines. The codes are available at https://github.com/chujiezheng/DiffKS.

## 总结
提出使用当前候选知识与历史选择知识之间的差异性来选择知识
  ![[Pasted image 20220629083348.png]]
## 研究动机
以往的研究大多忽略了会话轮次所选知识之间的差异，而这通常为知识选择提供潜在线索

对话系统在选择知识时容易选择重复知识，这会导致回复的相似性，但如果选择差异性较大的知识有可能会造成上下文不连贯，因此，对话系统应避免与先前选择的知识相差太小或太大，而应选择适当的知识句子，使对话流畅自然。

## 研究背景/ 问题描述


## 方法的创新点
![[Pasted image 20220629083653.png]]
![[Pasted image 20220629083703.png]]
![[Pasted image 20220629083715.png]]


## 实验评测
![[Pasted image 20220629083728.png]]
![[Pasted image 20220629083746.png]]
![[Pasted image 20220629083801.png]]
![[Pasted image 20220629083817.png]]
![[Pasted image 20220629083829.png]]
![[Pasted image 20220629083845.png]]
![[Pasted image 20220629083922.png]]
## 实验结论


## 笔记
![[Pasted image 20220629084139.png]]