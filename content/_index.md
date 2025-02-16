+++
title = "项目介绍"
weight = 1
+++



# 项目介绍

{{< hint info >}}
** SuperSonic最新版本为0.9.10，本文档介绍基于该版本的功能。
{{< /hint >}}

SuperSonic是融合Headless BI和Chat BI的新一代数据分析平台，致力于通过自然语言对话来分析数据，与传统交互的分析产品组合，推动数据民主化。SuperSonic提供两套开箱即用的产品界面：
- Headless BI界面，用于构建语义数据模型，并设置数据访问权限。
- Chat BI界面，用于输入自然语言，并获得可视化的数据结果。

{{< figure src=../img/supersonic_demo.gif >}}

## BI新范式融合

当前，BI领域分别在应用架构和产品交互两个层面兴起新的范式：一方面，随着数据应用和产品的百花齐放，Headless BI架构范式致力于构建与治理统一的语义数据模型，通过语义层Open API开放给消费端查询调用，以此提升数据复用，解决口径差异。另一方面，随着以ChatGPT为代表的大语言模型横空出世，Chat BI交互范式致力于通过大模型将自然语言转换成SQL语言，以此降低数据分析门槛。

SuperSonic主张通过两种BI新范式的融合，一方面让数据得到更好的治理与复用，另一方面让大模型更好地理解数据语义，最终使得两者皆受益：

- Headless BI的Query能力，通过自然语言API获得智能拓展。
- Chat BI的Text2SQL能力，通过语义数据模型获得RAG增强。

{{< figure src=../img/supersonic_ideas.png  align="center" >}}

## 项目社区建设

项目开源地址：[https://github.com/tencentmusic/supersonic](https://github.com/tencentmusic/supersonic)

Playground地址：[http://117.72.46.148:9080](http://117.72.46.148:9080)

微信公众号，不定期更新项目发版计划与通知，进入公众号后可获取用户交流群二维码。

{{< figure src=../img/supersonic_wechat_oa.png  align="center" >}}
