
```ad-tldr
title: TLDR
#### RLHF 通常需要下面三步：

1. 第一步：收集指令数据，并训练一个基准策略网络。
2. 第二步：收集偏好数据，并训练奖励模型（Reward Model，RM）预测 人类喜欢的输出。
3. 第三步：根据奖励模型使用PPO强化学习算法对基准策略网络优化。

#### 共需要三种数据集：

1. ==SFT数据集==：该数据集用于训练得到基础策略网络（SFT模型），格式通常为 [prompt(instruct), input, response]
2. ==RM数据集==：该数据集记录了标注者对模型输出的偏好排名，该数据集用于RM的训练，格式通常为两两回复之间的偏序 [chosen, reject]
3. ==PPO数据集==：该数据只有输入没有任何人工标签，用于RLHF过程对模型的微调，格式通常和 SFT 一致
三种数据集大小比约为 1:3:3，InstructGPT 中使用了 13K SFT 数据，33K RM 数据，31K PPO 数据
```

## ColossalChat：完整RLHF平替ChatGPT的开源方案

Colossal人工智能是基于加州大学伯克利分校杰出教授James Demmel教授和新加坡国立大学总统青年教授Yang You教授的专业知识开发的。自开源发布以来，Colossal AI已多次在GitHub Trending上排名第一，拥有约20000名GitHub stars，并成功被接受为SC、AAAI、PPoPP、CVPR和ISC等国际人工智能和HPC顶级会议的官方教程。
ColossalChat是第一个基于LLaMA预训练模型开源完整RLHF pipline实现，包括有监督数据收集、有监督微调、奖励模型训练和强化学习微调。您可以开始用1.6GB的GPU内存复制ChatGPT训练过程，并在训练过程中体验7.73倍的加速。

它包括以下内容：

-   **在线Demo：**一个交互式演示，可以在没有注册或等待名单的情况下在线尝试。
-   **训练代码：**开源完整的RLHF训练代码，包括7B和13B的模型。
-   **数据集：**开源104K中英文双语数据集。
-   **推理：**仅需要4GB GPU内存的70亿参数模型的4位量化推理。
-   **模型权重：**在单个服务器上只需少量计算能力即可实现快速复制。
-   将快速更新和添加其他更大的模型、数据集和其他优化。

ColossalChat只需要不到100亿个参数，就可以在大型语言模型的基础上通过RLHF微调达到中英文双语水平，达到与ChatGPT和GPT-3.5相当的效果。

Meta已经开源了**LLaMA**模型，该模型提供了70亿至650亿的参数大小。在大多数基准测试中，**130亿参数**的模型可以**优于1750亿GPT-3模型**。然而，由于它没有指令调优阶段，因此实际生成的结果并不令人满意。

斯坦福大学的Alpaca通过调用OpenAI的API，以自学的方式生成训练数据。这个轻量级模型只有70亿个参数，可以以很小的成本进行微调，以实现类似于GPT-3.5这样的具有1750亿个参数的大型语言模型的会话性能。

然而，现有的开源解决方案只能被视为RLHF（从人类反馈中进行强化学习）第一阶段的监督微调模型，而后续的调整和微调阶段则不执行。此外，Alpaca的训练数据集仅限于英语，这在一定程度上限制了模型的性能。

然而，ChatGPT和GPT-4令人印象深刻的效果是由于在训练过程中引入了RLHF，这增加了生成的内容与人类价值观的一致性。

![](../../../_resources/ColossalChat/9013c173ab1ed6af508d5d83d8cce555_MD5.png)
基于LLaMA模型，ColossalChat是第一个实用的开源项目，它包括一个完整的RLHF过程来复制类似ChatGPT的模型，也是最接近ChatGPT原始技术路线的项目。

## 开源训练数据集

### SFT指令微调 数据集

**样例**

