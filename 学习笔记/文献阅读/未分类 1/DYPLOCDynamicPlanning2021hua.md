---
Type: inproceedings
Authors: Xinyu Hua, Ashwin Sreevatsa, Lu Wang
Year: 2021
Title: DYPLOC: Dynamic Planning of Content Using Mixed Language Models for Text Generation
Journal: Proceedings of the 59th Annual Meeting of the Association for Computational Linguistics and the 11th International Joint Conference on Natural Language Processing (Volume 1: Long Papers)
DOI: 10.18653/v1/2021.acl-long.501
Publisher: Association for Computational Linguistics
---

#  (2021)DYPLOC: Dynamic Planning of Content Using Mixed Language Models for Text Generation
###                  ——Xinyu Hua, Ashwin Sreevatsa, Lu Wang
[*Read it now! See in Zotero*](zotero://select/items/@DYPLOCDynamicPlanning2021hua)
**Web:** [Open online](https://aclanthology.org/2021.acl-long.501)
**Citekey:** DYPLOCDynamicPlanning2021hua
**Tags:** #内容规划 #自适应权重
**Code:** [*Available Here*](https://github.com/XinyuHua/dyploc-acl2021)


## 摘要
We study the task of long-form opinion text generation, which faces at least two distinct challenges. First, existing neural generation models fall short of coherence, thus requiring efficient content planning. Second, diverse types of information are needed to guide the generator to cover both subjective and objective content. To this end, we propose DYPLOC, a generation framework that conducts dynamic planning of content while generating the output based on a novel design of mixed language models. To enrich the generation with diverse content, we further propose to use large pre-trained models to predict relevant concepts and to generate claims. We experiment with two challenging tasks on newly collected datasets: (1) argument generation with Reddit ChangeMyView, and (2) writing articles using New York Times' Opinion section. Automatic evaluation shows that our model significantly outperforms competitive comparisons. Human judges further confirm that our generations are more coherent with richer content.

## 总结
提出了**DYPLOC**模型，在BART之外加了个权重生成层（全连接网络，其实就是Gate），实现动态选择内容作为输入去生成
  
## 研究动机
现有的神经生成模型**缺乏连贯性**，因此需要有效的内容规划。
其次，需要不同类型的信息来引导模型**涵盖主观和客观内容**。

## 研究背景/ 问题描述
模型的输入是 **Title 、一组实体 \[ENT] 、 一组概念 \[CON] 、 一句话概述 （可选）\[CLAIM]**
```ad-note
title: Claim生成
> fine-tune another BART model by taking in the title t and the entities Ei, which then produces a claim with nucleus sampling for decoding     ([Hua 等。, 2021, p. 6411](zotero://select/library/items/VEN7ZCKA)) ([pdf](zotero://open-pdf/library/items/TPX4HZPF?page=4&annotation=74V2GPYF))  
> 笔记：使用BART根据题目和实体生成Claim

```

输出是根据输入生成的辩论内容
> faithfully reflect the content items with a coherent structure.     ([Hua 等。, 2021, p. 6410](zotero://select/library/items/VEN7ZCKA)) ([pdf](zotero://open-pdf/library/items/TPX4HZPF?page=3&annotation=BFJ3MJ44))  
> 笔记：生成与输入内容一致性的文本
![[Pasted image 20220726150857.png]]

## 方法的创新点
![[Pasted image 20220726155332.png]]
基于BART添加内容规划模块
> a dynamic content planning generation framework, which is directly built on top of BART.     ([Hua 等。, 2021, p. 6409](zotero://select/library/items/VEN7ZCKA)) ([pdf](zotero://open-pdf/library/items/TPX4HZPF?page=2&annotation=ZFYKF6QG))  
> 笔记：在BART之外加的小模块，可以克服现有的根据注意力或硬拷贝的不可控缺点

> learns to dynamically select and order content based on what has been produced previously while generating the outputs.     ([Hua 等。, 2021, p. 6411](zotero://select/library/items/VEN7ZCKA)) ([pdf](zotero://open-pdf/library/items/TPX4HZPF?page=4&annotation=4YDQ9LWW))  
> 笔记：动态选择输入内容

> propose content plan augmentation by automatically generating relevant concepts and claims     ([Hua 等。, 2021, p. 6409](zotero://select/library/items/VEN7ZCKA)) ([pdf](zotero://open-pdf/library/items/TPX4HZPF?page=2&annotation=H3LMBZ5E))  
> 笔记：数据增强
```ad-note
title: 为什么需要数据增强
> With limited number of entities and concepts as input, generation systems are often incapable of producing long text with rich content, resulting in hallucination     ([Hua 等。, 2021, p. 6410](zotero://select/library/items/VEN7ZCKA)) ([pdf](zotero://open-pdf/library/items/TPX4HZPF?page=3&annotation=G6N2W8ZP))  
> 笔记：有限的实体和概念在生成长文本时可能会出现幻觉，因为提供的信息有限

> concept expansion module g(·), which predicts additional relevant concepts, denoted as C<sup>+</sup><sub>i</sub> , by conditioning on the original content item     ([Hua 等。, 2021, p. 6411](zotero://select/library/items/VEN7ZCKA)) ([pdf](zotero://open-pdf/library/items/TPX4HZPF?page=4&annotation=S3VFWCDK))  
> 笔记：构建一个概念扩充模块

```

> construct two opinion text generation datasets with content plans that capture prominent entities and concepts.     ([Hua 等。, 2021, p. 6409](zotero://select/library/items/VEN7ZCKA)) ([pdf](zotero://open-pdf/library/items/TPX4HZPF?page=2&annotation=IIPMW8W7))  
> 笔记：构建了两个数据集，包含捕捉的实体和概念

## Baselines
![[Pasted image 20220726160701.png]]
此外还比较了一个“强势”Baseline，**使用相同的扩展数据集，只不过是拼接输入，没有动态选择**
```ad-question
title: 疑问
这不就是消融实验吗？？？

```

![[Pasted image 20220726160740.png]]

## 实验评测
![[Pasted image 20220726160959.png]]
![[Pasted image 20220726161131.png]]
![[Pasted image 20220726161144.png]]
![[Pasted image 20220726161158.png]]
![[Pasted image 20220726161213.png]]
## 实验结论
我们提出了一种新的文本生成框架，该框架支持基于混合条件语言模型的动态内容规划。我们进一步采用大型模型，以涵盖客观和主观信息的不同内容来增加系统输入。在两个不同意见文本生成任务上的实验表明，与基于相同输入的微调BART模型的强比较相比，我们提出的模型更具优势。人类评估进一步证实，我们的模型生成具有更丰富的信息和更好的内容组织。

## 笔记
> g(·) can be any conditional predictor, our experiment shows that fine-tuned BART model performs best on our tasks, where it generates C+ i word-by-word by consuming the content item.3     ([Hua 等。, 2021, p. 6411](zotero://select/library/items/VEN7ZCKA)) ([pdf](zotero://open-pdf/library/items/TPX4HZPF?page=4&annotation=JKBCENV3))  
> 笔记：微调BART进行概念扩充

> Segmenter \<s> is added to indicate the change of elements in a content item.     ([Hua 等。, 2021, p. 6411](zotero://select/library/items/VEN7ZCKA)) ([pdf](zotero://open-pdf/library/items/TPX4HZPF?page=4&annotation=JNEK66XY))  
> 笔记：使用\<s>作为分隔符

> extract content item representations {hi}, based on the last layer’s hidden states of the first token.     ([Hua 等。, 2021, p. 6411](zotero://select/library/items/VEN7ZCKA)) ([pdf](zotero://open-pdf/library/items/TPX4HZPF?page=4&annotation=IKGGMJCN))  
> 笔记：使用编码器最后一层的第一个token作为item表示