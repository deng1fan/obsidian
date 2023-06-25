---
Type: inproceedings
Authors: Shaoxiong Feng, Xuancheng Ren, Hongshen Chen, Bin Sun, Kan Li, Xu Sun
Year: 2020
Title: Regularizing Dialogue Generation by Imitating Implicit Scenarios
Journal: Proceedings of the 2020 Conference on Empirical Methods in Natural Language Processing (EMNLP)
DOI: 10.18653/v1/2020.emnlp-main.534
Publisher: Association for Computational Linguistics
---

#  (2020)Regularizing Dialogue Generation by Imitating Implicit Scenarios
###                  ——Shaoxiong Feng, Xuancheng Ren, Hongshen Chen, Bin Sun, Kan Li, Xu Sun
[*Read it now! See in Zotero*](zotero://select/items/@RegularizingDialogueGeneration2020feng)
**Web:** [Open online](https://aclanthology.org/2020.emnlp-main.534)
**Citekey:** RegularizingDialogueGeneration2020feng
**Tags:** #对话场景
**Code:** [*Available Here*]()


## 摘要
Human dialogues are scenario-based and appropriate responses generally relate to the latent context knowledge entailed by the specific scenario. To enable responses that are more meaningful and context-specific, we propose to improve generative dialogue systems from the scenario perspective, where both dialogue history and future conversation are taken into account to implicitly reconstruct the scenario knowledge. More importantly, the conversation scenarios are further internalized using imitation learning framework, where the conventional dialogue model that has no access to future conversations is effectively regularized by transferring the scenario knowledge contained in hierarchical supervising signals from the scenario-based dialogue model, so that the future conversation is not required in actual inference. Extensive evaluations show that our approach significantly outperforms state-of-the-art baselines on diversity and relevance, and expresses scenario-specific knowledge.

## 总结
[论文分享视频](https://www.bilibili.com/video/BV1Q44y137xy/?spm_id_from=333.788&vd_source=15b1ecaee67a0e28fcffaa484b6d5482)

> 本文提出的研究角度很不错，提出了场景对对话的影响，但是本文简化了场景的概念，为了去隐式的建模场景，本文将历史对话和未来对话作为对话的场景，简单点说就是用未来对话代表了对话场景，在训练的时候融入了未来对话的信息，再通过模仿学习传递给先验的学生模型

## 研究动机
![[Pasted image 20220630123848.png]]

## 研究背景/ 问题描述
人类在对话时是基于场景的，我们可以将给定的对话扩展到许多可能的场景，这些场景是来自我们的经验、知识和一些背景信息，现有对话模型无法访问这些信息，而恰当的回复通常需要这些场景所包含的信息，所以不同的对话场景会对应着不同的恰当回复。作者认为现有的多轮对话语料中就包含着这样的对话场景信息，关于当前话语的历史对话和未来对话隐含地代表了一个特定的对话场景，只是没有被有效地使用，例如给定一个七轮的对话，本文将前三轮为历史对话，后三轮为未来对话，中间一轮是模型要生成的回复。使用历史对话和未来对话隐式地重建对话场景信息，从对话场景的角度改进对话系统。由于推理阶段是没有未来对话的，而训练阶段同时使用历史对话和未来对话，本文使用了模仿学习框架弥补了这种训练阶段和推理阶段之间的差距，同时模仿学习的使用使得模型可以利用更加多样化和丰富的知识。
![[Pasted image 20220630123814.png]]
![[Pasted image 20220630123834.png]]
## 方法的创新点
![[Pasted image 20220630124142.png]]
![[Pasted image 20220630124152.png]]
![[Pasted image 20220630124203.png]]
![[Pasted image 20220630124217.png]]
![[Pasted image 20220630124226.png]]
![[Pasted image 20220630124241.png]]
## Baselines
**LSTM-Based**
[Seq2Seq+Att](https://arxiv.org/abs/1409.3215) *(论文是普通Seq2Seq的论文)*
> which contains a vanilla Seq2Seq model (Sutskever et al., 2014) with attention mechanism (Bahdanau et al., 2015)

[VHRED+BOW](https://arxiv.org/abs/1605.06069)       [*Code*](https://github.com/ctr4si/A-Hierarchical-Latent-Structure-for-Variational-Conversation-Modeling)
>which introduces a continuous latent variable attached to the response information into HRED (Serban et al., 2016) and applies BOW loss (Zhao et al., 2017) as a complementary with KL annealing

[NEXUS](https://arxiv.org/abs/1810.00671)   
>which further uses the future conversation to incorporate more scenario information into the latent variable.![[Pasted image 20220630153612.png]]

**Transformer-Based**
[ReCoSa](https://arxiv.org/abs/1907.05339)      *[Tensorflow代码](https://github.com/zhanghainan/ReCoSa)*

>which further uses the future conversation to incorporate more scenario information into the latent variable.![[Pasted image 20220630154824.png]]

[CHMAM](https://www.researchgate.net/profile/Rui-Yan-27/publication/326201488_Get_The_Point_of_My_Utterance_Learning_Towards_Effective_Responses_with_Multi-Head_Attention_Mechanism/links/5e86018692851c2f52765657/Get-The-Point-of-My-Utterance-Learning-Towards-Effective-Responses-with-Multi-Head-Attention-Mechanism.pdf)  
>which consists of Multi-Head Attention Mechanism (MHAM) and an attention weight regularizer.  Aim to extract more relevant and diverse scenario information from dialogue history.![[Pasted image 20220630153801.png]]

## 实验评测
![[Pasted image 20220630124253.png]]
![[Pasted image 20220630124316.png]]
![[Pasted image 20220630124324.png]]
![[Pasted image 20220630124338.png]]
![[Pasted image 20220630124351.png]]
![[Pasted image 20220630124420.png]]
## 实验结论
![[Pasted image 20220630124503.png]]

## 笔记
