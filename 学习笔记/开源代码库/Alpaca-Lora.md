## 克隆仓库

`git clone git@github.com:tloen/alpaca-lora.git`

## 安装依赖

`pip install -r requirements.txt`

## 运行微调程序

``` bash
python finetune.py \
    --base_model 'decapoda-research/llama-7b-hf' \
    --data_path 'yahma/alpaca-cleaned' \
    --output_dir './lora-alpaca'
```

## 运行截图

### 7B 微调
![](../../../_resources/Alpaca-Lora/26b2e322bf10b83b5389366da8088236_MD5.png)

### 30B 微调
![](../../../_resources/Alpaca-Lora/412fb3a553a79d98ced6aab12e9b89e6_MD5.png)

占用大概 40G 显存
![](../../../_resources/Alpaca-Lora/d6294dc3b9950c177d2f08b6c6cfa649_MD5.png)

### 65B 模型下载

![](../../../_resources/Alpaca-Lora/a99388d05155189be1ee52a75a3ed707_MD5.png)



