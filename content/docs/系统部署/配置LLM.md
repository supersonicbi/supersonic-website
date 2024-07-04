+++
title = "配置LLM"
weight = 3
+++

# 配置LLM

## Chat Model

SuperSonic可以从两个粒度配置Chat Model：

### **1. 系统粒度**
#### **1.2.修改langchain4j.yaml配置文件方式**

从0.9.4版本开始，langchain4j配置从application.yaml文件中单独抽取，方便用户配置；以langchain4j-local.yaml为例配置：

{{< figure src=/img/supersonic_langchain4j_config.png#center >}}
目前支持：open-ai、ollama两种方式；
1、open_ai 用于连接云端模型；通常情况下各云上模型会兼容open-ai协议
2、ollama 用于连接本地模型；由ollama适配不同的模型

{{< hint info >}}
**注意**
推荐使用open_ai、ollama；其他azure、qianfan、dashscope、zhipu方式理论上也支持，但是待验证；
{{< /hint >}}

open-ai 配置方式：
```
langchain4j:
    open-ai:
        chat-model:
            base-url: ${OPENAI_API_BASE:demo}
            api-key: ${OPENAI_API_KEY:demo}
            model-name: ${OPENAI_MODEL_NAME:gpt-3.5-turbo}
            temperature: ${OPENAI_TEMPERATURE:0.0}
            timeout: ${OPENAI_TIMEOUT:PT60S}
```
ollama 配置方式：
```
langchain4j:
    ollama:
        chat-model:
            base-url: ${OPENAI_API_BASE:demo}
            api-key: ${OPENAI_API_KEY:demo}
            model-name: ${OPENAI_MODEL_NAME:gpt-3.5-turbo}
            temperature: ${OPENAI_TEMPERATURE:0.0}
            timeout: ${OPENAI_TIMEOUT:PT60S}
```
{{< hint info >}}
**注意**
以下方式配置，待验证：
{{< /hint >}}
zhipu 配置方式：
```
langchain4j:
    zhipu:
        chat-model:
            base-url: base-url
            api-key: demo
            model-name: xxx
            temperature: 0.0
            timeout: PT60S
```
azure 配置方式：
```
langchain4j:
    azure:
        chat-model:
            endpoint: endpoint
            api-key: demo
            deployment-name: xxx
            max-tokens: 20
```
qianfan 配置方式：
```
langchain4j:
    qianfan:
        chat-model:
            endpoint: endpoint
            api-key: demo
            deployment-name: xxx
            temperature: 0.0
            timeout: PT60S
```
dashscope 配置方式：
```
langchain4j:
    dashscope:
        chat-model:
            endpoint: endpoint
            api-key: demo
            deployment-name: xxx
            temperature: 0.0
            timeout: PT60S
```

### **2. 助理粒度**
在助理管理模块，修改助理配置，填入相应的变量:
open-ai 配置方式：

{{< figure src=/img/supersonic_agent_llm_1.png#center >}}

ollama 配置方式：


{{< figure src=/img/supersonic_agent_llm_2.png#center >}}


## Embedding Model

统一采用一种方式配置Embedding模型，支持in-memory、open-ai、zhipu、ollama、azure、qianfan、dashscope

{{< figure src=/img/supersonic_embedding_model_new.png#center >}}

支持in-memory 配置方式：
目前支持bge-small-zh、all-minilm-l6-v2-q内嵌模型；并支持符合onnx格式的本地模型；

```
langchain4j:
    in-memory:
        embedding-model:
            model-name: bge-small-zh
            modelPath: /data/model.onnx
            vocabularyPath: /data/onnx_vocab.txt
```
{{< hint info >}}
**注意**
如果是启动报错，version `GLIBC_2.27' not found (required by xxxlibonnxruntime.so)，如下图所示：
原因是本地环境缺少对应库文件可尝试切换open-ai、dashscope等提供的embedding-model
{{< /hint >}}

{{< figure src=/img/supersonic_inmemory_error.jpg#center >}}

open-ai 配置方式：
```
langchain4j:
    open-ai:
        embedding-model:
            base-url: ${OPENAI_API_BASE:demo}
            api-key: ${OPENAI_API_KEY:demo}
            model-name: xxx
            timeout: ${OPENAI_TIMEOUT:PT60S}
```
zhipu 配置方式：
```
langchain4j:
    zhipu:
        embedding-model:
            base-url: ${OPENAI_API_BASE:demo}
            api-key: ${OPENAI_API_KEY:demo}
            model: xxx
```
ollama 配置方式：
```
langchain4j:
    ollama:
        embedding-model:
            base-url: ${OPENAI_API_BASE:demo}
            model-name: xxx
            timeout: ${OPENAI_TIMEOUT:PT60S}
```
azure 配置方式：
```
langchain4j:
    azure:
        embedding-model:
            endpoint: ${OPENAI_API_BASE:demo}
            api-key: ${OPENAI_API_KEY:demo}
            deployment-name: xxx
```
qianfan 配置方式：
```
langchain4j:
    qianfan:
        embedding-model:
            base-url: ${OPENAI_API_BASE:demo}
            api-key: ${OPENAI_API_KEY:demo}
            model-name: xxx
```
dashscope 配置方式：
```
langchain4j:
    dashscope:
        embedding-model:
            api-key: ${OPENAI_API_KEY:demo}
            model-name: xxx
```
其他的方式类似

## Embedding Store
supsersonic支持in-memory、chroma、milvus三种模式；支持后续扩展更多Embedding Store。

in-memory 配置方式：
```
langchain4j:
    in-memory:
        embedding-store:
            persist-path: /tmp
```
chroma 配置方式：
```
langchain4j:
    chroma:
        embedding-store:
            baseUrl: http://0.0.0.0:8000
            timeout: 120s
```
milvus 配置方式：
```
langchain4j:
    milvus:
        embedding-store:
            host: localhost
            port: 2379
            uri: http://0.0.0.0:2379
            token: demo
            dimension: 384
            timeout: 120s   
```

{{< hint info >}}
**注意**
如果是采用了in-memory embedding-store方式，如果修改了EmbeddingModel模型,需要清理一下本地数据：
```
rm  /tmp/InMemory.*collection
rm  /tmp/InMemory.meta_collection
rm  /tmp/InMemory.preset_query_collection
rm  /tmp/InMemory.solved_query_collection
rm  /tmp/InMemory.text2dsl_agent_collection
```
{{< /hint >}}
