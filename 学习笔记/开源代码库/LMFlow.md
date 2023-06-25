
``` bash
git clone https://github.com/OptimalScale/LMFlow.git
cd LMFlow
conda create -n lmflow python=3.9 -y
conda activate lmflow
conda install mpi4py
```

修改 .requirements.txt，注释其中几行
``` txt
numpy==1.24.2
datasets==2.10.1
# peft @ git+https://github.com/huggingface/peft.git@deff03f2c251534fffd2511fc2d440e84cc54b1b
torch==2.0.0
wandb==0.14.0
deepspeed==0.8.3
# trl @ git+https://github.com/lvwerra/trl.git#egg=trl-0.4.1
sentencepiece
# transformers @ git+https://github.com/huggingface/transformers@c612628045822f909020f7eb6784c79700813eda
flask
flask_cors
```
然后手动安装 PEFT：

``` bash
git clone https://github.com/huggingface/peft.git
cd peft/
git checkout e536616
pip install -e .
cd -
```
手动安装 trl：

``` bash
git clone https://github.com/lvwerra/trl.git
cd trl/
pip install -e .
cd -
```

最后安装依赖

``` bash
pip install -e .
```

下载数据集：

``` bash
cd data
bash download.sh all
cd -
```

申请 wandb API key：

```
wandb init
```

然后打开弹出的网址：

![](../../../_resources/LMFlow/a28bd9b63dede2659413b42ab5f9c4e9_MD5.png)

 打开后复制key

![](../../../_resources/LMFlow/442b6bcbf5f3f6d931c4af100f2a9cec_MD5.png)

运行微调：

``` bash
./scripts/run_finetune.sh
```

## 运行截图

![](../../../_resources/LMFlow/bb773ff659e0607d9e3d7739a8caa0dc_MD5.png)




