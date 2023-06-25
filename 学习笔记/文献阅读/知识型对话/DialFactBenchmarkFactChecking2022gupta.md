---
Type: unpublished
Authors: Prakhar Gupta, Chien-Sheng Wu, Wenhao Liu, Caiming Xiong[[Day Planner-20220718]]
Year: 2022
Title: DialFact: A Benchmark for Fact-Checking in Dialogue
Journal: arxiv:2110.08222 [cs]
DOI: 
Publisher: arXiv
---

#  (2022)DialFact: A Benchmark for Fact-Checking in Dialogue
###                  ——Prakhar Gupta, Chien-Sheng Wu, Wenhao Liu, Caiming Xiong
[*Read it now! See in Zotero*](zotero://select/items/@DialFactBenchmarkFactChecking2022gupta)
**Web:** [Open online](http://arxiv.org/abs/2110.08222)
**Citekey:** DialFactBenchmarkFactChecking2022gupta
**Tags:** #数据集 #知识一致性
**Code:** [*Available Here*](https://github.com/salesforce/DialFact)


## 摘要
Fact-checking is an essential tool to mitigate the spread of misinformation and disinformation. We introduce the task of fact-checking in dialogue, which is a relatively unexplored area. We construct DialFact, a testing benchmark dataset of 22,245 annotated conversational claims, paired with pieces of evidence from Wikipedia. There are three sub-tasks in DialFact: 1) Verifiable claim detection task distinguishes whether a response carries verifiable factual information; 2) Evidence retrieval task retrieves the most relevant Wikipedia snippets as evidence; 3) Claim verification task predicts a dialogue response to be supported, refuted, or not enough information. We found that existing fact-checking models trained on non-dialogue data like FEVER fail to perform well on our task, and thus, we propose a simple yet data-efficient solution to effectively improve fact-checking performance in dialogue. We point out unique challenges in DialFact such as handling the colloquialisms, coreferences and retrieval ambiguities in the error analysis to shed light on future research in this direction.

## 总结
![[Pasted image 20220718155324.png]]
  
## 研究动机


## 研究背景/ 问题描述


## 方法的创新点
> **Negation** ：We use the 42 rule-based transformations from Thorne et al. (2019) which apply to verb phrases of the claims to convert them to their negated versions by adding words like “not” or “no”. It typically creates REFUTED claims.     ([Gupta 等。, 2022, p. 3](zotero://select/library/items/RDW39Z57)) ([pdf](zotero://open-pdf/library/items/38VZGGZZ?page=3&annotation=CZKK2NXZ))  
> 笔记：肯定变否定的转换：添加否定词

> **Substitution** ：We perform three types of substitutions: For 1) Context and knowledge-based entity substitution, we first run SpaCy NER tagging (Honnibal and Montani, 2017) on a response ui from WoW. We then swap an entity in the response ui with an entity from either its conversation context C or its background knowledge articles set Ki. An entity is only swapped if it is present in ki, the original knowledge sentence to avoid swaps which do not change the facts. Entities are swapped within their types. For 2) Sense-based substitution, we swap an entity in ui with an entity with a similar “sense” returned from the sense2vec (Trask et al., 2015) library. For 3) Adjective substitution, we substitute adjectives in a claim (ignoring adjectives related to emotions, such as “happy”) with their WordNet (Miller, 1998) antonyms (for example best is replaced with worst). These operations typically create REFUTED claims.     ([Gupta 等。, 2022, p. 3](zotero://select/library/items/RDW39Z57)) ([pdf](zotero://open-pdf/library/items/38VZGGZZ?page=3&annotation=ND7PB6H7))  
> 笔记：替换：基于NER的知识中实体替换、基于语义相似度的实体的替换、基于WordNet的形容词的替换

> **Mask-and-Fill** ：This method generates claims in two stages: 1) Mask salient words from the original claims, and 2) Substitute those words with their alternates using a language model.     ([Gupta 等。, 2022, p. 3](zotero://select/library/items/RDW39Z57)) ([pdf](zotero://open-pdf/library/items/38VZGGZZ?page=3&annotation=LTWCAF39))  
> 笔记：先Mask再使用语言模型去填充，然后替换知识证据以生成不同类型的回复

![[Pasted image 20220718155341.png]]
![[Pasted image 20220718155702.png]]

## Baselines
[VitaminC](https://aclanthology.org/2021.naacl-main.52/)       [*Code*](https://github.com/TalSchuster/VitaminC)
![[Pasted image 20220718163051.png]]



## 实验评测
![[Pasted image 20220718161554.png]]
![[Pasted image 20220718161537.png]]
![[Pasted image 20220718155954.png]]

## 实验结论
我们提出了一个新的基准DIALFACT，用于在基于Wikipedia数据集向导中的固定对话创建的对话中进行事实检查。除了人工编写的响应声明外，我们还创建了具有矛盾、填充和替换等操作的合成声明。我们聘请合格的人群工作者将回答注释为不可验证、支持、反驳或NOTENOUGHINFORMATION类别以及相应的证据。我们从经验上指出，现有的基于非对话数据的事实检查模型不能很好地执行我们的任务。我们演示了如何利用自动生成的响应作为弱监督信号来提高性能。我们希望DIALFACT能够促进对话社区中的事实检查、一致性建模和评估研究。

## 笔记
> We use the MediaWiki API2 to find a set of relevant Wikipedia pages Pc for nk.     ([Gupta 等。, 2022, p. 4](zotero://select/library/items/RDW39Z57)) ([pdf](zotero://open-pdf/library/items/38VZGGZZ?page=4&annotation=DFT64BFI))  
> 笔记：查找Wikipedia的相关文章