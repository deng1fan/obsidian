---
Type: unpublished
Authors: Haopeng Zhang, Semih Yavuz, Wojciech Kryscinski, Kazuma Hashimoto, Yingbo Zhou
Year: 2022
Title: Improving the Faithfulness of Abstractive Summarization via Entity Coverage Control
Journal: arxiv:2207.02263 [cs]
DOI: 
Publisher: arXiv
---

#  (2022)Improving the Faithfulness of Abstractive Summarization via Entity Coverage Control
###                  ——Haopeng Zhang, Semih Yavuz, Wojciech Kryscinski, Kazuma Hashimoto, Yingbo Zhou
[*Read it now! See in Zotero*](zotero://select/items/@ImprovingFaithfulnessAbstractive2022zhang)
**Web:** [Open online](http://arxiv.org/abs/2207.02263)
**Citekey:** ImprovingFaithfulnessAbstractive2022zhang
**Tags:**  #幻觉 #粗读
**Code:** 暂无


## 摘要
Abstractive summarization systems leveraging pre-training language models have achieved superior results on benchmark datasets. However, such models have been shown to be more prone to hallucinate facts that are unfaithful to the input context. In this paper, we propose a method to remedy entity-level extrinsic hallucinations with Entity Coverage Control (ECC). We first compute entity coverage precision and prepend the corresponding control code for each training example, which implicitly guides the model to recognize faithfulness contents in the training phase. We further extend our method via intermediate fine-tuning on large but noisy data extracted from Wikipedia to unlock zero-shot summarization. We show that the proposed method leads to more faithful and salient abstractive summarization in supervised fine-tuning and zero-shot settings according to our experimental results on three benchmark datasets XSum, Pubmed, and SAMSum of very different domains and styles.

## 总结
使用实体覆盖精度来衡量对知识的使用程度，并提高回复的忠诚度，减少幻觉生成
并在此之外，还使用数据集标识符将多个数据集融合到一起训练，数据集标识符和实体覆盖标记同时作为控制信号
  
## 研究动机
使用预训练模型难免会出现幻觉，为了提高回复的忠诚度，提出了基于实体覆盖精度的可控模型

## 研究背景/ 问题描述


## 方法的创新点
> ![[Pasted image 20220724195401.png]]
> We first compute entity coverage precision precen for each document and reference summary pair (di, si) in the training set D. Then, we quantize precen into k discrete bins, each representing a range of entity faithfulness. These bin boundaries are selected to ensure that each bin contains roughly the same number of training examples to avoid data imbalance. We then represent each bin by a special token control code Ci and add all these special tokens {C1, C2, ..., Ck} to the input vocabulary of our seq2seq model.     ([Zhang 等。, 2022, p. 2](zotero://select/library/items/VMQUURR7)) ([pdf](zotero://open-pdf/library/items/PWZE9AHK?page=2&annotation=NGI3YEUQ))  
> 笔记：这不就是知识使用程度吗？按照覆盖率精度划分为几个区间，然后使用控制信号代表

> \<FF-low>, \<FF-mid> and \<FF-high>     ([Zhang 等。, 2022, p. 3](zotero://select/library/items/VMQUURR7)) ([pdf](zotero://open-pdf/library/items/PWZE9AHK?page=3&annotation=7NPGVZNN))  
> 笔记：三类标签

## Baselines
BART

## 实验评测
![[Pasted image 20220724195312.png]]
![[Pasted image 20220724195321.png]]
![[Pasted image 20220724195332.png]]
![[Pasted image 20220724195343.png]]

## 实验结论


## 笔记
