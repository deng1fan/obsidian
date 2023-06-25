---
Type: unpublished
Authors: Xueliang Zhao, Tingchen Fu, Chongyang Tao, Wei Wu, Dongyan Zhao, Rui Yan
Year: 2022
Title: Learning to Express in Knowledge-Grounded Conversation
Journal: arxiv:2204.05805 [cs]
DOI: 
Publisher: arXiv
---

#  (2022)Learning to Express in Knowledge-Grounded Conversation
###                  ——Xueliang Zhao, Tingchen Fu, Chongyang Tao, Wei Wu, Dongyan Zhao, Rui Yan
[*Read it now! See in Zotero*](zotero://select/items/@LearningExpressKnowledgeGrounded2022zhao)
**Web:** [Open online](http://arxiv.org/abs/2204.05805)
**Citekey:** LearningExpressKnowledgeGrounded2022zhao
**Tags:** #隐变量 #Zero-Resource  #未完 
**Code:** 暂无


## 摘要
Grounding dialogue generation by extra knowledge has shown great potentials towards building a system capable of replying with knowledgeable and engaging responses. Existing studies focus on how to synthesize a response with proper knowledge, yet neglect that the same knowledge could be expressed differently by speakers even under the same context. In this work, we mainly consider two aspects of knowledge expression, namely the structure of the response and style of the content in each part. We therefore introduce two sequential latent variables to represent the structure and the content style respectively. We propose a segmentation-based generation model and optimize the model by a variational approach to discover the underlying pattern of knowledge expression in a response. Evaluation results on two benchmarks indicate that our model can learn the structure style defined by a few examples and generate responses in desired content style.

## 总结
提出一个将回复拆解为多种结构的模型![[Pasted image 20220630103350.png]]
按照structure style（知识相关还是知识无关）和content style（积极还是消极）对回复进行标记，并使用两个**隐变量来模拟风格的转化**
  
## 研究动机
以往的模型都在研究如何基于合适的知识去生成回复，却忽略了相同的知识也可以生成不同风格的回复，为了建模在相同知识的条件下生成多种风格的回复，提出将回复拆解为不同风格组成的小片段来模拟风格的转化

## 研究背景/ 问题描述


## 方法的创新点
使用现有的工具来对回复进行风格片段的自动化标注，然后使用隐变量来指导模型应该生成什么风格的回复
![[Pasted image 20220630104104.png]]

## Baselines
**For structure style（知识相关还是知识无关）**
[BART](https://arxiv.org/abs/1910.13461)  
> a model that achieves state-of-theart performance on various text generation tasks. Note that **our model degrades into BART once we remove the module indicator Z and the boundary indicator M**

[ZRKGC](https://arxiv.org/abs/2008.12918)       [*Code*](https://github.com/nlpxucan/ZRKGC)
> a model that is based on UniLM (Dong et al., 2019) and optimized with Generalized EM method.

**For the content style（积极还是消极）**
[ECM](https://arxiv.org/abs/1704.01074)       [*Code*](https://github.com/thu-coai/ecm)
>a model which can generate appropriate responses not only content-relevant but also emotional consistent

[DialoGPT](https://arxiv.org/abs/1911.00536)       [*Code*](https://github.com/microsoft/DialoGPT)
>We **add a sentiment indicating token** at the first of the sequence and explore whether such simple heuristics works for controlling knowledge expression

[CTRL](https://arxiv.org/abs/1909.05858)       [*Code*](https://github.com/salesforce/ctrl)
>a large-scale model trained on conditional codes to govern the style and content of generation.


## 实验评测
![[Pasted image 20220630102409.png]]
![[Pasted image 20220630102440.png]]
![[Pasted image 20220630102506.png]]
![[Pasted image 20220630102521.png]]
> the average proportion of knowledge-related segments (pklg) in a sentence     ([Zhao 等。, 2022, p. 8](zotero://select/library/items/Q764P5LV)) ([pdf](zotero://open-pdf/library/items/XK68YYGB?page=8&annotation=V74LWGES))
> the average proportion of words belonging to knowledge-related segments (lklg)     ([Zhao 等。, 2022, p. 8](zotero://select/library/items/Q764P5LV)) ([pdf](zotero://open-pdf/library/items/XK68YYGB?page=8&annotation=TEIFTEGB))

## 实验结论
我们探讨了基于知识的对话中的知识表达，并将回复的表达方式分解为回复的结构（结构风格）和每个部分的内容风格（内容风格）。我们提出了一种基于（ #ELBO ）的生成模型来发现潜在的表达风格。具体而言，我们引入了两个潜在变量，分别对这两个方面的表达风格进行建模。对该任务的两个基准测试的评估结果表明，我们的模型能够以很低的成本学习结构样式，并且在没有任何人工注释数据的情况下生成所需内容样式的响应。

## 笔记
1、决定使用哪个模块的隐变量仅仅在一个片段完成的时候发生转变
> The transition of zt occurs only when a segment is completed, which is decided by the binary boundary variable M .     ([Zhao 等。, 2022, p. 3](zotero://select/library/items/Q764P5LV)) ([pdf](zotero://open-pdf/library/items/XK68YYGB?page=3&annotation=XLDDDGYT))

2、使用**全连接 + Softmax实现隐变量的预测**

3、使用**全连接 + Sigmoid**实现对片段边界的预测
> model the distribution pθm(mt|r≤t, zt) by a Bernoulli distribution parameterized by σ(fm−mlp(\[e<sub>t</sub>; h<sub>t</sub><sup>N,dec</sup>  \])), where σ denotes the sigmoid function.     ([Zhao 等。, 2022, p. 4](zotero://select/library/items/Q764P5LV)) ([pdf](zotero://open-pdf/library/items/XK68YYGB?page=4&annotation=4FA5IPNJ))
> (这里的伯努利分布其实就是Sigmoid)
> m<sub>0</sub> = 1

4、当隐变量z<sub>t</sub> >= 2 时，模型在解码时将使用带有Adapter的DecoderLayer进行解码（前两种都是普通的DecoderLayer，前两者的区别在于输入是知识还是对话历史）
> To make the style fine-grained and adjustable, each style has a unique set of adapters.     ([Zhao 等。, 2022, p. 5](zotero://select/library/items/Q764P5LV)) ([pdf](zotero://open-pdf/library/items/XK68YYGB?page=5&annotation=K5PV2654))

5、使用StandFordNLP Toolkit将回复分割成片段
> use StanfordNLP toolkit (Manning et al., 2014) to parse every response in the training set as a sequence of segments     ([Zhao 等。, 2022, p. 5](zotero://select/library/items/Q764P5LV)) ([pdf](zotero://open-pdf/library/items/XK68YYGB?page=5&annotation=HKX2NBLL))

6、使用少量的目标语料的训练语料训练，并不算严格的 #Zero-Resource 
> we first train the model on the Reddit Corpus and then fine-tune it on a small amount of examples in Wizard and CMU_DoG, respectively.     ([Zhao 等。, 2022, p. 6](zotero://select/library/items/Q764P5LV)) ([pdf](zotero://open-pdf/library/items/XK68YYGB?page=6&annotation=XRPW7UHC))

7、文中好像只关注了积极和消极两种风格
> we are primarily concerned with generating with two kinds of styles, positive and negative     ([Zhao 等。, 2022, p. 6](zotero://select/library/items/Q764P5LV)) ([pdf](zotero://open-pdf/library/items/XK68YYGB?page=6&annotation=UTR54SHV))

8、使用基于Roberta-base的知识选择器（在Reddit Corpus上预训练）选择top-7
> employ a knowledge selection(KS) module to select the top 7 related sentences in knowledge.     ([Zhao 等。, 2022, p. 13](zotero://select/library/items/Q764P5LV)) ([pdf](zotero://open-pdf/library/items/XK68YYGB?page=13&annotation=VEGXDRCJ))

9、Encoder-Decoder架构基于BART-Base（在Reddit Corpus上预训练）
> The encoder-decoder architecture is implemented on the basis of Bartbase(139M) and trained on the Reddit Corpus with a batch size of 64 and an initial learning rate of 5e − 6.     ([Zhao 等。, 2022, p. 13](zotero://select/library/items/Q764P5LV)) ([pdf](zotero://open-pdf/library/items/XK68YYGB?page=13&annotation=26JMC65P))