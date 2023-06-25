---
Type: unpublished
Authors: Deeksha Varshney, Akshara Prabhakar, Asif Ekbal
Year: 2022
Title: Commonsense and Named Entity Aware Knowledge Grounded Dialogue Generation
Journal: arxiv:2205.13928 [cs]
DOI: 10.48550/arXiv.2205.13928
Publisher: arXiv
---

#  (2022)Commonsense and Named Entity Aware Knowledge Grounded Dialogue Generation
###                  ——Deeksha Varshney, Akshara Prabhakar, Asif Ekbal
[*Read it now! See in Zotero*](zotero://select/items/@CommonsenseNamedEntity2022varshney)
**Web:** [Open online](http://arxiv.org/abs/2205.13928)
**Citekey:** CommonsenseNamedEntity2022varshney
**Tags:** #实体链接 #未完 
**Code:** [*Available Here*](https://github.com/deekshaVarshney/CNTF; https://www.iitp.ac.in/-ai-nlp-ml/resources/ codes/CNTF.zip)


## 摘要
Grounding dialogue on external knowledge and interpreting linguistic patterns in dialogue history context, such as ellipsis, anaphora, and co-references is critical for dialogue comprehension and generation. In this paper, we present a novel open-domain dialogue generation model which effectively utilizes the large-scale commonsense and named entity based knowledge in addition to the unstructured topic-specific knowledge associated with each utterance. We enhance the commonsense knowledge with named entity-aware structures using co-references. Our proposed model utilizes a multi-hop attention layer to preserve the most accurate and critical parts of the dialogue history and the associated knowledge. In addition, we employ a Commonsense and Named Entity Enhanced Attention Module, which starts with the extracted triples from various sources and gradually finds the relevant supporting set of triples using multi-hop attention with the query vector obtained from the interactive dialogue-knowledge module. Empirical results on two benchmark dataset demonstrate that our model significantly outperforms the state-of-the-art methods in terms of both automatic evaluation metrics and human judgment. Our code is publicly available at \href{https://github.com/deekshaVarshney/CNTF}{https://github.com/deekshaVarshney/CNTF}; \href{https://www.iitp.ac.in/~ai-nlp-ml/resources/codes/CNTF.zip}{https://www.iitp.ac.in/-ai-nlp-ml/resources/ codes/CNTF.zip}.

## 总结
利用AllenNLP实体共指、NER和ConceptNet构造实体关系图，然后基于此图做Multi-hop注意力，实现显式地模拟实体级别的对话引导
  
## 研究动机
建模命名实体在对话历史和知识中的引用

## 研究背景/ 问题描述


## 方法的创新点
使用实体共指消除代词，以方便实体识别
> Firstly, we use AllenNLP co-reference resolution module to identify co-reference chains in the dialogue.     ([Varshney 等。, 2022, p. 5](zotero://select/library/items/2SMW7IBQ)) ([pdf](zotero://open-pdf/library/items/9NY3VVNF?page=5&annotation=K98PB9YQ))
> 
> using the first co-reference chain: \[The Last of the Mohicans: it, that movie, It\] we rewrite the dialogue with resolved mentions in the utterances as: “\[The Last of the Mohicans\] is a 1992 American epic historical drama \[The Last of the Mohicans\] is also one of my favorite movies. Me too. I love \[The Last of the Mohicans\] and the soundtrack in particular. \[The Last of the Mohicans\] was directed by Michael Mann, based on \[James Fenimore Cooper’s eponymous 1826\] novel and so on".     ([Varshney 等。, 2022, p. 5](zotero://select/library/items/2SMW7IBQ)) ([pdf](zotero://open-pdf/library/items/9NY3VVNF?page=5&annotation=RFZFCK3L))

对新的句子进行NER
> then use Spacy Named Entity tagging module to recognize named entities from the augmented dialogue.     ([Varshney 等。, 2022, p. 5](zotero://select/library/items/2SMW7IBQ)) ([pdf](zotero://open-pdf/library/items/9NY3VVNF?page=5&annotation=PXFNUX52))

最后再使用ConceptNet识别所有Concept words并建立边
> The new set of triples is obtained using the named entities and concepts as nodes, and the corresponding edges are built as follows:     ([Varshney 等。, 2022, p. 5](zotero://select/library/items/2SMW7IBQ)) ([pdf](zotero://open-pdf/library/items/9NY3VVNF?page=5&annotation=AD9YQ9VP))
> - between every pair of named entities that appear in the same dialogue     ([Varshney 等。, 2022, p. 5](zotero://select/library/items/2SMW7IBQ)) ([pdf](zotero://open-pdf/library/items/9NY3VVNF?page=5&annotation=YTIJ3ZYI))
> - between a named entity node and other concepts within the same dialogue     ([Varshney 等。, 2022, p. 5](zotero://select/library/items/2SMW7IBQ)) ([pdf](zotero://open-pdf/library/items/9NY3VVNF?page=5&annotation=ZUYBUSVK))


> 需要注意的是，为了使多轮对话间的实体建立关系，使用实体共指消除代词是必要的（所有Turns中的相同实体都会被视为一个Concept Node）


## Baselines
[Transformer Memory Network (TMN)（2018）](https://arxiv.org/abs/1811.01241)        [*Code*](https://github.com/facebookresearch/ParlAI/tree/main/projects/wizard_of_wikipedia)
> To encode dialogue, a shared transformer-based encoder is used. After knowledge selection, memory networks are used to reencode the dialogue information. Finally, a transformer decoder is used to decode the responses.

[DialogGPT<sub>finetune</sub>（2020）](https://arxiv.org/abs/2011.09708)
> It utilises a DialoGPT (345M) model fine-tuned on training examples from the Topical Chat dataset to determine whether the pre-trained models can serve as knowledge bases for open-domain dialogue generation.

[Incremental Transformer with Deliberation Decoder (ITDD)（2019 ACL）](https://arxiv.org/abs/1907.08854)       [*Code*](https://github.com/lizekang/ITDD)
> It uses an incremental transformer-based model to encode utterances and documents and a deliberation decoder to decode responses.

[Disentangled Response Decoder (DRD)（2019 ICLR）](https://arxiv.org/abs/2002.10348)   
> It is made up of three modules: a language model, a context processor, and a knowledge processor for decoding responses. The response decoder is broken down into independent components in this case to investigate knowledgebased dialogue generation.

[ConKADI（2020 ACL）](https://aclanthology.org/2020.acl-main.515/)           [*Code*](https://github.com/pku-sixing/ACL2020-ConKADI)
> It includes a Felicitous Fact mechanism to help the model focus on knowledge facts that are highly significant; additionally, two techniques, Context-Knowledge Fusion and Flexible Mode Fusion, are proposed to assist ConKADI in integrating the knowledge information.

[KnowledGPT（2020 EMNLP）](https://aclanthology.org/2020.emnlp-main.272/)         [*Code*](https://github.com/zhaoxlpku/KnowledGPT)
> This model implements response generation by combining a pre-trained language model with a knowledge selection module, and it intends to jointly optimize knowledge selection and response generation with unlabeled dialogues using an unsupervised approach.

## 实验评测
![[Pasted image 20220629123734.png]]

## 实验结论


## 笔记
