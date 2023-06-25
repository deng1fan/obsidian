---
Type: unpublished
Authors: Ruibo Liu, Guoqing Zheng, Shashank Gupta, Radhika Gaonkar, Chongyang Gao, Soroush Vosoughi, Milad Shokouhi, Ahmed Hassan Awadallah
Year: 2022
Title: Knowledge Infused Decoding
Journal: arxiv:2204.03084 [cs]
DOI: 10.48550/arXiv.2204.03084
Publisher: arXiv
---

#  (2022)Knowledge Infused Decoding
###                  ——Ruibo Liu, Guoqing Zheng, Shashank Gupta, Radhika Gaonkar, Chongyang Gao, Soroush Vosoughi, Milad Shokouhi, Ahmed Hassan Awadallah
[*Read it now! See in Zotero*](zotero://select/items/@KnowledgeInfusedDecoding2022liu)
**Web:** [Open online](http://arxiv.org/abs/2204.03084)
**Citekey:** KnowledgeInfusedDecoding2022liu
**Tags:** #ICLR, #WoW #未完 
**Code:** [*Available Here*](Language Models that Seek for Knowledge: Modular Search & Generation for Dialogue and Prompt Completion)


## 摘要
Pre-trained language models (LMs) have been shown to memorize a substantial amount of knowledge from the pre-training corpora; however, they are still limited in recalling factually correct knowledge given a certain context. Hence, they tend to suffer from counterfactual or hallucinatory generation when used in knowledge-intensive natural language generation (NLG) tasks. Recent remedies to this problem focus on modifying either the pre-training or task fine-tuning objectives to incorporate knowledge, which normally require additional costly training or architecture modification of LMs for practical applications. We present Knowledge Infused Decoding (KID) – a novel decoding algorithm for generative LMs, which dynamically infuses external knowledge into each step of the LM decoding. Specifically, we maintain a local knowledge memory based on the current context, interacting with a dynamically created external knowledge trie, and continuously update the local memory as a knowledge-aware constraint to guide decoding via reinforcement learning. On six diverse knowledge-intensive NLG tasks, task-agnostic LMs (e.g., GPT-2 and BART) armed with KID outperform many task-optimized state-of-the-art models, and show particularly strong performance in few-shot scenarios over seven related knowledge-infusion techniques. Human evaluation confirms KID's ability to generate more relevant and factual language for the input context when compared with multiple baselines. Finally, KID also alleviates exposure bias and provides stable generation quality when generating longer sequences. Code for KID is available at https://github.com/microsoft/KID.

## 总结

  
## 研究动机


## 研究背景/ 问题描述


## 方法的创新点


## Baselines
[]()       [*Code*]()
> 

## 实验评测


## 实验结论


## 笔记
