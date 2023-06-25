

![](ChatGLM-6B.pptx)



![|500](a4ca36b08af58f60c2febf95c6deedd0_MD5.png)

## 克隆仓库

```
git clone https://github.com/THUDM/ChatGLM-6B.git
```

## 安装环境依赖

```ad-attention
title: 注意
`transformers` 库版本推荐为 `4.27.1`，但理论上不低于 `4.23.1` 即可。

```

```
pip install -r requirements.txt
```

## 调用方式

### 代码调用

``` python
>>> from transformers import AutoTokenizer, AutoModel
>>> tokenizer = AutoTokenizer.from_pretrained("THUDM/chatglm-6b", trust_remote_code=True)
>>> model = AutoModel.from_pretrained("THUDM/chatglm-6b", trust_remote_code=True).half().cuda()
>>> model = model.eval()
>>> response, history = model.chat(tokenizer, "你好", history=[])
>>> print(response)
你好!我是人工智能助手 ChatGLM-6B,很高兴见到你,欢迎问我任何问题。
>>> response, history = model.chat(tokenizer, "晚上睡不着应该怎么办", history=history)
>>> print(response)

晚上睡不着可能会让你感到焦虑或不舒服,但以下是一些可以帮助你入睡的方法:

1. 制定规律的睡眠时间表:保持规律的睡眠时间表可以帮助你建立健康的睡眠习惯,使你更容易入睡。尽量在每天的相同时间上床,并在同一时间起床。
2. 创造一个舒适的睡眠环境:确保睡眠环境舒适,安静,黑暗且温度适宜。可以使用舒适的床上用品,并保持房间通风。
3. 放松身心:在睡前做些放松的活动,例如泡个热水澡,听些轻柔的音乐,阅读一些有趣的书籍等,有助于缓解紧张和焦虑,使你更容易入睡。
4. 避免饮用含有咖啡因的饮料:咖啡因是一种刺激性物质,会影响你的睡眠质量。尽量避免在睡前饮用含有咖啡因的饮料,例如咖啡,茶和可乐。
5. 避免在床上做与睡眠无关的事情:在床上做些与睡眠无关的事情,例如看电影,玩游戏或工作等,可能会干扰你的睡眠。
6. 尝试呼吸技巧:深呼吸是一种放松技巧,可以帮助你缓解紧张和焦虑,使你更容易入睡。试着慢慢吸气,保持几秒钟,然后缓慢呼气。

如果这些方法无法帮助你入睡,你可以考虑咨询医生或睡眠专家,寻求进一步的建议。
```

### 网页服务

网页服务基于 Gradio，因此需要先安装 `pip install gradio`

然后就可以启动网页服务

```
python web_demo.py
```
[![web-demo](f3b0907c6291ecdd360261384c68c616_MD5.gif)](https://github.com/THUDM/ChatGLM-6B/blob/main/resources/web-demo.gif)

### 命令行调用


``` bash
python cli_demo.py
```

程序会在命令行中进行交互式的对话，在命令行中输入指示并回车即可生成回复，输入 `clear` 可以清空对话历史，输入 `stop` 终止程序。
[![cli-demo](https://github.com/THUDM/ChatGLM-6B/raw/main/resources/cli-demo.png)](https://github.com/THUDM/ChatGLM-6B/blob/main/resources/cli-demo.png)


### API 调用

首先需要安装额外的依赖 `pip install fastapi uvicorn`，然后运行仓库中的 [api.py](https://github.com/THUDM/ChatGLM-6B/blob/main/api.py)：

```
python api.py
```

默认部署在本地的 8000 端口，通过 POST 方法进行调用

``` bash
curl -X POST "http://127.0.0.1:8000" \
     -H 'Content-Type: application/json' \
     -d '{"prompt": "你好", "history": []}'
```

得到的返回值为

``` json
{
  "response":"你好👋！我是人工智能助手 ChatGLM-6B，很高兴见到你，欢迎问我任何问题。",
  "history":[["你好","你好👋！我是人工智能助手 ChatGLM-6B，很高兴见到你，欢迎问我任何问题。"]],
  "status":200,
  "time":"2023-03-23 21:38:40"
}
```


## 模型量化

默认情况下，模型以 FP16 精度加载，运行上述代码需要==大概 13GB 显存==。如果你的 GPU 显存有限，可以尝试以量化方式加载模型，使用方法如下：

```ad-danger
title: 注意
按需修改，目前只支持 4/8 bit 量化

```

``` python
model = AutoModel.from_pretrained("THUDM/chatglm-6b", trust_remote_code=True).quantize(4).half().cuda()
```

进行 2 至 3 轮对话后，==8-bit 量化下 GPU 显存占用约为 10GB，4-bit 量化下仅需 6GB 占用==。随着对话轮数的增多，对应消耗显存也随之增长，由于采用了相对位置编码，理论上 ChatGLM-6B 支持无限长的 context-length，但总长度超过 2048（训练长度）后性能会逐渐下降。
量化过程需要在内存中首先加载 FP16 格式的模型，消耗大概 13GB 的内存。如果你的内存不足的话，可以直接加载量化后的模型，仅需大概 5.2GB 的内存：

``` python
model = AutoModel.from_pretrained("THUDM/chatglm-6b-int4", trust_remote_code=True).half().cuda()
```

进一步提供了对Embedding量化后的模型，模型参数==仅占用4.3 GB==显存：

``` python
model = AutoModel.from_pretrained("THUDM/chatglm-6b-int4-qe", trust_remote_code=True).half().cuda()
```

## CPU 支持

如果你没有 GPU 硬件的话，也可以在 CPU 上进行推理，但是推理速度会更慢。使用方法如下（需要大概 ==32GB 内存==）

``` python
model = AutoModel.from_pretrained("THUDM/chatglm-6b", trust_remote_code=True).float()
```

如果你的内存不足，可以直接加载量化后的模型：

``` python
model = AutoModel.from_pretrained("THUDM/chatglm-6b-int4",trust_remote_code=True).float()
```

如果遇到了报错 `Could not find module 'nvcuda.dll'` 或者 `RuntimeError: Unknown platform: darwin`(MacOS) 的话请参考这个[Issue](https://github.com/THUDM/ChatGLM-6B/issues/6#issuecomment-1470060041).

## Apple Silicon 支持

对于搭载了Apple Silicon的Mac（以及MacBook），可以使用 MPS 后端来在 GPU 上运行 ChatGLM-6B。首先需要参考 Apple 的 [官方说明](https://developer.apple.com/metal/pytorch) 安装 PyTorch-Nightly。使用 mps 后端

``` python
model = AutoModel.from_pretrained("your local path", trust_remote_code=True).half().to('mps')
```

即可使用在 Mac 上使用 GPU 加速模型推理。



