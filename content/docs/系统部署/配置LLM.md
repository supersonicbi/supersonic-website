+++
title = "配置LLM"
weight = 3
+++

# 配置LLM

## Chat Model

SuperSonic可以从两个粒度配置Chat Model：

### **1. 系统粒度**
系统粒度有两种方式配置：  
#### **1.1.修改supersonic-env.sh方式**
修改配置文件`conf/supersonic-env.sh`，替换相应的变量

{{< figure src=/img/supersonic_deploy_llm.png#center >}}

#### **1.2.修改application-local.yaml方式**
修改配置文件`conf/application-local.yaml`，替换相应的变量
{{< figure src=/img/supersonic_llm_config.png#center >}}
目前支持：open-ai、zhipu、ollama、azure、qianfan、dashscope；通常情况下各模型会兼容open-ai协议，可以统一采用open-ai方式

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
zhipu 配置方式：
```
langchain4j:
    zhipu:
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
azure 配置方式：
```
langchain4j:
    azure:
        chat-model:
            endpoint: ${OPENAI_API_BASE:demo}
            api-key: ${OPENAI_API_KEY:demo}
            deployment-name: ${OPENAI_MODEL_NAME:gpt-3.5-turbo}
            max-tokens: ${OPENAI_TEMPERATURE:20}
```
qianfan 配置方式：
```
langchain4j:
    qianfan:
        chat-model:
            base-url: ${OPENAI_API_BASE:demo}
            api-key: ${OPENAI_API_KEY:demo}
            model-name: ${OPENAI_MODEL_NAME:gpt-3.5-turbo}
            temperature: ${OPENAI_TEMPERATURE:0.0}
            timeout: ${OPENAI_TIMEOUT:PT60S}
```
dashscope 配置方式：
```
langchain4j:
    dashscope:
        chat-model:
            base-url: ${OPENAI_API_BASE:demo}
            api-key: ${OPENAI_API_KEY:demo}
            model-name: ${OPENAI_MODEL_NAME:gpt-3.5-turbo}
            temperature: ${OPENAI_TEMPERATURE:0.0}
            timeout: ${OPENAI_TIMEOUT:PT60S}
```
其他的方式类似

### **2. 助理粒度**
在助理管理模块，修改助理配置，填入相应的变量
{{< figure src=/img/supersonic_agent_config.png#center >}}

## Embedding Model
### **1. 0.9.2版本及之前**
SuperSonic0.9.2版本及之前，有三种方式配置Embedding模型：

- in_process：默认采用内嵌的BgeSmallZhEmbeddingModel模型；可支持配置本地模型（需符合onnx格式）

- open_ai：采用open_ai提供的Embedding模型

- hugging_face：采用hugging_face提供的Embedding模型

{{< figure src=/img/supersonic_embedding_model.png#center >}}      

注意：如果修改了EmbeddingModel模型,需要清理一下本地数据：
```
rm  /tmp/InMemory.meta_collectio年
rm  /tmp/InMemory.preset_query_collection
rm  /tmp/InMemory.solved_query_collection
rm  /tmp/InMemory.text2dsl_agent_collection
```
### **2. 0.9.2版本之后**
统一采用一种方式配置Embedding模型，支持in-memory、open-ai、zhipu、ollama、azure、qianfan、dashscope

{{< figure src=/img/supersonic_embedding_model_v2.png#center >}}

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
            model-name: xxx
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
        chat-model:
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
            file-path: /tmp
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
            url: http://0.0.0.0:2379
            token: demo
            dimension: 384
            timeout: 120s   
```