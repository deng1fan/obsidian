---
Type: inproceedings
Authors: Zhiyong Wu, Wei Bi, Xiang Li, Lingpeng Kong, Ben Kao
Year: 2022
Title: Lexical Knowledge Internalization for Neural Dialog Generation
Journal: Proceedings of the 60th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)
DOI: 10.18653/v1/2022.acl-long.547
Publisher: Association for Computational Linguistics
---

#  (2022)Lexical Knowledge Internalization for Neural Dialog Generation
###                  ——Zhiyong Wu, Wei Bi, Xiang Li, Lingpeng Kong, Ben Kao
[*Read it now! See in Zotero*](zotero://select/items/@LexicalKnowledgeInternalization2022wu)
**Web:** [Open online](https://aclanthology.org/2022.acl-long.547)
**Citekey:** LexicalKnowledgeInternalization2022wu
**Tags:** #ACL, #单词释义 #对比学习
**Code:** 暂无


## 摘要
We propose knowledge internalization (KI), which aims to complement the lexical knowledge into neural dialog models. Instead of further conditioning the knowledge-grounded dialog (KGD) models on externally retrieved knowledge, we seek to integrate knowledge about each input token internally into the model's parameters. To tackle the challenge due to the large scale of lexical knowledge, we adopt the contrastive learning approach and create an effective token-level lexical knowledge retriever that requires only weak supervision mined from Wikipedia. We demonstrate the effectiveness and general applicability of our approach on various datasets and diversified model structures.

## 总结
提出了融入**Token-level Knowledge**来实现知识内化**Knowledge Internalization (KI)** ，通过使用对比学习，在训练阶段使用KI Loss拉近单词与知识（单词释义）的语义距离，在测试阶段就可以脱离对知识的依赖
> At the inference time, those relevant knowledge is no longer required as they have been internalized into model by KI, making inference more efficient. ([pdf](zotero://open-pdf/library/items/BJGILACZ?page=3&annotation=JZIP7KVR))
> ([Wu 等。, 2022, p. 7947](zotero://select/library/items/C98PXND9))

 [[Lexical Knowledge Internalization for Neural Dialog Generation图示]]
## 研究动机
为了避免在推理阶段使用额外的知识并且增加对知识引用的粒度以及多样性，本文将知识融入到了单词的参数里边实现了单次级别的知识引用

## 研究背景/ 问题描述
现有的模型都是在句子级别上检索知识并融入，这样做一是会限制回复的多样性和信息丰富度，二是需要在推理阶段去检索知识造成大量计算，针对这些gap，本文提出了在单词级别上引用知识

## 方法的创新点
1、使用KI Loss 拉近单词与知识的语义距离：
![[Pasted image 20220610110954.png]]
![[Pasted image 20220610111014.png]]


## 实验评测
![[Pasted image 20220610122259.png]]

基于预训练Encoder的模型对比：![[Pasted image 20220610121126.png]]

解码速度的影响：![[Pasted image 20220610121011.png]]

语义空间的可视化：![[Pasted image 20220610120846.png]]

使用不同知识源的影响：![[Pasted image 20220610120735.png]]

## 实验结论
1、提出了将lexical knowledge融入到模型中去，可以提升模型的性能
2、提出了一个有效的知识检索器，可以将词汇与知识进行对齐

## 笔记
1、微调预训练Encoder时并没有冻结参数
> The LMs are fine-tuned together with the decoder. We also experimented with LMs frozen, but this generally works worse. ([pdf](zotero://open-pdf/library/items/BJGILACZ?page=12&annotation=7FMRIZFA))
> ([Wu 等。, 2022, p. 7956](zotero://select/library/items/C98PXND9))

2、全部使用Bert的tokenizer，**但是好像并没有使用预训练模型的词表id**
> with sentences tokenized using BERT’s tokenizer provided by Transformers
> (Wu 等。, 2022, p. 7956)