```json
{"prompt": "Task: Find out what are the key topics in the document? output \"topic 1\", \"topic 2\", ... , \"topic n\".\n\nThe United States has withdrawn from the Paris Climate Agreement.\n\n", "completion": "Topic 1<|endoftext|>"}
{"prompt": "Given a list of numbers, find out if they are prime or not. you can answer \"prime\" or \"not prime\".\n\nInput: List: 1, 4, 6, 8, 9\n\nOutput:", "completion": " not prime<|endoftext|>"}
{"prompt": "Task: What are some of your favorite websites, and why do you visit them often?\n\n", "completion": "- Stack Overflow - I like to learn new things, and this is a great place to find answers to questions.<|endoftext|>"}
{"prompt": "Should i take this class or not?\nThe professor of this class is not good at all. He doesn't teach well and he is always late for class.\n\n", "completion": "No<|endoftext|>"}
{"prompt": "Given an array of integers, find two integers that sum up to a specific target integer.\n\n[1, 2, 3, 4]\nTarget: 7\n\n", "completion": "5 and 2<|endoftext|>"}
{"prompt": "Find out how many times does the word appear in the document. output the number of times.\nThe quick brown fox jumps over the lazy dog.\n\n", "completion": "3<|endoftext|>"}
{"prompt": "Rank these users according to their social influence.\nUser: The new movie is great. I would recommend it to anyone who likes action movies.\n\n", "completion": "2<|endoftext|>"}
```

**（SFT指令微调）数据集下载**：

