---
Type: unpublished
Authors: Bodhisattwa Prasad Majumder, Harsh Jhamtani, Taylor Berg-Kirkpatrick, Julian McAuley
Year: 2022
Title: Achieving Conversational Goals with Unsupervised Post-hoc Knowledge Injection
Journal: arxiv:2203.11399 [cs]
DOI: 
Publisher: arXiv
---

#  (2022)Achieving Conversational Goals with Unsupervised Post-hoc Knowledge Injection
###                  ——Bodhisattwa Prasad Majumder, Harsh Jhamtani, Taylor Berg-Kirkpatrick, Julian McAuley
[*Read it now! See in Zotero*](zotero://select/items/@AchievingConversationalGoals2022majumderb)
**Web:** [Open online](http://arxiv.org/abs/2203.11399)
**Citekey:** AchievingConversationalGoals2022majumderb
**Tags:** #ACL
**Code:** [*Available Here*]()

## 摘要
A limitation of current neural dialog models is that they tend to suffer from a lack of specificity and informativeness in generated responses, primarily due to dependence on training data that covers a limited variety of scenarios and conveys limited knowledge. One way to alleviate this issue is to extract relevant knowledge from external sources at decoding time and incorporate it into the dialog response. In this paper, we propose a post-hoc knowledge-injection technique where we first retrieve a diverse set of relevant knowledge snippets conditioned on both the dialog history and an initial response from an existing dialog model. We construct multiple candidate responses, individually injecting each retrieved snippet into the initial response using a gradient-based decoding method, and then select the final response with an unsupervised ranking step. Our experiments in goal-oriented and knowledge-grounded dialog settings demonstrate that human annotators judge the outputs from the proposed method to be more engaging and informative compared to responses from prior dialog systems. We further show that knowledge-augmentation promotes success in achieving conversational goals in both experimental settings.

## 总结
提出**POKI(Post-hoc Knowledge Injection in Generated Dialog)** 模型
  
## 研究动机


## 研究背景/ 问题描述


## 方法的创新点

> construct a query using both dialog history H and the initial response xd, and gather a relevant knowledge candidate k from a knowledge source K.     ([Majumder 等。, 2022, p. 2](zotero://select/library/items/P4BTWQ5X)) ([pdf](zotero://open-pdf/library/items/C8QL46D9?page=2&annotation=EPALLMY9))  
> 笔记：将原始回复与对话历史拼接，去检索一个相关知识

> We explore both parametric (e.g querying a language model) and non-parametric (e.g. deterministic retrieval using word-overlap) ways to obtain post-hoc knowledge.     ([Majumder 等。, 2022, p. 2](zotero://select/library/items/P4BTWQ5X)) ([pdf](zotero://open-pdf/library/items/C8QL46D9?page=2&annotation=GGGFZMX9))  
> 笔记：一种是参数化知识检索；一种是非参数化知识检索

> We assemble simple prompts inspired from various knowledge-seeking situations in dialog (Shwartz et al., 2020) such as \[KP\] is famous for , Here is what I know about \[KP\]: > where [KP] is a key-phrase2 extracted from dialog context.      ([Majumder 等。, 2022, p. 2](zotero://select/library/items/P4BTWQ5X)) ([pdf](zotero://open-pdf/library/items/C8QL46D9?page=2&annotation=RQMBPN6N))  
> 笔记：在参数化知识检索中，使用prompt技术检索，使用模板+关键字构建提示

> Next, we identify the top relevant instances in the given corpus with respect to the constructed query using cosine similarity on TF-IDF based representations     ([Majumder 等。, 2022, p. 3](zotero://select/library/items/P4BTWQ5X)) ([pdf](zotero://open-pdf/library/items/C8QL46D9?page=3&annotation=8GBVB8M3))  
> 笔记：使用TF-IDF检索最相关的文本知识

## Baselines
[]()       [*Code*]()
> 

## 实验评测


## 实验结论


## 笔记

