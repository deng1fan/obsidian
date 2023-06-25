---
Type: unpublished
Authors: Nouha Dziri, Sivan Milton, Mo Yu, Osmar Zaiane, Siva Reddy
Year: 2022
Title: On the Origin of Hallucinations in Conversational Models: Is it the Datasets or the Models?
Journal: arxiv:2204.07931 [cs]
DOI: 
Publisher: arXiv
---

#  (2022)On the Origin of Hallucinations in Conversational Models: Is it the Datasets or the Models?
###                  ——Nouha Dziri, Sivan Milton, Mo Yu, Osmar Zaiane, Siva Reddy
[*Read it now! See in Zotero*](zotero://select/items/@OriginHallucinationsConversational2022dziri)
**Web:** [Open online](http://arxiv.org/abs/2204.07931)
**Citekey:** OriginHallucinationsConversational2022dziri
**Tags:**  #幻觉回复 #数据分析 #粗读 #NAACL #数据集
**Code:** [*Available Here*](https://github.com/McGill-NLP/FaithDial)


## 摘要
Knowledge-grounded conversational models are known to suffer from producing factually invalid statements, a phenomenon commonly called hallucination. In this work, we investigate the underlying causes of this phenomenon: is hallucination due to the training data, or to the models? We conduct a comprehensive human study on both existing knowledge-grounded conversational benchmarks and several state-of-the-art models. Our study reveals that the standard benchmarks consist of >60% hallucinated responses, leading to models that not only hallucinate but even amplify hallucinations. Our findings raise important questions on the quality of existing datasets and models trained using them. We make our annotations publicly available for future research.

## 总结
本文主要研究了对话系统中幻觉回复的来源：数据集 or 模型
通过分析了三个主流知识对话数据集发现，数据集中超过60%的回复都存在幻觉
而且模型会进一步放大幻觉
> more than 60% of the responses are hallucinated in the three datasets     ([Dziri 等。, 2022, p. 2](zotero://select/library/items/WATYE2I7)) ([pdf](zotero://open-pdf/library/items/C7XV2378?page=2&annotation=RSE7TJTV))

> generated responses consist of an even larger portion of hallucinations, in comparison with the training data.     ([Dziri 等。, 2022, p. 2](zotero://select/library/items/WATYE2I7)) ([pdf](zotero://open-pdf/library/items/C7XV2378?page=2&annotation=JSGSPFQ3))

## 研究动机
现有的关于解决幻觉回复的论文都集中于从模型入手，并没有分析过幻觉的真正来源是来自于模型还是数据本身，因此本文旨在探究幻觉的来源是数据还是模型

## 研究背景/ 问题描述
一方面，基于知识的会话基准可能包含幻觉，这是由于容易出错的收集协议，或者是由于鼓励信息性而非忠实性的设计框架。
另一方面，神经会话模型的设计不一定产生忠实的输出，而是模拟数据的分布特性。
神经语言生成中的幻觉最近在许多领域引起了一些研究人员的注意，包括神经机器翻译（Raunak等人，2021；Wang和Sennrich，2020）和总结（Durmus等人，2020；Kang和Hashimoto，2020）。相反，基于知识的神经对话生成中的幻觉是一个新兴的研究问题（Mielke等人，2020；Shuster等人，2021；Dziri等人，2021a；Rashkin等人，2021b）。现有的大多数工作都通过引入更稳健的训练方法来避免产生输出中的幻觉。Dziri等人（2021a）提出了一个模型，该模型使用知识图提供的事实来减少生成反应中基于实体的幻觉。Rashkin等人（2021b）在训练时添加控制标记，以控制生成更客观的句子和忠实的句子。与我们的工作最接近的是Dziri等人（2021b）和Rashkin等人（2021a），他们引入了用于量化对话系统中归因的框架，而我们对多个基准和模型进行了更细粒度的手动分析。

## 方法的创新点
![[Pasted image 20220701111940.png]]

## Baselines
1、GPT-2
> an autoregressive model which takes as input a concatenation of the knowledge and the history.

2、[DoHA](https://aclanthology.org/2021.naacl-main.338/)
> builds a BARTbased conversational model (Lewis et al., 2020) for knowledge-grounding, with a two-view attention mechanism to handle separately the encoded document and the history during generation.

3、[CTRL](https://aclanthology.org/2021.acl-long.58/)
> augments the GPT2 model with control tokens (Keskar et al., 2019) that guide the generation towards less subjective and more entailed content.

## 实验评测
![[Pasted image 20220701111929.png]]![[Pasted image 20220701111950.png]]![[Pasted image 20220701112000.png]]

## 实验结论
我们的调查从经验上证明，幻觉是对话基准和模型中普遍存在的问题。我们对三个广泛使用的基准的分析表明，它们充满了幻觉，人们使用的最常见的策略是disclosure和edification。此外，我们还表明，在这些基准上训练的对话模型不仅会产生幻觉，而且会放大幻觉，甚至是旨在缓解这一问题的模型。这就要求发布干净的高质量数据，并仔细设计可信赖的对话系统。在此之前，我们强烈建议从业者查看任何数据集的样本，以便在使用或公开发布之前发现可操作的见解。
![[Pasted image 20220701112123.png]]

## 笔记
