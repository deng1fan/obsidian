---
Type: inproceedings
Authors: Haozhe Ji, Minlie Huang
Year: 2021
Title: DiscoDVT: Generating Long Text with Discourse-Aware Discrete Variational Transformer
Journal: Proceedings of the 2021 Conference on Empirical Methods in Natural Language Processing
DOI: 10.18653/v1/2021.emnlp-main.347
Publisher: Association for Computational Linguistics
---

#  (2021)DiscoDVT: Generating Long Text with Discourse-Aware Discrete Variational Transformer
###                  ——Haozhe Ji, Minlie Huang
[*Read it now! See in Zotero*](zotero://select/items/@DiscoDVTGeneratingLong2021ji)
**Web:** [Open online](https://aclanthology.org/2021.emnlp-main.347)
**Citekey:** DiscoDVTGeneratingLong2021ji
**Tags:** #EDU, #长文本生成 #隐变量
**Code:** [*Available Here*](https://github.com/cdjhz/DiscoDVT)

## 摘要
Despite the recent advances in applying pre-trained language models to generate high-quality texts, generating long passages that maintain long-range coherence is yet challenging for these models. In this paper, we propose DiscoDVT, a discourse-aware discrete variational Transformer to tackle the incoherence issue. DiscoDVT learns a discrete variable sequence that summarizes the global structure of the text and then applies it to guide the generation process at each decoding step. To further embed discourse-aware information into the discrete latent representations, we introduce an auxiliary objective to model the discourse relations within the text. We conduct extensive experiments on two open story generation datasets and demonstrate that the latent codes learn meaningful correspondence to the discourse structures that guide the model to generate long texts with better long-range coherence.

## 总结
提出**DISCODVT**模型，使用隐变量去重建文本做领域预训练，然后生成的时候使用Gumbel采样隐变量做生成
  
## 研究动机
尽管最近在应用预训练语言模型生成高质量文本方面取得了一些进展，但生成能够保持长期连贯性的长段落仍然是这些模型的挑战。在本文中，我们提出了DISCDVT，一种话语感知的离散变分变换器来解决非相干问题。DISCDVT学习一个离散变量序列，该序列总结了文本的全局结构，然后将其应用于指导每个解码步骤的生成过程。为了进一步将话语感知信息嵌入到离散的潜在表示中，我们引入了一个辅助目标来模拟文本中的话语关系。我们在两个开放的故事生成数据集上进行了大量实验，证明潜在代码学习到与话语结构的有意义对应，从而引导模型生成具有更好长期连贯性的长文本。

## 研究背景/ 问题描述


## 方法的创新点
![[Pasted image 20220722071107.png]]

> the bottleneck controls the information capacity of z by mapping continuous representations to a discrete space.     ([Ji 和 Huang, 2021, p. 4211](zotero://select/library/items/WUI7BB5X)) ([pdf](zotero://open-pdf/library/items/S9ZV5XMY?page=4&annotation=VB29QXF4))  
> 笔记：将连续变量映射到离散变量，以确保隐变量能够包含文本重建的重要信息

> to backpropagate gradients, we apply the Gumbel-Softmax trick (Jang et al., 2017; Maddison et al., 2017) to provide a differentiable relaxation of the argmax operation.     ([Ji 和 Huang, 2021, p. 4211](zotero://select/library/items/WUI7BB5X)) ([pdf](zotero://open-pdf/library/items/S9ZV5XMY?page=4&annotation=HHZZDHSG))  
> 笔记：使用Gumbel采样确保梯度传播


## Baselines
```ad-note
title: 注意
Baseline也是使用BRAT做Backbone，并且Seq2Seq模型使用的是未使用预训练参数的BART

```

![[Pasted image 20220725191620.png]]
![[Pasted image 20220725191636.png]]
## 实验评测
![[Pasted image 20220725191440.png]]
![[Pasted image 20220725191447.png]]
![[Pasted image 20220725191458.png]]
![[Pasted image 20220725191517.png]]
## 实验结论


## 笔记
