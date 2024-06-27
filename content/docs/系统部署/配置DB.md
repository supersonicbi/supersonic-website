+++
title = "配置DB"
weight = 2
+++

# 配置DB

{{< hint danger >}}
**注意**

系统默认使用H2内存数据库, 重启后会丢失数据, 若需要替换为自己的MySQL, 请按以下进行配置.
{{< /hint >}}



## 1. 执行SQL脚本

**初次配置DB**请依次执行conf/db下schema-mysql.sql、 data-mysql.sql, 这两个脚本均为最新表结构

**若是已配置过DB并部署好的服务**, 可参考sql-update.sql, 这里会注明每次功能改动需要改动的表结构

## 2. 配置YAML文件

conf下application-local.yaml中默认的DB配置为H2配置, 替换为自己的MySQL即可

```
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/your_database?useUnicode=true&characterEncoding=UTF-8&useSSL=false&allowMultiQueries=true
    username: your_username
    password: your_password
    driver-class-name: com.mysql.jdbc.Driver
```
