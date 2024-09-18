+++
title = "配置LLM"
weight = 3
+++

# 配置LLM

SuperSonic可以从两个粒度配置Chat Model：系统设置和agent上都可以配置大模型；优先级agent级别高于系统设置

### **1. 系统粒度**
系统设置支持设置ChatModel、EmbeddingModel、EmbeddingStore，该设置为全局粒度；
{{< figure src=/img/system_set.png#center >}}

{{< hint info >}}
**注意**
推荐使用open_ai、ollama；其他azure、qianfan、dashscope、zhipu方式理论上也支持，但是待验证；
{{< /hint >}}


### **2. 助理粒度**
在助理管理模块，修改助理配置，填入相应的变量，该设置会覆盖系统设置的配置； 
目前仅支持：open-ai、ollama两种方式；
1、open_ai 用于连接云端模型；通常情况下各云上模型会兼容open-ai协议
2、ollama 用于连接本地模型；由ollama适配不同的模型

open-ai 配置方式：

{{< figure src=/img/supersonic_agent_llm_1.png#center >}}

ollama 配置方式：

{{< figure src=/img/supersonic_agent_llm_2.png#center >}}

