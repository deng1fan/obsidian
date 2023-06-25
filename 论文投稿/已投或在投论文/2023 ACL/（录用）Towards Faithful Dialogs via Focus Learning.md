
## 论文介绍

#### 论文题目：Towards Faithful Dialogs via Focus Learning
#### 作者：邓一帆、张兴盛、黄河燕、胡玥
#### 类型：ACL 2023，Long Paper
#### 论文概述：保持生成回复与给定知识的一致性是构建可靠的知识对话系统的一个重要研究课题。现有的方法因为缺乏一种有效的方法来指导模型在训练过程中注重对知识的理解和利用，从而依赖于额外的模型参数或精心设计的数据工程。为了解决这个问题，我们对以往的方法进行了实验分析，发现模型在微调阶段的学习重点并不是我们所期望的内容，我们认为这阻碍了模型对知识的学习，并提出了一种新颖的学习方法 Focus Learning (FocusL) 来自适应的纠正模型在训练过程中的学习焦点。具体地来说，我们通过对回复中的每一个词的重要性进行了评估，根据评估结果为每个词分配学习的优先级，从而引导模型在训练过程中关注更加重要的知识。实验结果表明，该方法在保持训练稳定性和生成流畅性的同时，显著提高了回复的忠实性和一致性，同时我们还发现我们的模型在低资源场景以及 Out-of-domain 场景下表现依旧优越。我们的方法不需要增加额外的参数开销以及数据预处理成本，简单有效且方便与其他训练方法组合使用。

## CRC 版本

![](../../../_resources/%EF%BC%88%E5%BD%95%E7%94%A8%EF%BC%89Towards%20Faithful%20Dialogs%20via%20Focus%20Learning/final_v11.pdf)


## 参会邀请函

![](../../../_resources/%EF%BC%88%E5%BD%95%E7%94%A8%EF%BC%89Towards%20Faithful%20Dialogs%20via%20Focus%20Learning/a001045-dengyifan.pdf)



## 提交版本
![](../../../_resources/Towards%20Faithful%20Dialogs%20via%20Focus%20Learning/Towards%20Faithful%20Dialogs%20via%20Focus%20Learning.pdf)

## 审稿意见

![](../../../_resources/Towards%20Faithful%20Dialogs%20via%20Focus%20Learning/%E5%AE%A1%E7%A8%BF%E6%84%8F%E8%A7%81.pdf)

## 审稿意见标注

![](../../../_resources/Towards%20Faithful%20Dialogs%20via%20Focus%20Learning/%E5%AE%A1%E7%A8%BF%E6%84%8F%E8%A7%81%E6%A0%87%E6%B3%A8.pdf)

## 回复内容

![](../../../_resources/Towards%20Faithful%20Dialogs%20via%20Focus%20Learning/d71c0dc493f780dd438f43e9ccfb1cff_MD5.png)





