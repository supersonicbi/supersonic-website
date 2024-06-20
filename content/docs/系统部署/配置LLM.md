+++
title = "配置LLM"
weight = 3
+++

# 配置LLM

## Text2SQL模型

SuperSonic可以从两个粒度配置LLM：

- 系统粒度：修改配置文件`conf/supersonic-env.sh`，替换相应的变量

<img src="../../assets/supersonic_deploy_llm.png" align="center"/> 


- 助理粒度：在助理管理模块，修改助理配置，填入相应的变量

<img src="../../assets/supersonic_quickstart_chat.png" align="center"/> 

## Embedding模型
SuperSonic有三种方式配置Embedding模型（0.9.2版本及之前）：

- in_process：默认采用内嵌的BgeSmallZhEmbeddingModel模型；可支持配置本地模型（需符合onnx格式）

- open_ai：采用open_ai提供的Embedding模型

- hugging_face：采用hugging_face提供的Embedding模型

<img src="../../assets/supersonic_embedding_model.png" align="center"/> 