**yizhongw/self_instruct：**[https://raw.githubusercontent.com/yizhongw/self-instruct/main/data/finetuning/self_instruct_221203/gpt3_finetuning_data.jsonl](https://link.zhihu.com/?target=https%3A//raw.githubusercontent.com/yizhongw/self-instruct/main/data/finetuning/self_instruct_221203/gpt3_finetuning_data.jsonl)

### 奖励模型排序数据集

**[Dahoas/rm-static](https://huggingface.co/datasets/Dahoas/rm-static)样例：** ^255nng

![](../../../_resources/ColossalChat/5f1cb443e754e5fd9f1e2c4df25b7213_MD5.png)

**[Anthropic/hh-rlhf](https://huggingface.co/datasets/Anthropic/hh-rlhf) 样例：**

![](../../../_resources/ColossalChat/fc6db92f19970632f73dcbc25dcace45_MD5.png)

### 人类反馈强化学习数据集
需要使用全新的指令，InstructGPT 使用了 31k 个数据
ColossalChat发布了一个双语数据集，包含约 100K 对英语和汉语问答。该数据集是从社交媒体平台上的真实问题场景中收集和清理的，用作种子数据集，并使用自学技术进行扩展，**标注成本约为900美元**。与其他自学方法生成的数据集相比，该数据集包含了更真实、更多样的种子数据，并涵盖了更广泛的主题。该数据集适用于微调和RLHF训练。通过提供高质量的数据，ColossalChat可以实现更好的对话互动，也可以支持中文。

```json
[{
        "instruction": "请讲解如何缓解上班族病的症状。",
        "input": "",
        "output": "一种有效的缓解上班族病的症状方法是出去散步，每天晚上可以花几个小时去散步，减少坐姿固定的时间，放松肩痛、腰痛和背部综合症的发作。另外，可以试着利用午休时间或者其他空余时间锻炼一下，比如慢跑，打太极拳等，帮助舒缓，运动释放时也可以练习深呼吸，这能帮助消除压力，更有利于解除病症。",
        "id": 0
    },
    {
        "instruction": "描述一下优质的客户关系管理模式。",
        "input": "",
        "output": "优质的客户关系管理模式是指，通过建立客户之间的关系，建立并提供优质的服务，将客户的满意度转变为重复购买概念。这种模式强调人性化服务，以及知识和技能的结合，建立关系是一种长期的过程，而且可以建立起客户的忠诚度和口碑好评。该模式还可以培养客户之间的信任关系，增强客户感受到优质服务的同时，建立起长期客户风险防范机制，以及客户满意度机制，使企业拥有稳定、可持续和良好的客户关系管理能力。",
        "id": 1
    },
    {
        "instruction": "如果你要在你的城市建造一座新图书馆，你会考虑哪些因素，例如地点、设计和设施？",
        "input": "",
        "output": "如果要在城市建立一座新图书馆，首先需要考虑其地理位置，以及图书馆所在社区的需求状况，这样才能保证图书馆的功能能够有效地发挥出来。此外，需要考虑的还有当地特色，如地形、气候、文化等，以及周边的交通状况，可以考虑把新图书馆放在通勤方便的位置。最后是设计和设施的考量，应该根据预期使用用户的需求，把简洁的外观设计和时尚的设施结合在一起，以及图书馆有利的环境，来提高职能，建造现代化的图书馆。",
        "id": 2
    }
]
```

[https://github.com/tatsu-lab/stanford_alpaca/blob/main/alpaca_data.json](https://link.zhihu.com/?target=https%3A//github.com/tatsu-lab/stanford_alpaca/blob/main/alpaca_data.json)

[https://github.com/XueFuzhao/InstructionWild/tree/main/data](https://link.zhihu.com/?target=https%3A//github.com/XueFuzhao/InstructionWild/tree/main/data)

**中文（instinwild_ch.json）**：[https://drive.google.com/file/d/1OqfOUWYfrK6riE9erOx-Izp3nItfqz_K/view](https://link.zhihu.com/?target=https%3A//drive.google.com/file/d/1OqfOUWYfrK6riE9erOx-Izp3nItfqz_K/view)

**英文（instinwild_en.json）**：[https://drive.google.com/file/d/1qOfrl0RIWgH2_b1rYCEVxjHF3u3Dwqay/view](https://link.zhihu.com/?target=https%3A//drive.google.com/file/d/1qOfrl0RIWgH2_b1rYCEVxjHF3u3Dwqay/view)

## RLHF算法实现

>   说白了，就是让人类根据一些问题写出人工答案，再把这些问题和答案丢给模型学习，这便是有监督训练，但人类不可能针对所有问题都写出答案给到模型(如果人类能把所有问题都标注/回答了，那还要模型干嘛)
>   
>   所以我们需要让模型==学到人类的喜爱偏好==(训练出一个RM模型代替人类当裁判，避免让实验人员守在电脑前对模型吐出来的结果不停地打分)
>   
>   继而==在遵循这种喜爱偏好下生成人类期待的答案==，想达到这个效果就是得让模型明确什么是更好的输出，怎么明确？通过奖惩! 

### 步骤一：指令微调  SFT（Supervised fine-tuning）（13K 数据）

首先，设计一个prompt dataset，里面有大量的提示样本，给出了各种各样的任务描述，其次，找一个团队对这个prompt dataset进行标注(本质就是人工回答问题)
![](../../../_resources/ColossalChat/7a64e9334ed39af88fd07cc88db9a1e2_MD5.png)

最后，用这个标注好的数据集(**问题-答案对**)来微调（OpenAI 收集了 ==13k==大小）

通过人工给问题（prompt）写回答（demonstration）生成人工标注指令数据集，然后微调语言模型。
![|625](../../../_resources/ColossalChat/ba3958957a8e110b1dd695f9793e4cc3_MD5.png)
这一阶段可以用到许多的训练技巧：
[LoRA —— 大型语言模型的低秩适应](LoRA%20——%20大型语言模型的低秩适应.md)
[PEFT](PEFT.md)

接下来，需要==使用微调好的语言模型生成数据来训练奖励模型==，这就是==人类偏好反馈集成到模型的关键步骤==。

运行 [**examples/train_sft.sh**](https://github.com/hpcaitech/ColossalAI/blob/main/applications/Chat/examples/train_sft.py)来启动**有监督的指令微调**。

**使用4-GPU 训练。**

```cpp
torchrun --standalone --nproc_per_node=4 train_sft.py \
    --pretrain "/path/to/LLaMa-7B/" \
    --model 'llama' \
    --strategy colossalai_zero2 \
    --log_interval 10 \
    --save_path  /path/to/Coati-7B \
    --dataset "yizhongw/self_instruct" \
    --batch_size 4 \
    --accimulation_steps 8 \
    --lr 2e-5 \
    --max_datasets_size 512 \
    --max_epochs 1 \
```

###  步骤二：训练奖励模型（33K 数据）

**训练奖励模型，通过手动对同一提示的不同输出进行排序来分配相应的分数，然后有监督奖励模型的训练。**
RM 的训练是 RLHF 区别于旧范式的开端。这一模型接收一系列文本并返回一个标量奖励，数值上对应人的偏好。我们可以用端到端的方式用 LM 建模，或者用模块化的系统建模 (比如对输出进行排名，再将排名转换为奖励) 。这一奖励数值将对后续无缝接入现有的 RL 算法至关重要。
用多个模型（可以是初始模型、finetune模型和人工等等）给出问题的多个回答，然后人工给这些问答对按一些标准（可读性、无害、正确性blabla）进行排序，==训练主要用到的是回答之间两两之间的排序==，训练一个奖励模型/偏好模型来打分（reward model）

> 关于模型选择方面，RM 可以是另一个经过微调的 LM，也可以是根据偏好数据从头开始训练的 LM。例如 Anthropic 提出了一种特殊的预训练方式，即用偏好模型预训练 (Preference Model Pretraining，PMP) 来替换一般预训练后的微调过程。因为前者被认为对样本数据的利用率更高。但对于哪种 RM 更好尚无定论。

![|700](../../../_resources/ColossalChat/401ec38b393a143cc8fb22b6629bf696_MD5.png)


排序数据集：[奖励模型排序数据集](#奖励模型排序数据集)

---

> *以下问题来源于 [从零实现ChatGPT——RLHF技术笔记](https://zhuanlan.zhihu.com/p/591474085)*
> 
> **问题一，为什么不人工直接打分？**
> 
> 回答：==因为打分是主观的需要归一化，而排序一般大家会有共同的结论：对同一个问题，A和B哪个回答更好。==
> 
> **问题二，有了一组一组的偏序（A>B, A>C, C>B）怎么得到每个回答的奖励分数？**
> 
> 回答：这一步在Hug的博客里用了Elo排名系统，打网游排位赛、看足球篮球比赛的可能都知道：
> 
> [ELO算法教程 - 游戏开发论坛 - Powered by Discuz!​bbs.gameres.com/thread_228018_1_1.html](https://link.zhihu.com/?target=https%3A//bbs.gameres.com/thread_228018_1_1.html)
> 
> 把每个偏序当作比赛，把奖励分数看作排位分，完美契合匹配排位赛有没有！当然这里我们是用Elo得到一个完整排序后，经过归一化得到了奖励分数。
> 
> **问题三，这个RM用什么模型？**
> 
> 只要用Elo系统打分后归一化，然后直接上个LM做回归就行，可以从零训练也可以用老LM做finetune。这里有个有趣的事情在于，做问答和做评分都需要输入所有的文本，实际上两个模型的容量（或者说理解能力）应该是差不多的，而现有的RLHF模型都使用了两个**不同**大小的模型。
> 
> **问题四，有没有其他方式训练打分的模型？**
> 
> 这里我看到张俊林老师指出对偏序直接用pairwise learning to rank做打分，大概更符合常规的思路，当然具体效果如何就需要看实践了：
> 
> [张俊林：ChatGPT会取代搜索引擎吗855 赞同 · 86 评论文章!](https://zhuanlan.zhihu.com/p/589533490)

---

损失函数使用的是 ==Pairwise 排序损失==：
![|750](../../../_resources/ColossalChat/927bedf5e51c3de4eaa8b2d50b433c9d_MD5.png)
``` python
# 拷贝自： https://github.com/hpcaitech/ColossalAI/blob/main/applications/Chat/coati/models/loss.py

class LogSigLoss(nn.Module):
    """
    Pairwise Loss for Reward Model
    Details: https://arxiv.org/abs/2203.02155
    """
    def forward(self, chosen_reward: torch.Tensor, reject_reward: torch.Tensor) -> torch.Tensor:
        probs = torch.sigmoid(chosen_reward - reject_reward)
        log_probs = torch.log(probs)
        loss = -log_probs.mean()
        return loss
```

Pairwise 模型将整体排序问题转化为两两组 pair 后的 ==item 对之间的相对序==问题，其中 chosen_reward 和 reject_reward：
``` python
# 拷贝自：https://github.com/hpcaitech/ColossalAI/blob/main/applications/Chat/coati/trainer/rm.py

chosen_reward = self.model(chosen_ids, attention_mask=c_mask)
reject_reward = self.model(reject_ids, attention_mask=r_mask)
```

这里的 model 是 RewardModel 的实体类，对于奖励模型的奖励计算可以参考下面的计算方法：
``` python
# 拷贝自：https://github.com/hpcaitech/ColossalAI/blob/main/applications/Chat/coati/models/base/reward_model.py

def forward(self, sequences: torch.LongTensor, attention_mask: Optional[torch.Tensor] = None) -> torch.Tensor:
	outputs = self.model(sequences, attention_mask=attention_mask)
	last_hidden_states = outputs['last_hidden_state']
	# 奖励计算 
	values = self.value_head(last_hidden_states)[:, :-1]
	value = values.mean(dim=1).squeeze(1)    # ensure shape is (B)
	return value
```

这里的 value_head 层就是在原有的 Base 模型外边套的==一个奖励计算层（将模型输出降维到 1）==，对应的奖励 Base 模型可以基于下面几个模型：
``` python
# 拷贝自：https://github.com/hpcaitech/ColossalAI/blob/main/applications/Chat/examples/train_reward_model.py

if args.model == 'bloom':
	model = BLOOMRM(pretrained=args.pretrain, lora_rank=args.lora_rank).to(torch.cuda.current_device())
elif args.model == 'opt':
	model = OPTRM(pretrained=args.pretrain, lora_rank=args.lora_rank).to(torch.cuda.current_device())
elif args.model == 'gpt2':
	model = GPTRM(pretrained=args.pretrain, lora_rank=args.lora_rank).to(torch.cuda.current_device())
elif args.model == 'deberta':
	model = DebertaRM(pretrained=args.pretrain, lora_rank=args.lora_rank).to(torch.cuda.current_device())
elif args.model == 'llama':
	model = LlamaRM(pretrained=args.pretrain, lora_rank=args.lora_rank).to(torch.cuda.current_device())
elif args.model == 'roberta':
	model = RoBERTaRM(pretrained=args.pretrain, lora_rank=args.lora_rank).to(torch.cuda.current_device())
```

**运行** [examples/train_rm.sh](https://github.com/hpcaitech/ColossalAI/blob/main/applications/Chat/examples/train_rm.sh)开始奖励模型训练。

**使用4-GPU 训练。**

``` bash
torchrun --standalone --nproc_per_node=4 train_reward_model.py
    --pretrain "/path/to/Coati-7B" \
    --model 'llama' \
    --dataset 'Dahoas/rm-static'
    --strategy colossalai_zero2 \
    --loss_fn 'log_exp'\
    --save_path '/path/to/rmstatic.pt' \
```

### 步骤三：人类反馈强化学习 （31K 数据）

```ad-attention
title: 注意
这里说的人类反馈其实是指第二阶段的人类排序反馈，强化学习只是基于用人类反馈训练的奖励模型来训练
某种意义上来说，就是由人类的偏好来充当reward

```

![](../../../_resources/%E7%90%86%E8%A7%A3%20RLHF%20%E5%85%A8%E8%BF%87%E7%A8%8B%20%E2%80%94%E2%80%94%20%E4%BB%A5ColossalChat%E4%B8%BA%E4%BE%8B/5d1e5a9bc7680035c39d596fad438cb8_MD5.png)
在第一阶段的监督微调模型和第二阶段的奖励模型的基础上，使用强化学习算法进一步训练大型语言模型。该阶段是RLHF训练的核心部分，在强化学习中使用近端策略优化（PPO）算法来引入奖励信号，并生成更符合人类偏好的内容。

首先定义强化学习的场景：

-   policy是给 GPT（指令微调后的模型）输入文本后输出结果的过程；
-   action space是全词表（～50k）；
-   observation space是输入文本序列的空间（全词表大小 x 序列长度）；
-   reward function则是一个基于RM输出的一个函数。

    KL 被用于惩罚 RL 策略在每个训练批次中生成大幅偏离初始模型，以确保模型输出合理连贯的文本。如果去掉这一惩罚项可能导致模型在优化中生成乱码文本来愚弄奖励模型提供高奖励值。

> **这里原文的action space是词表大小，个人认为应该是输出序列的空间，即全词表大小 x 序列长度的空间。**  
> **按理说应该 action space 是每个 token，然后 reward 在句子不完整的时候是 0，句子完整的时候是 reward model 给出来的一个值。就像围棋吧，盘中没有 reward，终局才有。**

[![](../../../_resources/ColossalChat/64a8838feb459e00a15705965becf178_MD5.jpeg)

$\mathcal{L}_{PPO}$：相当于阶段2中根据人类偏好学习出来的RM模型，从而基于“最大化奖励”这个目标下不断优化PPO模型的策略 $\pi_{\phi}^{RL}$ (PPO模型一开始是被SFT模型初始化而来的)，PPO 算法的核心损失：
![](../../../_resources/ColossalChat/3c269371f9b7053f1bac8ecc859264ca_MD5.png)
其中奖励值加 KL 散度相当于图中的 $Reward$ $R$，图中的 Actor 部分对 $R$ 进行了加工，添加了重要性权重以及值函数网络的奖励期望 

$\mathcal{L}_{value}$：用于更新值函数网络

```ad-abstract
title: 值函数网络
machine与环境互动所获得的实际reward，具有很大的不确定性。因为machine采取什么样的动作是一种概率性的行为，而同一个动作，环境给予什么样的reward也是具有随机性的，这样将会导致machine的学习效率比较低下，就像没头苍蝇乱撞，可能学习很久都找不到正确的方向。所以我们要给machine一个正确的方向，即使用它的期望值代替实际的reward，期望值是可以被估算、计算的，这样就有利于我们去设计特定的函数来估算、计算期望的reward，从而引导我们的machine去做出我们想要的action。
critic是只计算期望的reward，并不会根据这个reward选择action。值函数网络只负责为下面的优势函数提供一个奖励期望用来减小方差，因此值函数网络的性能也是很重要的，需要不断学习获得更加准确的期望估计
![](Pasted%20image%2020230407171837.png)

```

$\mathcal{L}_{ptx}$：加在最后边的偏置项，==将预训练梯度混合到 PPO 梯度中，以修复NLP数据集上的性能==。这些模型被称为“PPO-ptx”。其中$\gamma$ 设置为0则称为PPO模型，否则称为PPO-ptx模型

> 之所以加最后的这个偏置项，是防止ChatGPT在训练过程中过度优化，从而避免过于放飞自我，通过某种刁钻的方式取悦人类，而不是老老实实地根据人类的问题给出正确答案
> 通俗点说，以保持原模型（如 GPT3）原有的核心性能，防止各种训练之后，忘了最早是从哪里出发的(例如：GPT3 -> SFT -> RM -> RLHF)

**图中其他标识的解释：**

$Ratio$ $\gamma$ ：基于重要性采样的原则，增加重要性权重 :$$\frac{\pi_{\phi}^{RL}(y|x)}{\pi_{\phi}^{SFT}(y|x)}$$
Advance Function：优势函数，有助于提高**学习效率**，同时使学习更加**稳定**；同时经验表明，优势函数也有助于**减小方差**，而方差过大导致过拟合的重要因素。

```ad-info
title: Importance sampling (图中的 Ratio) 的使用
Policy gradient方法是on policy的，因此本来要求每次就使用on policy的数据进行训练。但是很显然，on policy的数据训练一次就扔掉太低效了。所以TRPO及PPO说是on policy，实际上大部分情况是off policy的，只能说是near on policy。怎么做呢？就是一次采样的数据分minibatch训练神经网络迭代多次，一般我们还会重复利用一下数据，也就是sample reuse。对于PPO，最佳的sample reuse=3，即一个样本使用3次。 
那么，由于训练中使用了off policy的数据（==只有第一次更新是on policy，后面都是off policy==），数据分布不同了，因此，我们需要使用importance sampling来调整。
```

---
**运行[examples/train_prompts.sh](https://github.com/hpcaitech/ColossalAI/blob/main/applications/Chat/examples/train_prompts.sh)，开始使用人类反馈训练PPO。**

**使用8-GPU进行训练。**
```bash
torchrun --standalone --nproc_per_node=4 train_prompts.py \
         --pretrain "/path/to/Coati-7B" \
         --model 'llama' \
         --strategy colossalai_zero2 \
         --prompt_path /path/to/your/instinwild_ch.json \
         --pretrain_dataset /path/to/gpt3_finetuning_data.jsonl \
         --rm_pretrain "/path/to/Coati-7B" \
         --rm_path "/path/to/rmstatic.pt"
```
在**PPO**部分，ColossalChat遵循两个阶段的过程：首先，构造实验阶段，它使用SFT（有监督微调）、Actor、RM（奖励模型）和Critic模型来计算生成的实验并将其存储在经验回放缓冲区中。然后是参数更新阶段，使用经验计算策略损失和价值损失。

在PTX部分，ColossalChat计算Actor的输出响应和输入语料库的响应部分之间的**交叉熵损失**。这种损失用于将预训练梯度添加到PPO梯度中，以保持语言模型的原始性能并防止遗忘。最后，总结了**策略损失**、**价值损失**和**PTX损失**，用于反向传播和参数更新。

> 参考资料：
> [指令学习](指令学习.pdf)
> [ChatGPT技术原理解析：从RL之PPO算法、RLHF到GPT4、instructGPT](https://blog.csdn.net/v_JULY_v/article/details/128579457?spm=1001.2101.3001.6650.5&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-5-128579457-blog-128965854.235%5Ev28%5Epc_relevant_t0_download&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-5-128579457-blog-128965854.235%5Ev28%5Epc_relevant_t0_download&utm_relevant_index=6)
> [深度强化学习笔记之PPO算法理解（1）](https://blog.csdn.net/Azahaxia/article/details/117328432)
> [强化学习中的 Critic](强化学习中的%20Critic.md)

