+++
title = "配置LLM"
weight = 2
+++

# 配置LLM

LLM的使用是SuperSonic的重要一环。能显著增强对用户的问题的理解能力，是通过对话形式与用户交互的基石之一。在本项目中对语言模型能力的应用主要在 LLM 和 Embedding 两方面, 且支持Java和Python两种访问语言模型的方式。

首先，关于LLM的配置，我们专门在launchers/standalone/src/main/resources下创建了一个supersonic-env.sh文件，用于LLM的配置，通过在这里配置，Java和Python两种访问LLM的方式都能生效。
<div align="center" >
    <img src=https://github.com/tencentmusic/supersonic/assets/22031277/7beab043-532f-4a30-8ae2-45a2f6160f11  width="60%"  height="60%"/>
    <p>图1-1 配置文件</p>
</div>
除了这里以外，Java和Python两种请求LLM的方式也都能分别配置LLM相关的配置。下面分别介绍这两种访问方式的配置。

## JavaLLMProxy
服务默认启D动方式就为Java访问语言模型的方式，语言模型相关配置可直接通过YAML文件来配置，目前在配置中支持配置访问open-ai的key和LLM模型的名称
<div align="center" >
    <img src=https://github.com/tencentmusic/supersonic/assets/22031277/7a9da92e-84a4-4a4d-9b4c-108d0a6f2e88  width="60%"  height="60%"/>
    <p>图2-1 配置文件</p>
</div>

## PythonLLMProxy
Python访问LLM的方式需要通过`sh assembly/bin/supersonic-daemon.sh start pyllm`来启动Python服务, 该命令同时也会启动Java服务, 但通过Python服务来访问LLM。
Python服务默认使用的模型中，LLM选用闭源模型 gpt-3.5-turbo，Embedding模型选用开源模型 GanymedeNil/text2vec-large-chinese。用户可以根据自己实际需求进行配置更改。

**配置方式**
<div align="center" >
    <img src=https://github.com/tencentmusic/supersonic/assets/22031277/254f53ab-7d7e-413f-a1e1-4bad80d91113  width="60%"  height="60%"/>
    <p>图2-2 配置文件</p>
</div>


#### LLM模型的配置
1. LLM模型相关的配置，在 supersonic/headless/core/src/main/python/config/run_config.ini 进行配置。
2. LLM默认采用OpenAI的闭源模型 gpt-3.5-turbo，用户可以根据自己的实际需要选择LLM模型的提供方，例如Azure、文心一言等。通过[LLMProvider]下的LLM_PROVIDER_NAME 变量进行配置。需要注意的是，现阶段支持配置的模型提供方必须能够被langchain所支持，提供方的名字可以在langchain文档中查询。
3. LLM的相关变量在[LLMModel]下进行配置，例如openAI的模型，需要提供 MODEL_NAME、OPENAI_API_KEY、TEMPERATURE 等参数配置。不同的LLM提供方需要的配置各不相同，用户可以根据实际情况配置相关变量。

#### Embedding模型配置
1. Embedding模型默认采用开源模型 GanymedeNil/text2vec-large-chinese。用户可以根据实际需要配置适合的Embedding模型；通过[Text2Vec]下 HF_TEXT2VEC_MODEL_NAME 变量进行配置，为了使用方便采用托管在HuggingFace的源，初次启动时自动下载模型文件。

#### LLM与embedding配置 FAQ
1. 可以用开源的LLM模型替代OpenAI的GPT模型吗？
   - 暂时不能。我们测试过大部分主流的开源LLM，在实际使用中，在本项目需要LLM提供的逻辑推理和代码生成场景上，开源模型还不能满足需求。
   - 我们会持续跟进开源LLM的最新进展，在有满足要求的开源LLM后，在项目中集成私有化部署开源LLM的能力。
2. 可以用国产的闭源模型替代OpenAI的GPT模型吗？
   - 据部分用户反馈，在他们的场景下文心一言、混元等国产闭源模型的效果与GPT3.5差距不大；整体而言GPT3.5及GPT4适用的场景会更广泛一些。用户可以在自己的场景下修改LLM的相应配置，试一试实际效果。
3. GPT4、GPT3.5、GPT3.5-16k 这几个模型用哪个比较好？
   - GPT3.5、GPT3.5-16k 均能基本满足要求，但会有输出结果不稳定的情况；GPT3.5的token长度限制为4k，在现有CoT策略下，容易出现超过长度限制的情况。
   - GPT4的输出更稳定，但费用成本远超GPT3.5，可以根据实际使用场景进行选择。
4. Embedding模型用其他的可以吗？
   - 可以。可以以该项目[text2vec](https://github.com/shibing624/text2vec)的榜单作为参考，然后在HuggingFace找到对应模型的model card，修改HF_TEXT2VEC_MODEL_NAME变量的取值。
5. 启动时，首次下载Embedding模型需要会链接HuggingFace的源进行下载，如果网络不通怎么办？
   - 可以到HuggingFace的官网找到对应的model card，然后将模型下载到本地。在supersonic/chat/core/src/main/python/config/run_config.ini 中将HF_TEXT2VEC_MODEL_NAME变量配置为模型所在的绝对路径。

## **LLM在text2sql中的应用**
text2sql的功能实现，高度依赖对LLM的应用。通过LLM生成SQL的过程中，利用小样本(few-shots-examples)通过思维链(chain-of-thoughts)的方式对LLM in-context-learning的能力进行引导，对于生成较为稳定且符合下游语法解析规则的SQL非常重要。用户可以根据自身需要，对样本池及样本的数量进行配置，使其更加符合自身业务特点。


## **text2sql运行中更新配置的脚本**
1. 如果在启动项目后，用户需要对text2sql功能的相关配置进行调试，可以在修改相关配置文件后，通过以下2种方式让配置在项目运行中让配置生效。
   - 执行 supersonic-daemon.sh reload llmparser
   - 执行 python examples_reload_run.py
