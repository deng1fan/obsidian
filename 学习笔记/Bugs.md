## LLaMA 生成无法停止，直到生成到最大长度才停止

很有可能是因为 LLaMA 的 tokenizer 的问题，tokenizer 的 eos_token 为 ""，bos_token 也为 ""，因此通过结束符判断结束似乎是无法实现的

```ad-note
title: 猜测
之前的 GPT 生成问题会不会也是因为这个问题？

```


## LLaMA 的 Tokenizer 设置问题
https://github.com/huggingface/transformers/commit/c0f99b4d2ec73090595914dde4c16da207e21d73#diff-800a68920b5f9ba9260c83f0cc9dc57c20aa51a9a917b49c82667e1a92eebf23