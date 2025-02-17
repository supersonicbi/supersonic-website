+++
title = "配置DB"
weight = 2
+++

# 配置DB

{{< hint danger >}}
**注意**

系统默认使用H2内存数据库, 重启后会丢失数据, 若需要替换为自己的持久化数据库, 请按以下进行配置.
{{< /hint >}}

## 1. 初次部署

在bin/supersonic-env.sh脚本中配置数据库相关参数，当前系统默认支持 h2, mysql, postgres：

```
# Supported DB_TYPE:  h2, mysql, postgres
export S2_DB_TYPE=mysql
export S2_DB_HOST=localhost
export S2_DB_PORT=3306
export S2_DB_USER=mysql
export S2_DB_PASSWORD=mysql
export S2_DB_DATABASE=mysql
```

## 2. 升级部署

升级部署时，需要将schema升级到最新版本，请手动执行脚本：conf/db/sql-update.sql