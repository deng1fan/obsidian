---
Type: inproceedings
Authors: Sougata Saha, Souvik Das, Rohini Srihari
Year: 2022
Title: Stylistic Response Generation by Controlling Personality Traits and Intent
Journal: Proceedings of the 4th Workshop on NLP for Conversational AI
DOI: 10.18653/v1/2022.nlp4convai-1.16
Publisher: Association for Computational Linguistics
---

#  (2022)Stylistic Response Generation by Controlling Personality Traits and Intent
###                  ——Sougata Saha, Souvik Das, Rohini Srihari
[*Read it now! See in Zotero*](zotero://select/items/@StylisticResponseGeneration2022sahaa)
**Web:** [Open online](https://aclanthology.org/2022.nlp4convai-1.16)
**Citekey:** StylisticResponseGeneration2022sahaa
**Tags:** #可控生成 #ACL #数据集 #对话意图识别
**Code:** [Available Here](https://github.com/sougata-ub/personality-response-generation)


## 摘要
Personality traits influence human actions and thoughts, which is manifested in day to day conversations. Although glimpses of personality traits are observable in existing open domain conversation corpora, leveraging generic language modelling for response generation overlooks the interlocutor idiosyncrasies, resulting in non-customizable personality agnostic responses. With the motivation of enabling stylistically configurable response generators, in this paper we experiment with end-to-end mechanisms to ground neural response generators based on both (i) interlocutor Big-5 personality traits, and (ii) discourse intent as stylistic control codes. Since most of the existing large scale open domain chat corpora do not include Big-5 personality traits and discourse intent, we employ automatic annotation schemes to enrich the corpora with noisy estimates of personality and intent annotations, and further assess the impact of using such features as control codes for response generation using automatic evaluation metrics, ablation studies and human judgement. Our experiments illustrate the effectiveness of this strategy resulting in improvements to existing benchmarks. Additionally, we yield two silver standard annotated corpora with intents and personality traits annotated, which can be of use to the research community.

## 总结
使用**Big 5 personality traits taxonomy**去模拟对话的人格，使用**离散的控制信号**去控制对话时的意图
下面是本文用到的控制信号
![[Pasted image 20220617164215.png]]
  
## 研究动机
为了能更好的的去控制对话的风格，本文提出使用**离散的**、**显式的**控制信号去控制对话的风格

## 研究背景/ 问题描述
**人格特征挖掘**：自动人格检测研究尚处于起步阶段，这可以归因于缺乏公开的大规模人格标注数据集。近年来一些研究者使用CNN、Bert等试图实现自动化的人格标注和检测，直到最近才有研究者推出第一个人工标注的对话数据集。Gjurkovíc等人（2021）发布了第一个大规模Reddit评论数据集，该数据集标有3个人格特征。
**可控文本生成**：相比于人格特征的自动挖掘，可控文本生成有着相对丰富的工作积累。其中比较经典的是CTRL模型和PPLM模型

其中这两个工作感觉挺吸引我，有机会看一下，同时也是本文受到启发的两篇
> Rashkin et al. (2021) explored tackling knowledge hallucination by incorporating control codes, which act as stylistic controls that encourage the model to generate responses that are faithful to the provided evidence. ([pdf](zotero://open-pdf/library/items/WJ3EPVFH?page=2&annotation=KFSLFR8Z))
> ([Saha 等。, 2022, p. 198](zotero://select/library/items/2VQNRAVJ))

> Hedayatnia et al. (2020) proposed a policy driven neural response generator, which generates a response policy, and adheres to it for faithful generation. ([pdf](zotero://open-pdf/library/items/WJ3EPVFH?page=2&annotation=MPJ8NKFK))
> ([Saha 等。, 2022, p. 198](zotero://select/library/items/2VQNRAVJ))

## 方法的创新点
使用预训练模型和辅助数据集的方法自动化的标注数据，之后根据控制信号去增强模型性能。
*将意图与选择知识关联，而不是单纯地根据上文选择知识*
![[Pasted image 20220617175831.png]]

## 实验评测
P-Traits：代表在Pandora数据集上预训练来标注Big five人格特征
E-Traits：代表在Essays数据集上预训练来标注Big five人格特征

![[Pasted image 20220617184652.png]]

![[Pasted image 20220617184747.png]]

![[Pasted image 20220617185321.png]]

## 实验结论
融入人格特征和意图后，模型生成的回复可以更加有效的去控制

## 笔记
*关于数据标注的细节：*
直接使用预训练的Bert来标注原数据集中的意图
> Leveraging the BERT (Devlin et al., 2019) based intent classifier by Saha et al. (2021), we automatically annotate each turn with interlocutor intent. ([pdf](zotero://open-pdf/library/items/WJ3EPVFH?page=3&annotation=APTW36E9))
> ([Saha 等。, 2022, p. 199](zotero://select/library/items/2VQNRAVJ))

使用RoBERTa在两个标注数据集上微调后，用来自动标注本文的原数据集
> Leveraging the Pandora (Gjurkovi ́ c et al., 2021) and the Essays (Pennebaker and King, 2000) datasets, we train models for automatically detecting Big-5 personality traits from text. ([pdf](zotero://open-pdf/library/items/WJ3EPVFH?page=4&annotation=FPJHNSQM))
> ([Saha 等。, 2022, p. 200](zotero://select/library/items/2VQNRAVJ))

除了这两个特征还定义了基于语料库的三个特征：
Attitude：表明立场，使用AllenNLP的文本蕴含分类器去计算对话者之间上下文的一致性分数来代表立场
> Leveraging AllenNLP (Gardner et al., 2017) textual entailment classifier trained on the MNLI (Williams et al., 2018) dataset, we calculate the frequency of contradicting turns between the interlocutors, and classify an interlocutor as positive if no contradictions are found, negative if more than 1 contradictions are found, and neutral otherwise. ([pdf](zotero://open-pdf/library/items/WJ3EPVFH?page=4&annotation=XN4BDZXH))
> ([Saha 等。, 2022, p. 200](zotero://select/library/items/2VQNRAVJ))

Tone：代表说话者的说话调性（偏主观还是偏客观），统计每个人的Tone分布，如果两者之间相差超过10%，就将多的定义为该说话者的调性，否则就认为既有客观又有主观

Length：标明说话者是否是健谈的，如果该说话者的平均每轮回复的单词数超过整个数据集的平均长度，就会被认为健谈

*注意：这三个特征只在Encoder端使用，用来帮助模型预测人格特征和意图识别*
> The corpus based codes are only input to the encoder to aid in trait and intent predictions, and are not used as stylistic control codes.
> (Saha 等。, 2022, p. 201)

*Bart和Blenderbot是本文的Base Model*

**本文产生的标注数据集已在[这里](https://github.com/sougata-ub/personality-response-generation)公开**