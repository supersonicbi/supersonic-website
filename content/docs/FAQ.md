+++
title = "FAQ"
weight = 6
+++

# FAQ

## 项目有没有体验的地址？

A: Playground访问地址：[http://117.72.46.148:9080](http://117.72.46.148:9080)

## 初始启动后为什么能显示DEMO问答对话？

A: 为了便于快速体验，系统内置DEMO语义模型，且实现了基于规则的解析器，所以不需要大模型也可以进行问答对话。不过，规则解析器能力有限，推荐仅用于测试验证，生产使用还是需要大模型解析。

## 是否自带大模型服务？

A: 项目内置langchain4j社区提供的demo API key，但单次请求openai大模型限制在1000 token，因而只能用于快速体验。要正常体验问答对话，请自行申请大模型服务。

## 支持哪些大模型服务？

A: 当前主要支持兼容open_ai接口协议的大模型服务，比如GPT、GLM、DeepSeek、Qwen、Moonshot等。文心和混元正在验证中，敬请期待。

## 是否支持文本知识库？

A: 当前主要聚焦于结构化数据的问答，文本数据将在未来版本加入支持。

## 是否支持多轮对话？

A: 自0.9.2版本起已经支持多轮对话，但默认是关闭的，需要在助理配置里开启。

## 重启系统后为什么配置的助理/模型数据丢失了？

A: 系统默认使用H2内存数据库，如果需要持久化存储需配置DB，参考[文档](https://supersonicbi.github.io/docs/%E7%B3%BB%E7%BB%9F%E9%83%A8%E7%BD%B2/%E9%85%8D%E7%BD%AEdb/)

## 系统默认的账号和密码是什么？

A: 系统默认创建的用户有admin, jack, tom, lucy, alice，密码都是：123456

## 如果要用我自己的数据进行测试，我至少需要经过哪些步骤

A: [连接数据库](https://supersonicbi.github.io/docs/headless-bi/%E8%BF%9E%E6%8E%A5%E6%95%B0%E6%8D%AE%E5%BA%93/) 
-> [构造模型(创建指标和维度)](http://supersonicbi.github.io/docs/headless-bi/%E6%9E%84%E5%BB%BA%E6%A8%A1%E5%9E%8B/) 
-> [组装数据集](http://supersonicbi.github.io/docs/headless-bi/%E7%BB%84%E8%A3%85%E6%95%B0%E6%8D%AE%E9%9B%86/)
-> [创建助理和工具](http://supersonicbi.github.io/docs/chat-bi/%E9%85%8D%E7%BD%AE%E5%8A%A9%E7%90%86/)

## 是否可以提供接口供第三方应用调用？
A: 可以，启动系统后查看swagger接口文档：http://localhost:9080/swagger-ui/index.html
